---
name: temple-health-patient-access-launch
description: >-
  Authorize a patient-facing SMART on FHIR app against Temple Health and read the
  authenticated patient's own clinical record — conditions, allergies, medications,
  observations, encounters and documents.
api: openapi/temple-health-patient-api-openapi.yml
operations:
  - getSmartConfiguration
  - readPatient
  - searchCondition
  - searchAllergyIntolerance
  - searchMedicationRequest
  - searchObservation
  - searchEncounter
  - searchDocumentReference
---

# Patient access: launch and read one patient's record

This is the flow the CMS Interoperability and Patient Access rule exists to guarantee. A patient
authorizes your app against their own myTempleHealth account and you read their USCDI data.

**Everything below returns PHI.** Stay inside the patient context the token grants. Never accept
a patient identifier the model produced. Do not log or transcribe response bodies.

Base: `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4`

## 0. Register first — there is no self-service production access

Register the app at `https://fhir.epic.com/Developer/Apps`, then get it approved by Temple Health
against the production endpoint. Registration alone is not access.

## 1. Authorize (SMART standalone launch)

Read endpoints from `getSmartConfiguration`, then run OAuth 2.0 authorization code with PKCE:

- authorize: `https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/authorize`
- token: `https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/token`
- `code_challenge_method=S256` (the only method supported)
- public clients: no secret. Confidential clients may use `client_secret_post`,
  `client_secret_basic` or `private_key_jwt`.

Request the scopes you will actually use, plus `openid fhirUser` for identity and
`offline_access` if you need a refresh token:

```
patient/Patient.read patient/Condition.read patient/AllergyIntolerance.read
patient/MedicationRequest.read patient/Observation.read patient/Encounter.read
patient/DocumentReference.read openid fhirUser offline_access
```

The token response carries the `patient` context parameter — **that** is the id you use. Never
substitute one you inferred.

## 2. Read the patient — `readPatient`

```
GET {base}/Patient/{patient-from-token-context}
Authorization: Bearer {token}
Accept: application/fhir+json
```

Do not call `searchPatient` for this. Demographic search across a hospital's patient index is a
different, higher-risk capability and is not what a patient-access app needs.

## 3. Read the clinical record

Each search is scoped by `patient=` and returns a `Bundle` of `type: searchset`:

| Operation | Request |
|---|---|
| `searchCondition` | `GET {base}/Condition?patient={id}&clinical-status=active` |
| `searchAllergyIntolerance` | `GET {base}/AllergyIntolerance?patient={id}` |
| `searchMedicationRequest` | `GET {base}/MedicationRequest?patient={id}&status=active` |
| `searchObservation` | `GET {base}/Observation?patient={id}&category=vital-signs` |
| `searchEncounter` | `GET {base}/Encounter?patient={id}&date=ge2026-01-01` |
| `searchDocumentReference` | `GET {base}/DocumentReference?patient={id}` |

Rules that apply to every one of them:

- **Only declared parameters work.** Read `searchParam[]` for that resource out of the
  CapabilityStatement first. `Observation` and `Patient` declare 30 each, `DocumentReference` 27.
- **Page by following `Bundle.link[relation="next"]` verbatim.** The URL is opaque and
  server-signed — do not rebuild it from `_count`. `total` may be absent on large sets.
- **`_include` is broadly supported** (`searchInclude: ["*"]`); `_revinclude` is supported for
  `Provenance:target` only.
- **`Observation` needs a `category`.** Ask for `vital-signs`, `laboratory`, `social-history`
  etc. separately rather than pulling the whole resource type.

## 4. Fetch document content

`searchDocumentReference` returns references, not bytes. The attachment URL inside
`content[].attachment.url` points at a `Binary` read. That edge is not searchable — you must
follow the URL from the resource body.

## Error handling

- **401**, empty JSON body, `WWW-Authenticate: Bearer` — token missing or expired. Refresh with
  `offline_access` if you have it, otherwise re-authorize. There is no `OperationOutcome` on this
  response and no pointer to the authorization server.
- **403** — token is valid but the scope was not granted, or the app is not approved for
  production. Check the granted scopes on the token response, not the ones you requested.
- **404** on a resource path you invented returns an **HTML** IIS error page, not FHIR. Parse
  defensively.
- No `Retry-After` or `RateLimit-*` headers exist. Back off exponentially on any 429 or 5xx.
- There is **no idempotency contract** — every resource reports `conditionalCreate: false` and
  `conditionalUpdate: false`. This flow is read-only, so that is not a problem here; it becomes
  one the moment you write.

Full detail: `conventions/temple-health-conventions.yml`, `errors/temple-health-problem-types.yml`.

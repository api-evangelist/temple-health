---
name: temple-health-discover-the-endpoint
description: >-
  Read what the Temple Health FHIR server actually supports before calling it —
  the CapabilityStatement and the SMART configuration are both anonymous, so this
  is the one flow an agent can complete with no credentials at all.
api: openapi/temple-health-metadata-api-openapi.yml
operations:
  - getMetadata
  - getSmartConfiguration
---

# Discover the Temple Health FHIR endpoint

Temple Health publishes no developer documentation of its own. The server's own conformance
documents are the documentation, and both are anonymous. Always run this before anything else:
the supported resource list, the search parameters, and the OAuth endpoints all change with the
Epic release train and are not announced anywhere.

Base: `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4`

## 1. Read the CapabilityStatement — `getMetadata`

```
GET {base}/metadata
Accept: application/fhir+json
```

No token required. Returns a `CapabilityStatement`. Take from it:

- `software.version` and `software.releaseDate` — the Epic build. This is the only version
  signal the endpoint emits. Record it; if it changed since your last run, re-read everything.
- `fhirVersion` — expect `4.0.1`.
- `rest[0].resource[]` — the resource types. Do not assume a resource exists because FHIR
  defines it; ask this list. Each entry carries:
  - `interaction[].code` — `read`, `search-type`, and on 13 resources `create`/`update`.
  - `searchParam[]` — the ONLY search parameters that will be honoured for that resource.
  - `supportedProfile[]` — the US Core profile to validate against before any write.
- `instantiates[]` — confirms US Core 6.1.0 and Bulk Data conformance.
- `rest[0].security.extension` — the SMART `oauth-uris` extension with authorize and token URLs.

Note that `?_format=` is tolerant: an invalid value is ignored rather than rejected, so do not
use a round-trip on `_format` as a health check.

## 2. Read the SMART configuration — `getSmartConfiguration`

```
GET {base}/.well-known/smart-configuration
Accept: application/json
```

No token required. Returns authorize/token endpoints, `capabilities[]`, `grant_types_supported`,
`token_endpoint_auth_methods_supported` and `code_challenge_methods_supported`.

Two things to check before you design a launch:

- `capabilities` must contain the launch mode you intend — `launch-standalone` for a patient
  app, `launch-ehr` for an EHR-embedded app. Both are present today.
- `scopes_supported` on this server lists only five values (`epic.scanning.dmsusername`,
  `fhirUser`, `launch`, `openid`, `profile`). It does **not** enumerate the `patient/*.read`
  clinical scopes even though `permission-patient` and `permission-v2` are declared
  capabilities. Do not treat `scopes_supported` as the complete grantable set — see
  `scopes/temple-health-scopes.yml`.

## Gotchas

- The DSTU2 base has **no** `.well-known/smart-configuration` (404). For DSTU2, read the OAuth
  URLs out of the `Conformance` resource's `oauth-uris` extension instead.
- There is no `/.well-known/oauth-protected-resource` (RFC 9728) and no
  `/.well-known/oauth-authorization-server` (RFC 8414) on any path. The 401 challenge is a bare
  `WWW-Authenticate: Bearer` with no metadata pointer, so you cannot discover the authorization
  server from an error — you must read the SMART document.
- Successful responses can carry an RFC 7234 `Warning: 199 ...` header. Surface it; it is the
  only in-band advisory this API produces.

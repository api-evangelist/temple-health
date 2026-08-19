---
name: temple-health-bulk-data-export
description: >-
  Run an HL7 FHIR Bulk Data (Flat FHIR) Group-level $export against Temple Health
  using SMART Backend Services — population-scale extraction under a data-use
  agreement, not a patient-access flow.
api: openapi/temple-health-bulk-data-api-openapi.yml
operations:
  - bulkExportGroup
  - getMetadata
---

# Bulk Data: Group-level export

The Temple Health R4 endpoint declares conformance to the HL7 FHIR Bulk Data Access IG
(`instantiates` includes `http://hl7.org/fhir/uv/bulkdata/CapabilityStatement/bulk-data`) and the
`Group` resource declares the `group-export` operation. Confirmed live on 2026-08-15.

**This is population-scale PHI.** It is governed by an organizational data-use agreement with
Temple Health, not by patient authorization. Do not expose this operation to a general-purpose
agent. If you are an agent and you were not explicitly configured for a bulk pipeline, stop here.

Base: `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4`

## 1. Authorize with SMART Backend Services

Not the patient flow. Use `client_credentials` with `private_key_jwt` — both are in
`grant_types_supported` / `token_endpoint_auth_methods_supported` on the live SMART configuration.

- Register a JWKS and asymmetric client with Epic and Temple Health up front.
- Sign a client assertion, POST it to
  `https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/token`.
- Request `system/*.read`-class scopes as agreed at onboarding.

## 2. Kick off the export — `bulkExportGroup`

```
GET {base}/Group/{groupId}/$export
Authorization: Bearer {token}
Accept: application/fhir+json
Prefer: respond-async
```

`{groupId}` is assigned by Temple Health; there is no public group directory and you cannot
discover it by search. The response is **202 Accepted** with a `Content-Location` header naming
the status endpoint.

## 3. Poll the status endpoint

```
GET {content-location}
Authorization: Bearer {token}
```

- **202** — still running. Honour `X-Progress` if present; otherwise poll on a fixed backoff.
  There is no `Retry-After` on this server, so choose your own interval and be conservative.
- **200** — complete. The body is the manifest: `transactionTime`, `request`, and `output[]`
  with one `{type, url}` per NDJSON file.

## 4. Download the files

Each `output[].url` is a separate authenticated download of newline-delimited FHIR JSON, one
resource per line. Fetch with the same bearer token. Stream to disk — these are large.

## 5. Clean up

Issue `DELETE {content-location}` when finished so the server can release the job.

## Constraints observed on this endpoint

- No `Retry-After`, no `RateLimit-*` headers on any response. Concurrency is capped per
  registered system at onboarding and the number is not published.
- Responses are `Cache-Control: no-cache,no-store` — nothing is cacheable.
- `Group` declares only `read` and `search-type` interactions plus the `group-export` operation.
  There is no Patient-level or System-level `$export` declared.
- `Provenance` is the only `_revinclude` target on this server, which matters if you are trying
  to reconstruct lineage after an export.

# Temple Health

Temple Health is the brand name of Temple University Health System (TUHS), a Philadelphia-based academic health system anchored at Temple University Hospital and affiliated with the Lewis Katz School of Medicine at Temple University. The system operates Temple University Hospital (Main, Jeanes, Episcopal, Northeastern, and Women & Families campuses), Temple Health Chestnut Hill Hospital, and Fox Chase Cancer Center (NCI-designated), plus outpatient sites across the Philadelphia region.

This repository profiles Temple Health's externally accessible API surface. That surface is dominated by HL7 FHIR endpoints required under the CMS Interoperability and Patient Access Final Rule (CMS-9115-F) and the 21st Century Cures Act — not by a traditional commercial developer program. The hospital system's electronic health record runs on Epic and is presented to patients as myTempleHealth (MyChart).

## Documented APIs

| API | Type | Base URL | Notes |
|---|---|---|---|
| Temple Health FHIR R4 | Clinical / Patient Access | `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4` | Epic-powered FHIR R4 (4.0.1), August 2025 release, US Core-aligned, SMART on FHIR, Bulk Data Group export. Listed in Epic's R4 endpoint registry as "TempleHealth". |
| Temple Health FHIR DSTU2 | Clinical (legacy) | `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2/` | Legacy DSTU2 (1.0.2) endpoint listed in Epic's public DSTU2 registry. |
| myTempleHealth (MyChart) | Patient Portal | `https://my.templehealth.org/MyChartPRD/` | Epic MyChart deployment for Temple Health patients. |
| Temple Health Price Transparency MRF | Hospital Charges (CSV) | `https://www.templehealth.org/sites/default/files/file/` | Per-campus CMS Hospital Price Transparency standard-charges CSVs (Main, Jeanes, Episcopal, Northeastern, Fox Chase Campus, Fox Chase Cancer Center, Chestnut Hill, Women & Families). |

## Authentication

The Temple Health FHIR R4 endpoint exposes a standard SMART App Launch configuration:

- Authorization endpoint: `https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/authorize`
- Token endpoint: `https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/token`
- Discovery: `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/.well-known/smart-configuration`
- Capability statement: `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/metadata`
- Supported scopes include `launch`, `openid`, `profile`, `fhirUser`, plus the standard `patient/*.read`, `user/*.read`, and `system/*.read` SMART scope families.
- Capabilities include `launch-ehr`, `launch-standalone`, `client-public`, `client-confidential-symmetric`, `client-confidential-asymmetric`, `sso-openid-connect`, `authorize-post`, and `permission-v1`/`permission-v2`.
- Authorization-code flow uses PKCE (`code_challenge_methods_supported: ["S256"]`).
- App registration is handled through Epic on FHIR at `https://fhir.epic.com/Developer/Apps`.

The DSTU2 endpoint at the same host (`/FhirProxyPrd/api/FHIR/DSTU2/`) shares the same OAuth 2.0 authorize/token URLs and reports FHIR `1.0.2` with Epic's August 2025 software release.

## Regulatory Context

Temple Health's published APIs exist primarily to comply with:

- **CMS-9115-F** — CMS Interoperability and Patient Access Final Rule (Patient Access API).
- **21st Century Cures Act / ONC Final Rule** — information-blocking provisions requiring patient access to electronic health information via standard FHIR APIs.
- **CMS Hospital Price Transparency Final Rule (45 CFR 180)** — per-hospital machine-readable standard-charges CSVs.

There is no public commercial developer marketplace, no per-call pricing, and no published quantitative rate-limit table. Access is governed by app onboarding agreements with Epic (for the hospital FHIR endpoints) and by the CMS-required public posting (for the price transparency CSVs).

## Repository Layout

| Path | Contents |
|---|---|
| `apis.yml` | apis.json/apis.yml index of every API surface and supporting artifact. |
| `openapi/` | OpenAPI 3.0.3 spec for the Temple Health FHIR R4 API. |
| `capabilities/` | Naftiko capability YAMLs (one per FHIR resource surface) ready to drive sandboxes and MCP/REST adapters. |
| `rules/` | Spectral ruleset enforcing Temple Health's conventions (canonical URLs, FHIR version, USCDI resource coverage, Title Case summaries). |
| `examples/` | Representative request/response payloads for FHIR Patient and Observation searches, SMART configuration, and CapabilityStatement. |
| `json-schema/` | JSON Schema subsets for Patient and Observation. |
| `json-structure/` | JSON Structure shape for the Encounter resource. |
| `json-ld/` | JSON-LD context aligning Temple Health's FHIR surface with schema.org, HL7 FHIR, US Core, LOINC, SNOMED, RxNorm, and UCUM. |
| `vocabulary/` | Domain vocabulary spanning organizations, standards, regulations, FHIR resources, and endpoints. |
| `plans/` | API Commons Plans 0.1 disclosure (all free under CMS mandate). |
| `rate-limits/` | API Commons Rate Limits 0.1 disclosure (limits not publicly published). |
| `finops/` | FinOps Framework / FOCUS disclosure (no consumer-facing billing surface). |

## Notable Absences

- The `Temple-Health` GitHub organization exists (created 2022-04-07) but has zero public repositories — no SDKs, sample apps, or open-source tools are published.
- No published quantitative rate limits on the FHIR endpoints.
- No public commercial developer portal or pricing tiers; access is regulatory-mandated and free.
- No public price estimator tool was discovered (only the machine-readable standard-charges CSVs).
- No interoperability/Cures Act landing page was discovered on templehealth.org; the FHIR endpoint is documented only through Epic's public registry.

## Sources

- Temple Health FHIR R4 CapabilityStatement (live): `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/metadata`
- Temple Health FHIR DSTU2 Conformance (live): `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2/metadata`
- Temple Health SMART configuration (live): `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/.well-known/smart-configuration`
- Epic public R4 endpoint registry: `https://open.epic.com/Endpoints/R4`
- Epic public DSTU2 endpoint registry: `https://open.epic.com/Endpoints/DSTU2`
- Temple Health Price Transparency landing page: `https://www.templehealth.org/pricing-disclaimer`
- Temple Health website: `https://www.templehealth.org/`
- myTempleHealth login: `https://my.templehealth.org/MyChartPRD/Authentication/Login`

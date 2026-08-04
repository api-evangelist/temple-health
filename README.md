# Temple Health (temple-health)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Temple University Health System (Temple Health) is the Philadelphia-based academic health system affiliated with the Lewis Katz School of Medicine at Temple University. It operates Temple University Hospital (Main Campus, Jeanes, Episcopal, Northeastern, Women & Families), Temple Health Chestnut Hill Hospital, Fox Chase Cancer Center, and outpatient sites across the Philadelphia region. Its patient-facing electronic health record runs on Epic, branded myTempleHealth (MyChart), with CMS-mandated HL7 FHIR APIs published at epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4 (and a legacy DSTU2 endpoint at the same host) that expose USCDI-aligned clinical resources to third-party patient-access applications via SMART on FHIR and OAuth 2.0. Temple Health does not publish a separate commercial developer program; its API surface is regulatory-mandated and free at point of use.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/temple-health/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/temple-health/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consumer
- **Access:** 3rd-Party

## Tags

- Academic Medical Center
- CMS Interoperability
- Cures Act
- DSTU2
- Epic
- FHIR
- Fox Chase Cancer Center
- HL7
- Healthcare
- Hospital System
- MyChart
- OAuth 2.0
- Patient Access
- Price Transparency
- R4
- SMART on FHIR
- Temple University
- US Core
- USCDI

## Timestamps

- **Created:** 2026-05-23
- **Modified:** 2026-05-23

## APIs

### Temple Health FHIR R4 API

The Temple Health FHIR R4 API is Temple University Health System's CMS Interoperability and Patient Access (CMS-9115-F) compliant HL7 FHIR Release 4.0.1 endpoint powered by Epic's August 2025 release. It is listed in Epic's public R4 endpoint registry under the organization "TempleHealth" and exposes USCDI-aligned clinical resources — including Patient, Observation, Condition, Encounter, MedicationRequest, AllergyIntolerance, DiagnosticReport, DocumentReference, Procedure, Immunization, and AllergyIntolerance — to third-party patient-access applications using SMART on FHIR and OAuth 2.0 with standalone-patient and EHR launch contexts. The same endpoint covers the Temple University Hospital campuses (Main, Jeanes, Episcopal, Northeastern, Women & Families), Temple Health Chestnut Hill Hospital, and Fox Chase Cancer Center under one Epic instance. Both XML and JSON FHIR payloads are supported.

- **Human URL:** [https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4](https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4)
- **Base URL:** `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4`

#### Tags

- CMS Interoperability
- Cures Act
- Epic
- FHIR
- HL7
- Patient Access
- R4
- SMART on FHIR
- US Core
- USCDI

#### Properties

- [Capability Statement](https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/metadata)
- [Smart Configuration](https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/R4/.well-known/smart-configuration)
- [Authorization](https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/authorize)
- [Token](https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/token)
- [Documentation](https://fhir.epic.com/Documentation)
- [App Registration](https://fhir.epic.com/Developer/Apps)
- [Developer Portal](https://fhir.epic.com/)
- [Endpoint Directory](https://open.epic.com/Endpoints/R4)
- [Implementation Guide](https://hl7.org/fhir/us/core/STU6.1/)
- [Implementation Guide](https://hl7.org/fhir/smart-app-launch/)
- [Implementation Guide](https://hl7.org/fhir/uv/bulkdata/)
- [OpenAPI](openapi/temple-health-temple-health-fhir-r4-api-openapi.yml) — [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
- [Postman Collection](collections/temple-health-temple-health-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/temple-health-temple-health-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)
- [Spectral Ruleset](rules/temple-health-temple-health-fhir-r4-rules.yml)

### Temple Health FHIR DSTU2 API

The legacy Temple Health DSTU2 FHIR endpoint listed in Epic's public DSTU2 endpoint registry under the organization "TempleHealth". It remains available for backward compatibility with older SMART on FHIR apps written against the FHIR DSTU2 (1.0.2) baseline that pre-dates the CMS Interoperability and Patient Access mandate; new integrations should target the R4 endpoint instead. Supported resources include AllergyIntolerance, Binary, CarePlan, Condition, Device, DiagnosticReport, DocumentReference, FamilyMemberHistory, Goal, Immunization, Medication, MedicationOrder, MedicationStatement, Observation, Patient, Practitioner, and Procedure.

- **Human URL:** [https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2/](https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2/)
- **Base URL:** `https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2`

#### Tags

- DSTU2
- Epic
- FHIR
- Legacy
- SMART on FHIR

#### Properties

- [Capability Statement](https://epicaccess.templehealth.org/FhirProxyPrd/api/FHIR/DSTU2/metadata)
- [Authorization](https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/authorize)
- [Token](https://epicaccess.templehealth.org/FhirProxyPrd/oauth2/token)
- [Documentation](https://fhir.epic.com/Specifications)
- [Endpoint Directory](https://open.epic.com/Endpoints/DSTU2)
- [Postman Collection](collections/temple-health-temple-health-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/temple-health-temple-health-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)


#### Tags

- Epic
- MyChart
- Patient Portal

#### Properties

- [Patient Portal](https://my.templehealth.org/MyChartPRD/Authentication/Login)
- [Vendor](https://www.epic.com/software/mychart/)
- [Postman Collection](collections/temple-health-temple-health-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/temple-health-temple-health-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)


#### Tags

- CMS Price Transparency
- CSV
- Hospital Charges
- Open Data

#### Properties

- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-university-hospital-inc-main-campus_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-university-hospital--jeanes-campus_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-university-hospital--northeastern-campus_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-university-hospital--episcopal-campus_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-university-hospital--fox-chase-campus_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/231352156_fox-chase-cancer-center_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/883577015_temple-health--chestnut-hill-hospital_standardcharges.csv)
- [Data File](https://www.templehealth.org/sites/default/files/file/2026-04/232825878_temple-women--families-hospital_standardcharges.csv)
- [Compliance](https://www.cms.gov/hospital-price-transparency)
- [Postman Collection](collections/temple-health-temple-health-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/temple-health-temple-health-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [Website](https://www.templehealth.org/)
- [Patient Portal](https://my.templehealth.org/MyChartPRD/Authentication/Login)
- [Locations](https://www.templehealth.org/locations)
- [About](https://www.templehealth.org/about)
- [Price Transparency](https://www.templehealth.org/pricing-disclaimer)
- [Financial Assistance](https://www.templehealth.org/financial-assistance)
- [Privacy Policy](https://www.templehealth.org/web-privacy-policy)
- [Non Discrimination Notice](https://www.templehealth.org/section-1557-notice-non-discrimination)
- [University](https://www.temple.edu/)
- [Medical School](https://medicine.temple.edu/)
- [Cancer Center](https://www.foxchase.org/)
- [Git Hub](https://github.com/Temple-Health)
- [Compliance](https://www.cms.gov/Regulations-and-Guidance/Guidance/Interoperability/index)
- [Compliance](https://www.healthit.gov/curesrule/)
- [JSON-LD](json-ld/temple-health-context.jsonld) — [JSON-LD](https://www.w3.org/TR/json-ld11/)
- [Vocabulary](vocabulary/temple-health-vocabulary.yml)
- [JSON Schema](json-schema/temple-health-patient-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Schema](json-schema/temple-health-observation-schema.json) — [JSON Schema](https://json-schema.org/specification)
- [JSON Structure](json-structure/temple-health-fhir-encounter-structure.json)
- [Plans](plans/temple-health-plans-pricing.yml)
- [Rate Limits](rate-limits/temple-health-rate-limits.yml)
- [Fin Ops](finops/temple-health-finops.yml)

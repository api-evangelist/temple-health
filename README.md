# Temple Health (temple-health)

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

### myTempleHealth MyChart Patient Portal

myTempleHealth is the patient-facing Epic MyChart deployment used by Temple Health patients to view test results, message providers, request prescription renewals, schedule appointments, pay bills, and grant third-party patient-access apps consent to retrieve their data through Temple Health's underlying FHIR R4 API.

- **Human URL:** [https://my.templehealth.org/MyChartPRD/Authentication/Login](https://my.templehealth.org/MyChartPRD/Authentication/Login)
- **Base URL:** `https://my.templehealth.org/MyChartPRD/`

#### Tags

- Epic
- MyChart
- Patient Portal

#### Properties

- [Patient Portal](https://my.templehealth.org/MyChartPRD/Authentication/Login)
- [Vendor](https://www.epic.com/software/mychart/)
- [Postman Collection](collections/temple-health-temple-health-fhir-r4-api.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/temple-health-temple-health-fhir-r4-api.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### Temple Health Hospital Price Transparency Machine-Readable Files

The Hospital Price Transparency dataset Temple Health publishes per the CMS Hospital Price Transparency Final Rule (45 CFR 180). Each Temple Health hospital files a CSV of standard charges (gross, payer- specific negotiated, de-identified min/max, discounted cash). One file is published per hospital campus and refreshed periodically under the YYYY-MM-prefixed path on templehealth.org.

- **Human URL:** [https://www.templehealth.org/pricing-disclaimer](https://www.templehealth.org/pricing-disclaimer)
- **Base URL:** `https://www.templehealth.org/sites/default/files/file/`

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

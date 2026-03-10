# API Reference Record — Specification

Version: v1.0

The API Reference Record (ARR) governs structured API documentation — endpoints, contracts, authentication, error handling, and examples. It is generated after a Technical Design Document (TDD) is frozen (documenting designed contracts) or after a Release Record (RR) is frozen (documenting released API).

---

## What This Artifact Is Not

- **Not user documentation.** End-user documentation belongs in the UDR. The ARR covers technical API interfaces for developer consumers.
- **Not a system architecture document.** System internals belong in the SAD. The ARR documents the public-facing API surface only.
- **Not a test plan.** API test coverage belongs in the TDD or QAK artifacts. The ARR is reference documentation, not test specification.

---

## Purpose

The ARR serves four roles:

1. **Contract fidelity** — Ensures every public API endpoint is documented accurately
2. **Consumer enablement** — Provides developers with complete request/response schemas and examples
3. **Authentication clarity** — Documents auth requirements per endpoint or globally
4. **Version governance** — Tracks API versioning and deprecation policy

---

## Upstream Dependencies

- Frozen TDD (from EEK) — provides API contracts, interface definitions (sections on API contracts and interface specifications)
- Frozen SAD (from EEK) — provides system boundaries
- Organizational principles: `documentation-principles.md` — defines documentation quality standards

---

## Required Sections

1. Document Control
2. API Overview
3. Authentication
4. Endpoint Documentation
5. Error Reference
6. Versioning and Deprecation

---

## Content Rules

### Document Control
**Rules**
- ARR ID must be present (format: ARR-{PROJECT}-{NNN})
- System name must be present
- Owner must be present as a team or role, not an individual
- Version must be present (format: v{N})
- Status must be one of: Draft | Validated | Frozen
- TDD Reference must be present (the frozen TDD ID this ARR documents)
- API Version must be present (the API version being documented)

**Failure Examples**
- ARR ID absent
- TDD Reference absent
- API Version absent
- Owner listed as an individual person's name

### API Overview
**Rules**
- Brief description of the API's purpose and scope
- Base URL pattern or convention must be stated
- Supported content types must be listed (e.g., application/json)
- Rate limiting policy must be stated (or explicitly stated as "none")
- List of all public endpoints must be provided as a summary table

**Failure Examples**
- API overview absent
- Base URL not stated
- Content types not listed
- Endpoint summary table absent

### Authentication
**Rules**
- Authentication method must be described (e.g., API key, OAuth 2.0, JWT, session token)
- How to obtain credentials must be described
- How to include credentials in requests must be described (e.g., header name, format)
- Per-endpoint auth requirements must be stated if they differ from the global model
- Endpoints that require no authentication must be explicitly listed

**Failure Examples**
- Authentication method not described
- Credential inclusion format not specified
- Endpoints with ambiguous auth requirements

### Endpoint Documentation
**Rules**
- Every public API endpoint from the TDD must be documented
- No endpoints may be documented that are not in the TDD (no undocumented endpoints, no documented-but-removed endpoints)
- Each endpoint must include: HTTP method, path, description, parameters (path, query, header), request body schema (if applicable), response schema (success), status codes (all possible), and error responses
- Each endpoint must have at least one request/response example
- Parameters must include: name, type, required/optional, description, and constraints (if any)

**Failure Examples**
- TDD endpoints missing from documentation
- Endpoints documented that are not in the TDD
- Endpoints without request/response examples
- Parameters without type or required/optional designation
- Missing error response documentation

### Error Reference
**Rules**
- Common error response format must be documented (the standard error response schema)
- All error status codes used across endpoints must be catalogued with meaning
- Each error code must include: status code, error name, description, and when it occurs
- Error response body schema must be documented

**Failure Examples**
- No common error format documented
- Error codes used in endpoint documentation but not in the error reference
- Error codes without descriptions

### Versioning and Deprecation
**Rules**
- Current API version must be stated
- How API versioning works must be described (e.g., URL path, header, query parameter)
- Deprecation policy must be stated: how deprecation is communicated, what the deprecation timeline is, what happens to deprecated endpoints
- Changelog reference must be present (link or inline changelog for the current version)
- If no deprecation policy exists, this must be explicitly stated

**Failure Examples**
- API version absent
- Versioning mechanism not described
- Deprecation policy absent (not even a "none" statement)
- No changelog reference

---

## Format Requirements

- HTTP methods must be uppercase (GET, POST, PUT, DELETE, PATCH)
- Status codes must be numeric (200, 201, 400, 401, 404, 500)
- Request/response examples must use code blocks with the appropriate content type
- Parameter tables must use consistent column structure

---

## Completeness Rules

- All six sections must be present and non-empty
- Every TDD public endpoint documented
- Every endpoint has at least one example
- Authentication requirements stated per endpoint or globally
- API version and deprecation policy stated

---

## Hard Gates

1. **contract_fidelity** — Every public API endpoint from the TDD is documented; no undocumented endpoints; no documented-but-removed endpoints
2. **request_response_completeness** — Each endpoint has: method, path, parameters, request body schema (if applicable), response schema, status codes, and error responses
3. **authentication_documented** — Auth requirements stated per endpoint or globally; no endpoints with ambiguous auth; endpoints requiring no auth explicitly listed
4. **example_coverage** — Each endpoint has at least one request/response example with realistic data
5. **versioning_stated** — API version present; versioning mechanism described; deprecation policy stated (or explicitly noted as absent); changelog reference present

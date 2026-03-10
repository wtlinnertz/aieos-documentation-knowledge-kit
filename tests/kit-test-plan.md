# Documentation & Knowledge Kit — Test Plan

This document contains the structural integrity checks and flow scenario tests for the Documentation & Knowledge Kit. These tests verify that the kit is complete, internally consistent, and capable of producing valid artifacts.

---

## Structural Integrity Checks

Structural checks verify that the kit's files are present, properly named, and internally consistent. These checks do not require AI — they are verifiable by inspection.

### S-01: Four-File Completeness

**Check:** Every governed artifact type has exactly four files: spec, template, prompt, validator.

| Artifact Type | Spec | Template | Prompt | Validator |
|---------------|------|----------|--------|-----------|
| UDR | docs/specs/udr-spec.md | docs/artifacts/udr-template.md | docs/prompts/udr-prompt.md | docs/validators/udr-validator.md |
| ARR | docs/specs/arr-spec.md | docs/artifacts/arr-template.md | docs/prompts/arr-prompt.md | docs/validators/arr-validator.md |
| SKA | docs/specs/ska-spec.md | docs/artifacts/ska-template.md | docs/prompts/ska-prompt.md | docs/validators/ska-validator.md |
| DHR | docs/specs/dhr-spec.md | docs/artifacts/dhr-template.md | docs/prompts/dhr-prompt.md | docs/validators/dhr-validator.md |

**Expected result:** All 16 files present.

---

### S-02: Hard Gate Count Alignment

**Check:** Each spec's declared hard gate count matches the validator's gate checks.

| Artifact Type | Spec Hard Gates | Validator Gates |
|---------------|----------------|----------------|
| UDR | 5 | 5 |
| ARR | 5 | 5 |
| SKA | 4 | 4 |
| DHR | 5 | 5 |

**Expected result:** Counts match for all four artifact types.

---

### S-03: Hard Gate Name Alignment

**Check:** Gate names in specs match gate names in validators (exact string match for JSON output field names).

| Artifact | Spec Gate Names | Validator Gate Names |
|----------|----------------|---------------------|
| UDR | capability_coverage, accuracy_traceability, audience_clarity, task_completeness, currency_metadata | capability_coverage, accuracy_traceability, audience_clarity, task_completeness, currency_metadata |
| ARR | contract_fidelity, request_response_completeness, authentication_documented, example_coverage, versioning_stated | contract_fidelity, request_response_completeness, authentication_documented, example_coverage, versioning_stated |
| SKA | problem_statement_clear, resolution_actionable, scope_bounded, traceability_present | problem_statement_clear, resolution_actionable, scope_bounded, traceability_present |
| DHR | coverage_audit, currency_check, accuracy_sampling, retirement_review, health_score_declared | coverage_audit, currency_check, accuracy_sampling, retirement_review, health_score_declared |

**Expected result:** All gate names match exactly.

---

### S-04: Prompt-to-Spec Reference Integrity

**Check:** Each generation prompt references the correct spec and template. No prompt inlines content rules.

| Prompt | References Spec | References Template | Inlines Rules? |
|--------|----------------|--------------------|----|
| udr-prompt.md | docs/specs/udr-spec.md | docs/artifacts/udr-template.md | No |
| arr-prompt.md | docs/specs/arr-spec.md | docs/artifacts/arr-template.md | No |
| ska-prompt.md | docs/specs/ska-spec.md | docs/artifacts/ska-template.md | No |
| dhr-prompt.md | docs/specs/dhr-spec.md | docs/artifacts/dhr-template.md | No |

**Expected result:** All prompts reference correct spec and template; no inlined rules.

---

### S-05: Validator-to-Spec Reference Integrity

**Check:** Each validator references its spec as the source of truth. Validators do not reference prompts.

| Validator | References Spec | References Prompt? |
|-----------|-----------------|-------------------|
| udr-validator.md | docs/specs/udr-spec.md | No |
| arr-validator.md | docs/specs/arr-spec.md | No |
| ska-validator.md | docs/specs/ska-spec.md | No |
| dhr-validator.md | docs/specs/dhr-spec.md | No |

**Expected result:** All validators reference the correct spec; none reference prompts.

---

### S-06: Template Section Alignment

**Check:** Each template's section headings match the required sections listed in the corresponding spec.

| Artifact | Spec Required Sections | Template Sections |
|----------|----------------------|-------------------|
| UDR | Document Control, Release Scope Summary, Target Audience, Capability Documentation, Task Coverage, Traceability Matrix, Currency Metadata | sections 1-7 (all present) |
| ARR | Document Control, API Overview, Authentication, Endpoint Documentation, Error Reference, Versioning and Deprecation | sections 1-6 (all present) |
| SKA | Document Control, Problem Statement, Affected Scope, Resolution Steps, Verification, Source Traceability | sections 1-6 (all present) |
| DHR | Document Control, Review Scope, Coverage Audit, Currency Check, Accuracy Sampling, Retirement Review, Health Score | sections 1-7 (all present) |

**Expected result:** All template sections match spec required sections.

---

## Flow Scenario Tests

Flow scenarios verify that the kit's artifacts, when produced in order with appropriate inputs, pass validation. These tests require AI execution.

---

### F-01: User Documentation Record Generation and Validation

**Scenario:** Given a frozen RR describing a release with 3+ user-facing capabilities, a frozen PRD, and a frozen WDD, generate a UDR and validate it.

**Setup:**
- Provide: a frozen RR with 3+ released capabilities
- Provide: a frozen PRD with requirements for the released capabilities
- Provide: a frozen WDD with acceptance criteria
- Generate UDR using the UDR prompt
- Validate UDR using the UDR validator

**Expected outcomes:**
- UDR: all 5 gates PASS
- Every RR capability has a documentation section
- Every capability traces to PRD and WDD
- Target audience stated with technical level
- Every capability has at least one task with steps and outcomes
- Currency metadata complete

**Key gate to verify:** Gate 1 (capability_coverage) — confirm every RR capability appears in the documentation.

---

### F-02: API Reference Record Generation and Validation

**Scenario:** Given a frozen TDD with 3+ public API endpoints and a frozen SAD, generate an ARR and validate it.

**Setup:**
- Provide: a frozen TDD with 3+ public API endpoints including request/response schemas
- Provide: a frozen SAD for system boundary context
- Generate ARR using the ARR prompt
- Validate ARR using the ARR validator

**Expected outcomes:**
- ARR: all 5 gates PASS
- Every TDD public endpoint documented
- Each endpoint has method, path, parameters, schemas, status codes, errors
- Authentication requirements stated
- Each endpoint has at least one example
- API version and deprecation policy stated

**Key gate to verify:** Gate 2 (request_response_completeness) — confirm each endpoint has all required fields including error responses.

---

### F-03: Support Knowledge Article Generation and Validation

**Scenario:** Given a frozen PMR describing an incident with user-facing impact, generate a SKA and validate it.

**Setup:**
- Provide: a frozen PMR with incident findings and user-facing impact
- Generate SKA using the SKA prompt
- Validate SKA using the SKA validator

**Expected outcomes:**
- SKA: all 4 gates PASS
- Problem stated from user's perspective
- Resolution steps executable by support staff
- Article scoped to one problem
- Source artifact (PMR) referenced

**Key gate to verify:** Gate 1 (problem_statement_clear) — confirm the problem is described from the user's perspective, not implementation perspective.

---

### F-04: Documentation Health Review Generation and Validation

**Scenario:** Given a documentation corpus of 3+ frozen documentation artifacts and a current RR, generate a DHR and validate it.

**Setup:**
- Provide: 3+ frozen documentation artifacts (mix of UDR, ARR, SKA)
- Provide: current RR with released capabilities
- Generate DHR using the DHR prompt
- Validate DHR using the DHR validator

**Expected outcomes:**
- DHR: all 5 gates PASS
- Every RR capability checked for coverage
- Every documentation artifact checked for currency
- At least 3 accuracy spot-checks performed
- Retirement candidates identified or stated as none
- Health score declared with methodology

**Key gate to verify:** Gate 5 (health_score_declared) — confirm score has methodology with coverage, currency, and accuracy dimensions with weights.

---

## Notes

- All structural checks (S-01 through S-06) should be verified before running flow scenarios.
- Flow scenarios F-01 through F-04 cover all four artifact types.
- The cross-cutting nature of this kit means flow scenarios involve inputs from multiple other kits (REK, EEK, ODK).
- DHR flow scenario (F-04) requires other DKK artifacts to exist first — run F-01 through F-03 before F-04.

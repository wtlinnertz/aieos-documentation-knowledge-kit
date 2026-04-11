# Session Setup: Documentation & Knowledge Kit

Use this file to set up an AI session for each DKK artifact. Find the section for the artifact you're generating or validating. Follow the checklist before starting.

**Rule:** Generate and validate in separate sessions. Do not self-validate.

---

## User Documentation Record (UDR-{PROJECT}-{NNN})

**What you're creating:** End-user documentation governance record verifying every released capability is documented accurately, with audience-appropriate language and task-oriented coverage.

**Required Inputs (confirm before starting):**
- [ ] Frozen RR (RR-{PROJECT}-{NNN}): Frozen and received from REK?
- [ ] Frozen PRD: Available for requirements traceability?
- [ ] Frozen WDD: Available for acceptance criteria?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `capability_coverage`: Every capability from the RR release scope is identified and will be documented
- [ ] `accuracy_traceability`: PRD requirements and WDD acceptance criteria are available to trace claims against
- [ ] `audience_clarity`: Target audience is identified; language level is determined
- [ ] `task_completeness`: User-facing tasks for each capability are identified
- [ ] `currency_metadata`: Version number, product version, and review date are ready to record

**Session Setup:**
1. Load: `docs/prompts/udr-prompt.md`
2. Provide: Frozen RR, frozen PRD, frozen WDD
3. Provide: `docs/specs/udr-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/udr-validator.md`

**Common Failure to Avoid:**
Documenting features by description only without showing how to accomplish tasks. The UDR requires task-oriented documentation: not just "Feature X exists" but "How to accomplish Task Y using Feature X."

---

## API Reference Record (ARR-{PROJECT}-{NNN})

**What you're creating:** Structured API documentation covering every public endpoint with contracts, authentication, error handling, and examples.

**Required Inputs (confirm before starting):**
- [ ] Frozen TDD (from EEK) or frozen RR (from REK): Frozen and received?
- [ ] Frozen SAD: Available for system boundary context?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `contract_fidelity`: All public API endpoints from TDD are identified
- [ ] `request_response_completeness`: Method, path, parameters, schemas, status codes, and errors are available for each endpoint
- [ ] `authentication_documented`: Auth requirements per endpoint or global auth model are known
- [ ] `example_coverage`: Realistic request/response examples can be constructed for each endpoint
- [ ] `versioning_stated`: API version and deprecation policy (if applicable) are known

**Session Setup:**
1. Load: `docs/prompts/arr-prompt.md`
2. Provide: Frozen TDD (API contracts) and frozen SAD (system boundaries)
3. Provide: `docs/specs/arr-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/arr-validator.md`

**Common Failure to Avoid:**
Documenting endpoints without complete error response schemas. Every endpoint must include all possible status codes and error response formats, not just the success path.

---

## Support Knowledge Article (SKA-{PROJECT}-{NNN})

**What you're creating:** A support knowledge base article addressing a specific user problem with actionable resolution steps, written from the user's perspective.

**Required Inputs (confirm before starting):**
- [ ] Source artifact: Frozen RR, frozen PMR, or support ticket data available?
- [ ] Problem identification: Specific problem or closely related problem set defined?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `problem_statement_clear`: Problem can be described from the user's perspective (symptoms, not implementation details)
- [ ] `resolution_actionable`: Resolution steps are known and can be performed by support staff
- [ ] `scope_bounded`: Article will address exactly one problem or closely related problem set
- [ ] `traceability_present`: Source artifact (RR, PMR, or ticket reference) is available to link

**Session Setup:**
1. Load: `docs/prompts/ska-prompt.md`
2. Provide: Frozen RR or frozen PMR or support ticket data
3. Provide: `docs/specs/ska-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/ska-validator.md`

**Common Failure to Avoid:**
Writing the problem statement from the implementation perspective ("The API returns a 500 error when the cache is cold") instead of the user's perspective ("Users see an error message when first accessing the dashboard after a system update").

---

## Documentation Health Review (DHR-{PROJECT}-{NNN})

**What you're creating:** A periodic audit of documentation currency, coverage, and quality across all documentation types for a service or product.

**Required Inputs (confirm before starting):**
- [ ] Frozen UDRs, ARRs, SKAs: At least some documentation artifacts exist to audit?
- [ ] Current RR: Current release state known?
- [ ] Current SRP: Current operational state known (if available from RRK)?

**Pre-Flight Gate Check (verify before generating):**
- [ ] `coverage_audit`: Released capabilities can be enumerated to check documentation coverage
- [ ] `currency_check`: Policy threshold for documentation age is defined
- [ ] `accuracy_sampling`: Current system behavior is available to spot-check documentation claims against
- [ ] `retirement_review`: Deprecated or removed features can be identified to check for stale documentation
- [ ] `health_score_declared`: Scoring methodology is defined (coverage, currency, accuracy dimensions)

**Session Setup:**
1. Load: `docs/prompts/dhr-prompt.md`
2. Provide: All frozen UDRs, ARRs, SKAs + current RR + current SRP (if available)
3. Provide: `docs/specs/dhr-spec.md` (or confirm it is in context)
4. Validate in a separate session: `docs/validators/dhr-validator.md`

**Common Failure to Avoid:**
Declaring a health score without explaining the methodology. "Documentation health: 75/100" without stating how the score was calculated fails the health_score_declared gate. Define the scoring dimensions, weights, and calculation method.

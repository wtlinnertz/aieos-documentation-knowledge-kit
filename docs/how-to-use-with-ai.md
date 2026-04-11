# How to Use This Kit with AI

This guide explains how to set up AI sessions for each artifact in the Documentation & Knowledge Kit workflow. Follow the session setup instructions precisely. Incorrect session setup is the most common cause of poor artifact quality.

---

## Core Discipline

**One artifact per session.** Do not generate multiple artifacts in the same session.

**Separate generation and validation.** Always validate in a new session. Never ask the AI that generated an artifact to validate it. This produces self-validation bias.

**Include full frozen documents.** Do not summarize upstream artifacts. Provide the complete document.


## UDR. Generation Session

**Session setup:**
```
Documents to provide:
1. Frozen RR (Release Record. Full document)
2. Frozen PRD (Product Requirements Document. Full document)
3. Frozen WDD (Work Decomposition Document. Acceptance criteria)
4. docs/specs/udr-spec.md
5. docs/artifacts/udr-template.md
6. docs/principles/documentation-principles.md

Prompt:
"Generate a User Documentation Record using the provided inputs.
Follow the prompt in docs/prompts/udr-prompt.md.
Use the template exactly. Satisfy all hard gates in the spec.
Document every released capability from the RR.
Trace documentation claims to PRD requirements and WDD acceptance criteria.
Do not document features not in the RR. Mark any assumptions with
[ASSUMPTION: reason]. Output pure Markdown."
```

**After generation:** Review the UDR. Confirm:
- Every released capability from the RR has a documentation section
- Documentation claims trace to PRD requirements
- Language is appropriate for the stated audience
- Tasks are covered (how to accomplish each user-facing task)
- Version and currency metadata are present

**Validation session setup:**
```
Documents to provide:
1. The generated UDR (full document)
2. docs/specs/udr-spec.md

Prompt:
"Validate this User Documentation Record against the UDR spec.
Use only the spec as the source of truth for pass/fail criteria.
Do not suggest improvements. Judge only what is explicitly present.
Output JSON using the format defined in docs/validators/udr-validator.md."
```


## ARR. Generation Session

**Session setup:**
```
Documents to provide:
1. Frozen TDD (Technical Design Document. Full document, especially api contracts)
2. Frozen SAD (System Architecture Document. System boundaries)
3. docs/specs/arr-spec.md
4. docs/artifacts/arr-template.md
5. docs/principles/documentation-principles.md

Prompt:
"Generate an API Reference Record using the provided inputs.
Follow the prompt in docs/prompts/arr-prompt.md.
Use the template exactly. Satisfy all hard gates in the spec.
Document every public API endpoint from the TDD.
Include method, path, parameters, request/response schemas, status codes,
and at least one example per endpoint.
Do not invent endpoints not in the TDD. Mark any assumptions with
[ASSUMPTION: reason]. Output pure Markdown."
```

**After generation:** Review the ARR. Confirm:
- Every public API endpoint from the TDD is documented
- Request/response schemas are complete
- Authentication requirements are stated
- Each endpoint has at least one example
- API version and deprecation policy are stated

**Validation session setup:**
```
Documents to provide:
1. The generated ARR (full document)
2. docs/specs/arr-spec.md

Prompt:
"Validate this API Reference Record against the ARR spec.
Use only the spec as the source of truth for pass/fail criteria.
Do not suggest improvements. Judge only what is explicitly present.
Output JSON using the format defined in docs/validators/arr-validator.md."
```


## SKA. Generation Session

**Session setup:**
```
Documents to provide:
1. Frozen RR (if triggered by release) or frozen PMR (if triggered by incident)
   or support ticket data (if triggered on-demand)
2. docs/specs/ska-spec.md
3. docs/artifacts/ska-template.md
4. docs/principles/documentation-principles.md

Prompt:
"Generate a Support Knowledge Article using the provided inputs.
Follow the prompt in docs/prompts/ska-prompt.md.
Use the template exactly. Satisfy all hard gates in the spec.
State the problem from the user's perspective.
Provide specific, ordered resolution steps.
Scope the article to one problem or closely related problem set.
Include traceability to the source artifact. Output pure Markdown."
```

**After generation:** Review the SKA. Confirm:
- Problem is stated from the user's perspective, not implementation perspective
- Resolution steps are specific, ordered, and executable by support staff
- Article addresses exactly one problem or closely related problem set
- Traceability to source artifact is present

**Validation session setup:**
```
Documents to provide:
1. The generated SKA (full document)
2. docs/specs/ska-spec.md

Prompt:
"Validate this Support Knowledge Article against the SKA spec.
Use only the spec as the source of truth for pass/fail criteria.
Do not suggest improvements. Judge only what is explicitly present.
Output JSON using the format defined in docs/validators/ska-validator.md."
```


## DHR. Generation Session

**Session setup:**
```
Documents to provide:
1. All frozen UDRs, ARRs, SKAs for the service/product
2. Current RR (what is released)
3. Current SRP (what is running). If available from rrk
4. docs/specs/dhr-spec.md
5. docs/artifacts/dhr-template.md
6. docs/principles/documentation-principles.md

Prompt:
"Generate a Documentation Health Review using the provided inputs.
Follow the prompt in docs/prompts/dhr-prompt.md.
Use the template exactly. Satisfy all hard gates in the spec.
Audit documentation coverage against released capabilities.
Check documentation currency against policy thresholds.
Spot-check at least 3 documentation claims against current system behavior.
Identify documentation for deprecated features.
Declare a health score with methodology. Output pure Markdown."
```

**After generation:** Review the DHR. Confirm:
- Coverage audit identifies gaps between released capabilities and documentation
- Currency check flags documentation beyond the policy threshold
- At least 3 claims are spot-checked against current behavior
- Deprecated feature documentation is identified for retirement
- Health score is declared with clear methodology

**Validation session setup:**
```
Documents to provide:
1. The generated DHR (full document)
2. docs/specs/dhr-spec.md

Prompt:
"Validate this Documentation Health Review against the DHR spec.
Use only the spec as the source of truth for pass/fail criteria.
Do not suggest improvements. Judge only what is explicitly present.
Output JSON using the format defined in docs/validators/dhr-validator.md."
```


## Troubleshooting

**Validator returns FAIL on multiple gates**
Check that the generation session included all required inputs. Missing inputs are the most common cause of multi-gate failures.

**Capability coverage fails**
The UDR must document every released capability from the RR. Cross-reference the RR's release scope against the UDR's documentation sections. Every capability in the RR must have a corresponding section.

**Accuracy traceability fails**
Documentation claims must trace to PRD requirements and WDD acceptance criteria. If the UDR claims a feature exists, the claim must reference the requirement that defined it. Unsupported claims fail the gate.

**API endpoints missing from ARR**
The ARR must document every public API endpoint from the TDD. Cross-reference the TDD's API contracts against the ARR's endpoint documentation. Undocumented endpoints fail the contract_fidelity gate.

**SKA resolution steps flagged as not actionable**
Support staff must be able to execute the steps without engineering escalation (unless escalation IS the resolution). Steps like "check the database" are not actionable for support staff. Provide specific steps with observable outcomes.

**DHR health score seems arbitrary**
The health score must be declared with a methodology. "70 out of 100" without explaining how the score was calculated fails the health_score_declared gate. State the scoring methodology (e.g., weighted average of coverage, currency, and accuracy dimensions).

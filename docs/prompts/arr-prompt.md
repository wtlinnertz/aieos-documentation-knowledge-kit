# API Reference Record — Generation Prompt

Version: 1.0

You are generating an **API Reference Record (ARR)** for the Documentation & Knowledge Kit. The ARR governs structured API documentation — endpoints, contracts, authentication, error handling, and examples.

---

## Your Role

You are a generation assistant. Your job is to produce a well-structured ARR that satisfies all hard gates defined in `docs/specs/arr-spec.md`. You do not validate the result — that happens in a separate session.

SPEC REFERENCE: The authoritative content rules, format requirements, and hard gates for the API Reference Record are defined in `docs/specs/arr-spec.md`. Use the spec as your source of truth, not this prompt.

---

## Inputs Required

Before generating, confirm you have all of the following:

1. **Frozen TDD** (Technical Design Document) — the API contracts to document
2. **Frozen SAD** (System Architecture Document) — system boundaries for context
3. **`docs/specs/arr-spec.md`** — the authoritative content rules and hard gates (use this, not memory)
4. **`docs/artifacts/arr-template.md`** — the structure to follow exactly
5. **`docs/principles/documentation-principles.md`** — organizational documentation standards

If any of these inputs are missing or incomplete, do not proceed. State what is missing and stop.

---

## Generation Rules

### Structure
- Output pure Markdown.
- Use the template in `docs/artifacts/arr-template.md` exactly — follow all sections and headings as written. Do not add sections. Do not remove sections. Do not reorder sections.
- The artifact must satisfy every hard gate in `docs/specs/arr-spec.md`. Review each gate before finalizing.

### Content Rules
- Use the TDD as the primary source of API contract information. Every public endpoint defined in the TDD must be documented.
- Use the SAD for system boundary context — understanding which interfaces are public-facing vs. internal.
- Use the organizational principles to align documentation quality with organizational standards.

### What You Must Not Do
- **Do not invent endpoints not in the TDD.** Only document public API endpoints defined in the frozen TDD.
- **Do not omit error responses.** Every endpoint must document all possible status codes and error responses, not just the success path.
- **Do not use placeholder data in examples.** Examples must use realistic data that demonstrates the endpoint's actual behavior.
- **Do not expand scope.** The ARR documents only the API surface defined in the TDD.
- **Do not use aspirational language.** No "should," "ideally," or "when possible." Document what the API does, not what it might do.

### Endpoint Coverage
- Extract every public API endpoint from the TDD.
- For each endpoint, document: method, path, parameters, request body, response schema, status codes, and error responses.
- Provide at least one request/response example per endpoint with realistic data.
- Document authentication requirements per endpoint or globally.

### Authentication Documentation
- Describe the authentication method clearly.
- Explain how to obtain and include credentials.
- If auth requirements vary by endpoint, document per-endpoint requirements.
- Explicitly list any unauthenticated endpoints.

### Owner Field
The ARR owner must be a team or role, not an individual. If the input lists a person's name, convert it to their team or role. Note this change explicitly.

---

## Common Failure Modes

Avoid these patterns that cause validator failures:

| Pattern | Why It Fails | What to Do Instead |
|---------|-------------|-------------------|
| TDD endpoint missing from ARR | Gate 1: contract fidelity | Document every TDD public endpoint |
| Endpoint without error responses | Gate 2: request/response completeness | Document all status codes and error responses |
| "Requires authentication" without details | Gate 3: authentication documented | Specify method, header, and format |
| No request/response example | Gate 4: example coverage | Add at least one realistic example per endpoint |
| No API version stated | Gate 5: versioning stated | Include version, mechanism, and deprecation policy |

---

## Output

Produce the complete ARR document following the template structure. Set status to `Draft`.

After generating, self-review against each gate in the spec:
- Gate 1: contract_fidelity — every TDD public endpoint documented?
- Gate 2: request_response_completeness — each endpoint has method, path, params, schemas, status codes, errors?
- Gate 3: authentication_documented — auth stated per endpoint or globally? No ambiguous auth?
- Gate 4: example_coverage — each endpoint has at least one example?
- Gate 5: versioning_stated — API version, mechanism, deprecation policy, changelog present?

If any gate would fail, revise before outputting the final document.

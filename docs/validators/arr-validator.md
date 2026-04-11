# API Reference Record — Validator

This validator evaluates a completed API Reference Record (ARR) against `docs/specs/arr-spec.md`. It is used in a separate AI session from the one that generated the ARR.

**Validator role:** Judge pass/fail. Do not suggest improvements, redesign content, or offer alternatives. Evaluate only what is explicitly present.

---

## Inputs Required

To run this validator, provide:
1. The completed ARR (full document)
2. `docs/specs/arr-spec.md` (the spec — use this as the authoritative rules)

Do not use any other document as the source of truth for pass/fail criteria.

---

## Evaluation Procedure

Evaluate each hard gate in order. For each gate, apply the rules exactly as stated in the spec. Do not infer intent. Do not give partial credit. Ambiguity in the artifact is a failure condition — if you cannot determine whether a gate passes from what is explicitly present, the gate fails.

---

## Hard Gate Checks

### Gate 1: contract_fidelity

Check:
- Every public API endpoint from the TDD (referenced via ARR Document Control) is documented
- No endpoints are documented that are not in the TDD
- No undocumented endpoints remain

**Pass:** All TDD public endpoints are documented; no extra endpoints; no missing endpoints.
**Fail:** Any TDD endpoint missing from documentation; any endpoint documented that is not in the TDD.

---

### Gate 2: request_response_completeness

Check:
- Each endpoint has: HTTP method, path, description, parameters (with name, location, type, required/optional, description), request body schema (if applicable), response schema (success), all possible status codes, and error responses
- Parameters include type and required/optional designation

**Pass:** Every endpoint has all required fields; parameters are fully specified; error responses documented.
**Fail:** Any endpoint missing method, path, parameters, schemas, status codes, or error responses; parameters without type or required/optional.

---

### Gate 3: authentication_documented

Check:
- Authentication method is described
- How to obtain and include credentials is documented
- Per-endpoint auth requirements are stated if they differ from global model
- Endpoints requiring no authentication are explicitly listed

**Pass:** Auth method described; credential inclusion documented; no endpoints with ambiguous auth; unauthenticated endpoints listed.
**Fail:** Auth method not described; credential inclusion not specified; endpoints with ambiguous auth requirements.

---

### Gate 4: example_coverage

Check:
- Each endpoint has at least one request/response example
- Examples use realistic data (not obvious placeholders like "string" or "value")

**Pass:** Every endpoint has at least one example with realistic data.
**Fail:** Any endpoint without a request/response example; examples using only placeholder data.

---

### Gate 5: versioning_stated

Check:
- API version is present
- Versioning mechanism is described (how versioning works)
- Deprecation policy is stated (or explicitly noted as absent)
- Changelog reference is present

**Pass:** API version present; versioning mechanism described; deprecation policy stated; changelog present.
**Fail:** API version absent; versioning mechanism not described; deprecation policy not addressed; no changelog reference.

---

## Output Format

Produce a JSON result in exactly this format:

```json
{
  "status": "PASS | FAIL",
  "summary": "<one sentence verdict>",
  "hard_gates": {
    "contract_fidelity": "PASS | FAIL",
    "request_response_completeness": "PASS | FAIL",
    "authentication_documented": "PASS | FAIL",
    "example_coverage": "PASS | FAIL",
    "versioning_stated": "PASS | FAIL"
  },
  "blocking_issues": [
    {
      "gate": "<gate_name>",
      "description": "<what specifically failed>",
      "location": "<section or field where the failure is>"
    }
  ],
  "warnings": [
    {
      "description": "<non-blocking observation>",
      "location": "<section>"
    }
  ],
  "completeness_score": "<0-100>"
}
```

**Interpretation rules:**
- Any gate failure -> `"status": "FAIL"`
- `blocking_issues` lists exactly the failures — no additional content
- `warnings` are non-blocking; they do not affect status
- `completeness_score` is advisory; it does not override gate results
- If all gates pass, `blocking_issues` is an empty array

---

## Validator Constraints

- Do not suggest how to fix failures
- Do not redesign or improve the ARR
- Do not evaluate writing quality beyond spec requirements
- Do not accept placeholder examples as equivalent to realistic examples
- Evaluate only what is explicitly present in the document

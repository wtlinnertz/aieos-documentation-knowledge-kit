# Documentation Health Review — Validator

This validator evaluates a completed Documentation Health Review (DHR) against `docs/specs/dhr-spec.md`. It is used in a separate AI session from the one that generated the DHR.

**Validator role:** Judge pass/fail. Do not suggest improvements, redesign content, or offer alternatives. Evaluate only what is explicitly present.

---

## Inputs Required

To run this validator, provide:
1. The completed DHR (full document)
2. `docs/specs/dhr-spec.md` (the spec — use this as the authoritative rules)

Do not use any other document as the source of truth for pass/fail criteria.

---

## Evaluation Procedure

Evaluate each hard gate in order. For each gate, apply the rules exactly as stated in the spec. Do not infer intent. Do not give partial credit. Ambiguity in the artifact is a failure condition — if you cannot determine whether a gate passes from what is explicitly present, the gate fails.

---

## Hard Gate Checks

### Gate 1: coverage_audit

Check:
- Every released capability from the current RR is checked for corresponding documentation
- Documented capabilities are mapped to their documentation artifact (UDR or ARR)
- Coverage gaps are listed (capabilities with no corresponding documentation)
- Coverage percentage is stated

**Pass:** All released capabilities checked; gaps identified; coverage percentage stated.
**Fail:** Released capabilities not enumerated; gaps not identified; coverage percentage absent.

---

### Gate 2: currency_check

Check:
- Currency threshold is stated (from principles file policy)
- Every documentation artifact in the corpus is checked against the threshold
- Documents within the threshold are listed as current
- Documents beyond the threshold are listed as potentially stale
- Count of current vs. potentially stale documents is stated

**Pass:** Threshold stated; all documents checked; current vs. stale counts present.
**Fail:** Threshold not stated; documents not checked; counts absent.

---

### Gate 3: accuracy_sampling

Check:
- At least 3 documentation claims are spot-checked against current system behavior
- Each spot-check states: the claim being checked, the source artifact and section, the current behavior observed, and the verdict
- If any inaccuracy is found, the specific discrepancy is described
- If fewer than 3 spot-checks, justification is provided

**Pass:** At least 3 spot-checks (or justified fewer); each has claim, source, observation, verdict; discrepancies described.
**Fail:** Fewer than 3 spot-checks without justification; spot-checks missing claim, source, observation, or verdict; inaccuracies found but not described.

---

### Gate 4: retirement_review

Check:
- Documentation for deprecated or removed features is identified
- Each retirement candidate has: artifact ID, feature it documents, reason for retirement, and recommendation
- If no retirement candidates exist, this is explicitly stated

**Pass:** Retirement candidates identified with all required fields; or explicitly stated as none.
**Fail:** Retirement review absent; candidates without reason or recommendation; section empty without explicit "none" statement.

---

### Gate 5: health_score_declared

Check:
- Overall documentation health score is declared (0-100)
- Scoring methodology is stated with at least coverage, currency, and accuracy dimensions
- Each dimension has a weight
- The score is consistent with the findings in sections 3-6

**Pass:** Score declared; methodology with dimensions and weights; score consistent with findings.
**Fail:** Score absent; no methodology; methodology without dimension weights; score contradicts findings (e.g., high score with significant coverage gaps).

---

## Output Format

Produce a JSON result in exactly this format:

```json
{
  "status": "PASS | FAIL",
  "summary": "<one sentence verdict>",
  "hard_gates": {
    "coverage_audit": "PASS | FAIL",
    "currency_check": "PASS | FAIL",
    "accuracy_sampling": "PASS | FAIL",
    "retirement_review": "PASS | FAIL",
    "health_score_declared": "PASS | FAIL"
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
- Do not redesign or improve the DHR
- Do not evaluate writing quality beyond spec requirements
- Do not accept a health score that contradicts the findings as passing
- Evaluate only what is explicitly present in the document

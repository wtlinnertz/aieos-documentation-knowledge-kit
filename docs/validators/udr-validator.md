# User Documentation Record — Validator

This validator evaluates a completed User Documentation Record (UDR) against `docs/specs/udr-spec.md`. It is used in a separate AI session from the one that generated the UDR.

**Validator role:** Judge pass/fail. Do not suggest improvements, redesign content, or offer alternatives. Evaluate only what is explicitly present.

---

## Inputs Required

To run this validator, provide:
1. The completed UDR (full document)
2. `docs/specs/udr-spec.md` (the spec — use this as the authoritative rules)

Do not use any other document as the source of truth for pass/fail criteria.

---

## Evaluation Procedure

Evaluate each hard gate in order. For each gate, apply the rules exactly as stated in the spec. Do not infer intent. Do not give partial credit. Ambiguity in the artifact is a failure condition — if you cannot determine whether a gate passes from what is explicitly present, the gate fails.

---

## Hard Gate Checks

### Gate 1: capability_coverage

Check:
- Every released capability from the RR (referenced via UDR Document Control) has a corresponding documentation section
- No documentation section describes capabilities not present in the RR
- No released capabilities are undocumented

**Pass:** All RR capabilities have documentation sections; no undocumented capabilities; no documented-but-unbuilt capabilities.
**Fail:** Any RR capability missing from documentation; any capability documented that is not in the RR.

---

### Gate 2: accuracy_traceability

Check:
- A traceability matrix is present mapping capabilities to PRD requirements and WDD acceptance criteria
- Every documented capability has at least one PRD requirement reference
- Every documented capability has at least one WDD acceptance criterion reference
- No capability exists in the documentation without a traceability entry

**Pass:** Traceability matrix is complete; every capability traced to PRD and WDD; no untraced capabilities.
**Fail:** Traceability matrix absent or incomplete; any capability without PRD reference; any capability without WDD reference.

---

### Gate 3: audience_clarity

Check:
- Target audience is explicitly stated
- Audience technical level is stated
- Language guidelines for the audience are stated
- Documentation language is appropriate for the stated audience (no implementation jargon in end-user docs)

**Pass:** Audience stated with technical level and language guidelines; documentation language matches audience.
**Fail:** Audience not stated; technical level absent; implementation jargon present in end-user documentation; language guidelines absent.

---

### Gate 4: task_completeness

Check:
- Every capability has at least one associated task
- Each task has: task name, prerequisites, step-by-step procedure, and expected outcome
- Tasks are written from the user's perspective (what they do), not the system's perspective
- Each task references the capability it exercises

**Pass:** Every capability has tasks; all tasks have prerequisites, steps, and outcomes; tasks are user-perspective.
**Fail:** Any capability without tasks; tasks missing prerequisites, steps, or outcomes; tasks written from system perspective.

---

### Gate 5: currency_metadata

Check:
- Document version is present
- Applicable product version is present
- Last-reviewed date is present
- Next review date or review cadence is present

**Pass:** All currency metadata fields present.
**Fail:** Any currency metadata field absent.

---

## Output Format

Produce a JSON result in exactly this format:

```json
{
  "status": "PASS | FAIL",
  "summary": "<one sentence verdict>",
  "hard_gates": {
    "capability_coverage": "PASS | FAIL",
    "accuracy_traceability": "PASS | FAIL",
    "audience_clarity": "PASS | FAIL",
    "task_completeness": "PASS | FAIL",
    "currency_metadata": "PASS | FAIL"
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
- Do not redesign or improve the UDR
- Do not evaluate writing quality beyond spec requirements
- Do not accept feature descriptions as equivalent to task documentation
- Evaluate only what is explicitly present in the document

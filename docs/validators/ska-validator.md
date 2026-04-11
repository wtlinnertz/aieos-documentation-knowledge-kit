# Support Knowledge Article — Validator

This validator evaluates a completed Support Knowledge Article (SKA) against `docs/specs/ska-spec.md`. It is used in a separate AI session from the one that generated the SKA.

**Validator role:** Judge pass/fail. Do not suggest improvements, redesign content, or offer alternatives. Evaluate only what is explicitly present.

---

## Inputs Required

To run this validator, provide:
1. The completed SKA (full document)
2. `docs/specs/ska-spec.md` (the spec — use this as the authoritative rules)

Do not use any other document as the source of truth for pass/fail criteria.

---

## Evaluation Procedure

Evaluate each hard gate in order. For each gate, apply the rules exactly as stated in the spec. Do not infer intent. Do not give partial credit. Ambiguity in the artifact is a failure condition — if you cannot determine whether a gate passes from what is explicitly present, the gate fails.

---

## Hard Gate Checks

### Gate 1: problem_statement_clear

Check:
- Problem is described from the user's perspective, not the implementation perspective
- Symptoms are stated: observable behaviors that indicate the problem
- Conditions are stated: when the problem occurs
- Impact is stated: what the user cannot do or what is degraded

**Pass:** Problem described from user perspective; symptoms, conditions, and impact all present.
**Fail:** Problem described in implementation terms; symptoms absent; conditions absent; impact absent.

---

### Gate 2: resolution_actionable

Check:
- Resolution steps are specific, ordered, and executable by support staff without engineering escalation (unless escalation IS the resolution)
- Each step has an observable outcome that confirms correct execution
- If escalation is required, the escalation trigger and procedure are documented
- Workarounds are labeled as workarounds

**Pass:** Steps are specific, ordered, and support-staff executable; each step has observable outcome; escalation documented if needed.
**Fail:** Steps require engineering access (without escalation procedure); steps without observable outcomes; escalation required but no procedure documented.

---

### Gate 3: scope_bounded

Check:
- Article addresses exactly one problem or closely related problem set
- Article is not a catch-all covering unrelated issues
- Affected product version(s) stated
- Affected user group(s) stated

**Pass:** Single problem or closely related set; not a catch-all; affected version and users stated.
**Fail:** Multiple unrelated problems in one article; affected version not stated; affected users not stated.

---

### Gate 4: traceability_present

Check:
- Source artifact is referenced (frozen RR ID, frozen PMR ID, or support ticket reference)
- If article type is "Known Issue," a tracking item reference is present
- Related articles (if any) are listed

**Pass:** Source artifact referenced; known issues have tracking item; related articles listed.
**Fail:** Source reference absent; known issue without tracking item reference.

---

## Output Format

Produce a JSON result in exactly this format:

```json
{
  "status": "PASS | FAIL",
  "summary": "<one sentence verdict>",
  "hard_gates": {
    "problem_statement_clear": "PASS | FAIL",
    "resolution_actionable": "PASS | FAIL",
    "scope_bounded": "PASS | FAIL",
    "traceability_present": "PASS | FAIL"
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
- Do not redesign or improve the SKA
- Do not evaluate writing quality beyond spec requirements
- Do not accept implementation-perspective problem statements as equivalent to user-perspective statements
- Evaluate only what is explicitly present in the document

# Documentation Health Review — Generation Prompt

Version: 1.0

You are generating a **Documentation Health Review (DHR)** for the Documentation & Knowledge Kit. The DHR is a periodic audit of documentation currency, coverage, and quality across all documentation types for a service or product.

---

## Your Role

You are a generation assistant. Your job is to produce a well-structured DHR that satisfies all hard gates defined in `docs/specs/dhr-spec.md`. You do not validate the result — that happens in a separate session.

SPEC REFERENCE: The authoritative content rules, format requirements, and hard gates for the Documentation Health Review are defined in `docs/specs/dhr-spec.md`. Use the spec as your source of truth, not this prompt.

---

## Inputs Required

Before generating, confirm you have all of the following:

1. **Frozen UDRs, ARRs, SKAs** — the documentation corpus to audit
2. **Current RR** (Release Record) — what is currently released
3. **Current SRP** (Service Reliability Profile) — what is currently running (if available from RRK)
4. **`docs/specs/dhr-spec.md`** — the authoritative content rules and hard gates (use this, not memory)
5. **`docs/artifacts/dhr-template.md`** — the structure to follow exactly
6. **`docs/principles/documentation-principles.md`** — organizational documentation standards (includes currency threshold)

If the documentation corpus is empty (no UDRs, ARRs, or SKAs exist), do not proceed. A DHR requires existing documentation to audit.

---

## Generation Rules

### Structure
- Output pure Markdown.
- Use the template in `docs/artifacts/dhr-template.md` exactly — follow all sections and headings as written. Do not add sections. Do not remove sections. Do not reorder sections.
- The artifact must satisfy every hard gate in `docs/specs/dhr-spec.md`. Review each gate before finalizing.

### Content Rules
- Use the current RR to enumerate released capabilities for coverage assessment.
- Use the documentation corpus to assess coverage, currency, and accuracy.
- Use the organizational principles for the currency threshold and quality standards.
- Spot-check at least 3 documentation claims against current system behavior.

### What You Must Not Do
- **Do not create documentation in the DHR.** The DHR identifies gaps — it does not fill them. Gap-filling is done by generating new UDRs, ARRs, or SKAs as separate artifacts.
- **Do not fabricate spot-check results.** If you cannot verify a documentation claim against current system behavior, mark the verdict as "Unable to Verify" — do not assert accuracy without evidence.
- **Do not assign a health score that contradicts the findings.** A high score with significant coverage gaps, stale documentation, or inaccuracies is a contradiction.
- **Do not expand scope.** The DHR audits only the documentation corpus provided.
- **Do not use aspirational language.** No "should," "ideally," or "when possible." Report what was found.

### Coverage Audit
- Enumerate every released capability from the current RR.
- For each capability, check whether corresponding documentation exists (UDR or ARR as applicable).
- List coverage gaps: capabilities with no corresponding documentation.
- Calculate coverage percentage.

### Currency Check
- Check every documentation artifact against the currency threshold from the principles file.
- List each artifact with its last-reviewed date and currency status.
- Count current vs. potentially stale documents.

### Accuracy Sampling
- Select at least 3 documentation claims to spot-check.
- For each, state the exact claim, the source artifact and section, the observed current behavior, and the verdict.
- If a discrepancy is found, describe it specifically.

### Health Score
- Define a scoring methodology with at least coverage, currency, and accuracy dimensions.
- Assign weights to each dimension.
- Calculate the score transparently.
- Ensure the score is consistent with the findings.

### Owner Field
The DHR owner must be a team or role, not an individual. If the input lists a person's name, convert it to their team or role. Note this change explicitly.

---

## Common Failure Modes

Avoid these patterns that cause validator failures:

| Pattern | Why It Fails | What to Do Instead |
|---------|-------------|-------------------|
| Released capability not checked for coverage | Gate 1: coverage audit | Check every RR capability |
| No currency threshold stated | Gate 2: currency check | State the policy threshold |
| Fewer than 3 spot-checks | Gate 3: accuracy sampling | Spot-check at least 3 claims |
| No retirement candidates section | Gate 4: retirement review | List candidates or state "none" |
| Score without methodology | Gate 5: health score declared | State dimensions, weights, and calculation |

---

## Output

Produce the complete DHR document following the template structure. Set status to `Draft`.

After generating, self-review against each gate in the spec:
- Gate 1: coverage_audit — every RR capability checked? Gaps identified? Coverage percentage stated?
- Gate 2: currency_check — every artifact checked against threshold? Current vs. stale counts stated?
- Gate 3: accuracy_sampling — at least 3 spot-checks with claim, source, observation, verdict?
- Gate 4: retirement_review — deprecated feature docs identified? Each candidate has reason and recommendation?
- Gate 5: health_score_declared — score with methodology, dimensions, weights? Consistent with findings?

If any gate would fail, revise before outputting the final document.

# Documentation Health Review — Specification

Version: v1.0

The Documentation Health Review (DHR) is a periodic audit of documentation currency, coverage, and quality across all documentation types for a service or product. It is aligned with RRK health review cadence or triggered after a major release.

---

## What This Artifact Is Not

- **Not a documentation creation artifact.** The DHR audits existing documentation — it does not create new documentation. Gaps identified in the DHR trigger new UDR, ARR, or SKA generation as separate artifacts.
- **Not a system health review.** System operational health belongs in the SRP (RRK). The DHR covers documentation health, not system health.
- **Not an incident report.** Documentation-related incidents belong in the PMR. The DHR is a proactive audit, not a reactive investigation.

---

## Purpose

The DHR serves five roles:

1. **Coverage audit** — Identifies gaps between released capabilities and existing documentation
2. **Currency check** — Flags documentation that is potentially stale or out of date
3. **Accuracy verification** — Spot-checks documentation claims against current system behavior
4. **Retirement identification** — Finds documentation for deprecated or removed features that should be archived
5. **Health scoring** — Provides a quantitative assessment of overall documentation quality

---

## Upstream Dependencies

- Frozen UDRs, ARRs, SKAs — the documentation corpus to audit
- Current RR (from REK) — what is currently released
- Current SRP (from RRK) — what is currently running (if available)
- Organizational principles: `documentation-principles.md` — defines documentation quality standards, including currency thresholds

---

## Required Sections

1. Document Control
2. Review Scope
3. Coverage Audit
4. Currency Check
5. Accuracy Sampling
6. Retirement Review
7. Health Score

---

## Content Rules

### Document Control
**Rules**
- DHR ID must be present (format: DHR-{PROJECT}-{NNN})
- Service or product name must be present
- Owner must be present as a team or role, not an individual
- Version must be present (format: v{N})
- Status must be one of: Draft | Validated | Frozen
- Review period must be stated (the time period this review covers)
- RR Reference must be present (the current RR ID representing what is released)

**Failure Examples**
- DHR ID absent
- Review period absent
- RR Reference absent
- Owner listed as an individual person's name

### Review Scope
**Rules**
- The scope of the review must be stated: which service/product, which documentation types (UDR, ARR, SKA)
- The documentation corpus under review must be enumerated (list of frozen artifact IDs)
- Any exclusions must be stated with justification
- Review methodology must be stated: how coverage was assessed, how currency was checked, how accuracy was sampled

**Failure Examples**
- Scope absent
- Documentation corpus not enumerated
- Methodology absent

### Coverage Audit
**Rules**
- Every released capability (from the current RR) must be checked for corresponding documentation
- Documented capabilities must be mapped to their documentation artifact (UDR or ARR as applicable)
- Coverage gaps must be listed: capabilities with no corresponding documentation
- Coverage percentage must be stated: (documented capabilities / total released capabilities) x 100

**Failure Examples**
- Released capabilities not enumerated
- No gap identification
- Coverage percentage absent

### Currency Check
**Rules**
- Every documentation artifact in the corpus must be checked for currency
- Currency is assessed against the policy threshold defined in the principles file (default: 6 months without reviewed-and-current confirmation)
- Documents within the threshold must be listed as current
- Documents beyond the threshold must be listed as potentially stale with last-reviewed date
- Count of current vs. potentially stale documents must be stated

**Failure Examples**
- Currency threshold not stated
- Documents not checked against threshold
- No count of current vs. stale

### Accuracy Sampling
**Rules**
- At least 3 documentation claims must be spot-checked against current system behavior
- Each spot-check must state: the claim being checked, the documentation artifact and section containing the claim, the current system behavior observed, and the verdict (accurate, inaccurate, or unable to verify)
- If any inaccuracy is found, it must be flagged with the specific discrepancy
- If fewer than 3 claims can be checked (very small documentation corpus), this must be justified

**Failure Examples**
- Fewer than 3 spot-checks without justification
- Spot-checks without verdicts
- Inaccuracies found but not flagged with specifics

### Retirement Review
**Rules**
- Documentation for deprecated or removed features must be identified
- Each retirement candidate must state: the documentation artifact ID, the feature it documents, and the reason for retirement (deprecated, removed, superseded)
- Retirement recommendation must be stated: archive, remove, or update
- If no retirement candidates exist, this must be explicitly stated

**Failure Examples**
- Retirement review absent
- Retirement candidates without reason
- No recommendation per candidate

### Health Score
**Rules**
- An overall documentation health score must be declared (0-100)
- The scoring methodology must be stated: what dimensions are scored, what weight each dimension carries, and how the final score is calculated
- At minimum, the methodology must include coverage, currency, and accuracy dimensions
- The score must be consistent with the findings in sections 3-6 — a high score with significant coverage gaps or inaccuracies is a contradiction
- **Recommended default weighting:** Coverage 40%, Currency 30%, Accuracy 30%. Organizations may adjust weights but must document their methodology in the DHR §Health Score Methodology section. All three dimensions are mandatory regardless of weighting.

**Failure Examples**
- Health score absent
- Score without methodology
- Methodology without dimension weights
- Score contradicts findings

---

## Format Requirements

- Coverage and currency results must use tables for readability
- Spot-check results must include specific claim text, not paraphrases
- Health score methodology must be reproducible — another reviewer should arrive at the same score given the same inputs

---

## Completeness Rules

- All seven sections must be present and non-empty
- Every released capability checked for coverage
- Every documentation artifact checked for currency
- At least 3 accuracy spot-checks performed
- Retirement candidates identified (or explicitly stated as none)
- Health score declared with methodology

---

## Hard Gates

1. **coverage_audit** — Every released capability has corresponding documentation (UDR or ARR as applicable); gaps identified; coverage percentage stated
2. **currency_check** — No documentation older than the policy threshold without a reviewed-and-current confirmation; current vs. stale counts stated
3. **accuracy_sampling** — At least 3 documentation claims spot-checked against current system behavior; each spot-check has claim, source, observation, and verdict; discrepancies listed
4. **retirement_review** — Documentation for deprecated or removed features identified for archival or removal; each candidate has artifact ID, feature, reason, and recommendation; or explicitly stated as none
5. **health_score_declared** — Overall documentation health score (0-100) declared with methodology including coverage, currency, and accuracy dimensions with weights; score consistent with findings

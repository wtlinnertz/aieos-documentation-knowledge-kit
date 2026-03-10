# Documentation Health Review

---

## 1. Document Control

| Field | Value |
|-------|-------|
| DHR ID | DHR-{PROJECT}-{NNN} |
| Service/Product Name | {service or product name} |
| Owner | {team or role — not an individual person} |
| Version | v{N} |
| Status | Draft / Validated / Freeze Pending / Frozen |
| Review Period | {e.g., 2026-Q1, or 2026-01-01 to 2026-03-31} |
| RR Reference | {RR-{PROJECT}-{NNN} — current release} |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

---

## 2. Review Scope

**Service/Product:** {name of the service or product under review}

**Documentation Types Reviewed:** {UDR, ARR, SKA — list which types are in scope}

**Documentation Corpus:**

| Artifact ID | Type | Title/Subject | Status |
|-------------|------|---------------|--------|
| {artifact ID} | {UDR/ARR/SKA} | {title} | {Frozen/Draft} |
| {artifact ID} | {UDR/ARR/SKA} | {title} | {Frozen/Draft} |

*List every documentation artifact under review.*

**Exclusions:** {any documentation excluded from this review, with justification — or "None"}

**Review Methodology:** {how coverage was assessed, how currency was checked, how accuracy was sampled}

---

## 3. Coverage Audit

### Released Capabilities vs. Documentation

| Capability | Source (RR section) | Documentation Artifact | Coverage Status |
|-----------|--------------------|-----------------------|-----------------|
| {capability name} | {RR section reference} | {UDR/ARR ID or "NONE"} | {Covered / Gap} |
| {capability name} | {RR section reference} | {UDR/ARR ID or "NONE"} | {Covered / Gap} |

### Coverage Gaps

| Capability | Expected Documentation Type | Gap Description |
|-----------|---------------------------|-----------------|
| {capability name} | {UDR / ARR} | {what documentation is missing} |

*If no gaps, state: "No coverage gaps identified."*

**Coverage Percentage:** {documented capabilities / total released capabilities x 100}%

---

## 4. Currency Check

**Currency Threshold:** {policy threshold, e.g., "6 months without reviewed-and-current confirmation"}

### Documentation Currency Status

| Artifact ID | Type | Last Reviewed | Age (months) | Currency Status |
|-------------|------|--------------|-------------|-----------------|
| {artifact ID} | {UDR/ARR/SKA} | {YYYY-MM-DD} | {N} | {Current / Potentially Stale} |
| {artifact ID} | {UDR/ARR/SKA} | {YYYY-MM-DD} | {N} | {Current / Potentially Stale} |

**Summary:** {N} current, {N} potentially stale out of {N} total documents.

---

## 5. Accuracy Sampling

### Spot-Check 1

| Field | Value |
|-------|-------|
| Claim | {exact claim text from the documentation} |
| Source | {artifact ID, section reference} |
| Current System Behavior | {what was actually observed} |
| Verdict | {Accurate / Inaccurate / Unable to Verify} |
| Discrepancy | {specific discrepancy, if inaccurate — or "N/A"} |

### Spot-Check 2

| Field | Value |
|-------|-------|
| Claim | {exact claim text from the documentation} |
| Source | {artifact ID, section reference} |
| Current System Behavior | {what was actually observed} |
| Verdict | {Accurate / Inaccurate / Unable to Verify} |
| Discrepancy | {specific discrepancy, if inaccurate — or "N/A"} |

### Spot-Check 3

| Field | Value |
|-------|-------|
| Claim | {exact claim text from the documentation} |
| Source | {artifact ID, section reference} |
| Current System Behavior | {what was actually observed} |
| Verdict | {Accurate / Inaccurate / Unable to Verify} |
| Discrepancy | {specific discrepancy, if inaccurate — or "N/A"} |

*Minimum 3 spot-checks. Add more as appropriate.*

---

## 6. Retirement Review

### Retirement Candidates

| Artifact ID | Feature Documented | Reason | Recommendation |
|-------------|-------------------|--------|----------------|
| {artifact ID} | {feature name} | {Deprecated / Removed / Superseded} | {Archive / Remove / Update} |

*If no retirement candidates, state: "No retirement candidates identified. All documented features remain current."*

---

## 7. Health Score

**Overall Documentation Health Score:** {0-100}

### Scoring Methodology

| Dimension | Weight | Score | Weighted Score |
|-----------|--------|-------|----------------|
| Coverage | {weight, e.g., 40%} | {0-100} | {weighted} |
| Currency | {weight, e.g., 30%} | {0-100} | {weighted} |
| Accuracy | {weight, e.g., 30%} | {0-100} | {weighted} |

**Calculation:** {description of how each dimension score was determined}

**Score Justification:** {why this score is consistent with the findings in sections 3-6}

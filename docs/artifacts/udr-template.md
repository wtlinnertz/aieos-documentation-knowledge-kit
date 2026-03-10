# User Documentation Record

---

## 1. Document Control

| Field | Value |
|-------|-------|
| UDR ID | UDR-{PROJECT}-{NNN} |
| System Name | {system name — must match RR} |
| Owner | {team or role — not an individual person} |
| Version | v{N} |
| Status | Draft / Validated / Freeze Pending / Frozen |
| RR Reference | {RR-{PROJECT}-{NNN}} |
| PRD Reference | {PRD-{PROJECT}-{NNN}} |
| Governance Model Version | 1.0 |
| Prompt Version | {prompt version} |
| Spec Version | {spec version} |
| Principles Version | {principles file versions} |

---

## 2. Release Scope Summary

**Release Summary:** {brief summary of what was released, sourced from the RR}

**Released Capabilities:**

| Capability ID | Capability Name | Description |
|---------------|----------------|-------------|
| {capability reference from RR} | {name} | {brief description} |
| {capability reference from RR} | {name} | {brief description} |

*List every released capability from the RR's release scope.*

---

## 3. Target Audience

| Field | Value |
|-------|-------|
| Primary Audience | {e.g., end users, administrators, business analysts} |
| Technical Level | {e.g., non-technical, technical but not developers, domain experts} |
| Language Guidelines | {e.g., no implementation jargon, use business terminology, avoid acronyms without definition} |

---

## 4. Capability Documentation

### 4.1 {Capability Name}

| Field | Value |
|-------|-------|
| Capability ID | {capability reference from RR} |
| Description | {what this capability does — in audience-appropriate language} |
| User Benefit | {why this capability matters to the user} |

### 4.2 {Capability Name}

| Field | Value |
|-------|-------|
| Capability ID | {capability reference from RR} |
| Description | {what this capability does — in audience-appropriate language} |
| User Benefit | {why this capability matters to the user} |

*Add one section per released capability. Every RR capability must appear here.*

---

## 5. Task Coverage

### Task 1: {Task Name}

| Field | Value |
|-------|-------|
| Related Capability | {capability ID from section 4} |
| Prerequisites | {what the user must have or do before starting} |

**Steps:**
1. {Step 1 — from the user's perspective}
2. {Step 2}
3. {Step 3}

**Expected Outcome:** {what the user should see or achieve upon completion}

### Task 2: {Task Name}

| Field | Value |
|-------|-------|
| Related Capability | {capability ID from section 4} |
| Prerequisites | {what the user must have or do before starting} |

**Steps:**
1. {Step 1 — from the user's perspective}
2. {Step 2}
3. {Step 3}

**Expected Outcome:** {what the user should see or achieve upon completion}

*At least one task per capability. Add additional tasks as needed.*

---

## 6. Traceability Matrix

| Capability ID | Capability Name | PRD Requirement | WDD Acceptance Criterion |
|---------------|----------------|-----------------|--------------------------|
| {capability ID} | {name} | {PRD-{PROJECT}-{NNN} section reference} | {WDD acceptance criterion reference} |
| {capability ID} | {name} | {PRD-{PROJECT}-{NNN} section reference} | {WDD acceptance criterion reference} |

*Every documented capability must have at least one PRD requirement and one WDD acceptance criterion.*

---

## 7. Currency Metadata

| Field | Value |
|-------|-------|
| Document Version | v{N} |
| Applicable Product Version | {product version this documentation covers} |
| Last Reviewed Date | {YYYY-MM-DD} |
| Next Review Date | {YYYY-MM-DD or review cadence, e.g., "quarterly"} |

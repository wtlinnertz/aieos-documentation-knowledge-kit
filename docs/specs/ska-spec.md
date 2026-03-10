# Support Knowledge Article — Specification

Version: v1.0

The Support Knowledge Article (SKA) governs support team knowledge base articles — troubleshooting guides, FAQs, and known issues. It is generated after a Release Record (RR) is frozen (new capabilities), after an Operational Diagnostics postmortem report (PMR) is frozen (incident learnings), or on-demand for recurring support issues.

---

## What This Artifact Is Not

- **Not user documentation.** End-user capability documentation belongs in the UDR. The SKA covers troubleshooting and problem resolution, not feature usage.
- **Not an incident report.** Incident investigation and root cause analysis belong in the PMR. The SKA translates incident learnings into actionable support knowledge.
- **Not an API reference.** API documentation belongs in the ARR. The SKA covers user-facing problems and resolutions, not technical interface specifications.

---

## Purpose

The SKA serves three roles:

1. **Problem documentation** — Captures user-facing problems in user-appropriate language
2. **Resolution guidance** — Provides specific, actionable resolution steps that support staff can execute
3. **Knowledge capture** — Preserves incident learnings and support patterns as reusable knowledge

---

## Upstream Dependencies

- Frozen RR (from REK) — provides release context for new capability support articles
- Frozen PMR (from ODK) — provides incident findings for incident learning articles
- Support ticket patterns (human input) — provides recurring issue data for on-demand articles
- Organizational principles: `documentation-principles.md` — defines documentation quality standards

At least one of the first three inputs is required. Not all three are needed simultaneously.

---

## Required Sections

1. Document Control
2. Problem Statement
3. Affected Scope
4. Resolution Steps
5. Verification
6. Source Traceability

---

## Content Rules

### Document Control
**Rules**
- SKA ID must be present (format: SKA-{PROJECT}-{NNN})
- Article title must be present and descriptive (from the user's perspective)
- Owner must be present as a team or role, not an individual
- Version must be present (format: v{N})
- Status must be one of: Draft | Validated | Frozen
- Source Reference must be present (the frozen RR ID, frozen PMR ID, or support ticket reference that triggered this article)
- Article type must be stated: Troubleshooting | FAQ | Known Issue

**Failure Examples**
- SKA ID absent
- Article title written from implementation perspective
- Source Reference absent
- Article type absent

### Problem Statement
**Rules**
- Problem must be described from the user's perspective — what the user sees or experiences, not what the system does internally
- Symptoms must be stated: observable behaviors that indicate the problem
- Conditions must be stated: when the problem occurs (specific scenarios, triggers, or prerequisites)
- Impact must be stated: what the user cannot do or what is degraded

**Failure Examples**
- Problem described from implementation perspective ("The cache invalidation fails")
- Symptoms absent
- Conditions absent
- Impact absent

### Affected Scope
**Rules**
- Affected product version(s) must be stated
- Affected user group(s) must be stated (e.g., all users, administrators only, users of feature X)
- Affected environment(s) must be stated if relevant (e.g., all environments, production only)

**Failure Examples**
- Product version not stated
- Affected users not stated

### Resolution Steps
**Rules**
- Resolution steps must be specific, ordered, and executable by support staff without engineering escalation (unless escalation IS the resolution)
- Each step must have an observable outcome that confirms the step was executed correctly
- If the resolution requires escalation to engineering, the escalation trigger and escalation procedure must be documented
- Workarounds must be clearly labeled as workarounds, distinct from permanent resolutions
- If no resolution exists (known issue with no fix), this must be explicitly stated with expected resolution timeline

**Failure Examples**
- Steps requiring engineering access for support staff
- Steps without observable outcomes
- Escalation required but no escalation procedure documented
- Workaround not labeled as workaround

### Verification
**Rules**
- How to verify the resolution was successful must be stated
- What the user should see after successful resolution must be described
- If verification requires specific actions, those actions must be documented step-by-step

**Failure Examples**
- No verification procedure
- Verification stated as "confirm it works" without specifics

### Source Traceability
**Rules**
- Source artifact must be referenced: frozen RR ID, frozen PMR ID, or support ticket reference
- If triggered by a known issue, a tracking item reference must be present
- Related articles (if any) must be listed

**Failure Examples**
- Source reference absent
- Known issue without tracking item reference

---

## Format Requirements

- Steps must be numbered sequentially
- Each step must be a single action with an observable outcome
- Escalation procedures must be in a clearly labeled subsection

---

## Completeness Rules

- All six sections must be present and non-empty
- Problem described from user's perspective
- Resolution steps are actionable by support staff
- Verification procedure present
- Source traceability present

---

## Hard Gates

1. **problem_statement_clear** — Problem described from the user's perspective, not implementation perspective; symptoms, conditions, and impact stated
2. **resolution_actionable** — Resolution steps are specific, ordered, and executable by support staff without engineering escalation (unless escalation IS the resolution); each step has an observable outcome
3. **scope_bounded** — Article addresses exactly one problem or closely related problem set; not a catch-all; affected version, users, and environment stated
4. **traceability_present** — Links to source artifact (RR, PMR, or ticket reference); known issue articles link to tracking item

# User Documentation Record — Specification

Version: v1.0

The User Documentation Record (UDR) governs end-user documentation for a released capability. It ensures every released capability is documented, documentation claims trace to engineering artifacts, language is audience-appropriate, and documentation is task-oriented. It is generated after a Release Record (RR) is frozen or after a significant feature change.

---

## What This Artifact Is Not

- **Not the documentation itself.** The UDR is a governance record that ensures documentation quality — it defines what must be documented and verifies that it was. The actual user-facing documentation lives in the organization's documentation platform.
- **Not an API reference.** API documentation belongs in the ARR. The UDR covers user-facing capabilities, not technical interfaces.
- **Not a support article.** Troubleshooting and FAQs belong in the SKA. The UDR covers how to use the system, not how to fix problems.

---

## Purpose

The UDR serves four roles:

1. **Capability coverage** — Ensures every released capability has corresponding documentation
2. **Accuracy traceability** — Ensures documentation claims trace to PRD requirements and WDD acceptance criteria
3. **Audience alignment** — Ensures documentation language is appropriate for the stated audience
4. **Task orientation** — Ensures documentation covers how to accomplish tasks, not just feature descriptions

---

## Upstream Dependencies

- Frozen Release Record (RR) — provides the release scope (what was released)
- Frozen Product Requirements Document (PRD) — provides requirements for traceability
- Frozen Work Decomposition Document (WDD) — provides acceptance criteria for accuracy verification
- Organizational principles: `documentation-principles.md` — defines documentation quality standards

---

## Required Sections

1. Document Control
2. Release Scope Summary
3. Target Audience
4. Capability Documentation
5. Task Coverage
6. Traceability Matrix
7. Currency Metadata

---

## Content Rules

### Document Control
**Rules**
- UDR ID must be present (format: UDR-{PROJECT}-{NNN})
- System name must be present and match the RR system name
- Owner must be present as a team or role, not an individual
- Version must be present (format: v{N})
- Status must be one of: Draft | Validated | Frozen
- RR Reference must be present (the frozen RR ID this UDR documents)
- PRD Reference must be present (the frozen PRD ID for traceability)

**Failure Examples**
- UDR ID absent
- System name does not match RR
- Owner listed as an individual person's name
- RR Reference absent
- PRD Reference absent

### Release Scope Summary
**Rules**
- Brief summary of what was released, sourced from the RR
- List of all released capabilities from the RR's release scope
- Each capability must have a capability ID or reference for traceability

**Failure Examples**
- Release scope absent
- Capabilities listed without IDs or references
- Capabilities in UDR not present in the RR

### Target Audience
**Rules**
- Target audience must be explicitly stated (e.g., "end users," "administrators," "business analysts")
- Audience technical level must be stated (e.g., "non-technical," "technical but not developers," "domain experts")
- Language guidelines for this audience must be stated (e.g., "no implementation jargon," "use business terminology")

**Failure Examples**
- Target audience absent
- Audience stated without technical level
- No language guidelines for the audience

### Capability Documentation
**Rules**
- Every released capability from the RR must have a corresponding documentation section
- Each documentation section must include: capability name, description (what it does), and user benefit (why it matters)
- No documentation section may describe capabilities not present in the RR (no undocumented features, no documented-but-unbuilt features)
- Language must be appropriate for the stated target audience — no implementation jargon in end-user docs

**Failure Examples**
- RR capabilities missing from documentation
- Capabilities documented that are not in the RR
- Implementation jargon in end-user documentation
- Capability sections without user benefit

### Task Coverage
**Rules**
- Every user-facing task enabled by the released capabilities must be documented
- Each task must include: task name, prerequisite conditions, step-by-step procedure, and expected outcome
- Tasks must be written from the user's perspective (what they do), not the system's perspective (what the system does)
- Each task must reference the capability it exercises

**Failure Examples**
- Capabilities without associated tasks
- Tasks without step-by-step procedures
- Tasks written from the system's perspective
- Tasks without expected outcomes

### Traceability Matrix
**Rules**
- A matrix mapping each documented capability to its PRD requirement and WDD acceptance criterion
- Every capability must have at least one PRD requirement reference
- Every capability must have at least one WDD acceptance criterion reference
- No capability may exist in the documentation without a traceability entry

**Failure Examples**
- Traceability matrix absent
- Capabilities without PRD references
- Capabilities without WDD references
- Capabilities in documentation but not in traceability matrix

### Currency Metadata
**Rules**
- Document version must be present
- Applicable product version must be present (the version of the product this documentation covers)
- Last-reviewed date must be present
- Next review date must be present or review cadence must be stated

**Failure Examples**
- Document version absent
- Product version absent
- Last-reviewed date absent
- No review date or cadence

---

## Format Requirements

- Capability IDs must be consistent with the RR's capability references
- All traceability references must use the artifact ID format (e.g., PRD-{PROJECT}-{NNN} section reference)
- Tasks must be numbered step-by-step procedures

---

## Completeness Rules

- All seven sections must be present and non-empty
- Every RR capability documented
- Every capability traced to PRD and WDD
- Every capability has at least one task
- Currency metadata complete

---

## Hard Gates

1. **capability_coverage** — Every released capability from the RR has a corresponding documentation section; no undocumented capabilities, no documented-but-unbuilt capabilities
2. **accuracy_traceability** — Documentation claims trace to PRD requirements and WDD acceptance criteria; traceability matrix is complete with no untraced capabilities
3. **audience_clarity** — Target audience explicitly stated with technical level; language appropriate for stated audience; no implementation jargon in end-user docs
4. **task_completeness** — Documentation covers how to accomplish each user-facing task with prerequisites, steps, and expected outcomes; not just feature descriptions
5. **currency_metadata** — Version, last-reviewed date, and applicable product version are present; review cadence or next review date stated

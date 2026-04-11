# Documentation & Knowledge Kit — Playbook

This playbook defines the process for the Documentation & Knowledge Kit (Layer 13). Unlike sequential kits, this kit uses trigger-based activation — each artifact type is triggered at a different point in the delivery pipeline.

---

## Trigger-Based Artifact Flow

This kit does not follow a single linear flow. Artifacts are triggered independently:

```
Trigger A: RR frozen (from REK, Layer 5)
         |
         |---> User Documentation Record (UDR) -> generate -> validate -> freeze
         |
         |---> Support Knowledge Article (SKA) -> generate -> validate -> freeze
         |     (UDR and SKA may run in parallel)
         |
         |---> API Reference Record (ARR) -> generate -> validate -> freeze
               (if public API was released)

Trigger B: TDD frozen (from EEK, Layer 4)
         |
         v
  API Reference Record (ARR) -> generate -> validate -> freeze
  (documents API contracts before release)

Trigger C: PMR frozen (from ODK, Layer 8) or on-demand
         |
         v
  Support Knowledge Article (SKA) -> generate -> validate -> freeze
  (captures incident learnings or recurring support patterns)

Trigger D: Periodic (semi-annual minimum) or after major release
         |
         v
  Documentation Health Review (DHR) -> generate -> validate -> freeze
  (requires existing frozen UDRs, ARRs, SKAs to audit)
```

### Dependency Rules

- **UDR** depends on a frozen RR from REK. It also requires the frozen PRD (for requirements traceability) and frozen WDD (for acceptance criteria).
- **ARR** depends on a frozen TDD from EEK (for API contracts) or a frozen RR from REK (for released API). It also requires the frozen SAD (for system boundaries).
- **SKA** has no dependency on other DKK artifacts. It depends on a frozen RR or frozen PMR, or can be triggered on-demand from support ticket patterns.
- **DHR** depends on existing frozen UDRs, ARRs, and SKAs to audit. It also references the current RR (what is released) and current SRP (what is running).

---

## Upstream Interface

**Primary upstream:** Release & Exposure Kit (REK, Layer 5)

### For User Documentation Record (UDR)

**Input:** Frozen Release Record (RR) + frozen PRD + frozen WDD
**Dependency:** RR release scope (what was released), PRD requirements (what was built), WDD acceptance criteria (how it should work)

The RR must be frozen before UDR generation begins. If the RR is absent or incomplete, do not generate the UDR. Request a completed RR from the REK team.

### For API Reference Record (ARR)

**Input:** Frozen TDD (from EEK) or frozen RR (from REK) + frozen SAD
**Dependency:** TDD API contracts and interface definitions, SAD system boundaries

The TDD or RR must be frozen before ARR generation begins. The ARR documents API contracts as designed (from TDD) or as released (from RR).

### For Support Knowledge Article (SKA)

**Input:** Frozen RR (from REK) or frozen PMR (from ODK) or support ticket patterns (human input)
**Dependency:** RR release scope (new capabilities), PMR incident findings (learnings), or recurring support issue patterns

SKA can be triggered by any of these inputs independently. It does not require all three.

### For Documentation Health Review (DHR)

**Input:** All frozen UDRs, ARRs, SKAs for the service/product + current RR + current SRP
**Dependency:** Complete documentation corpus, current release state, current operational state

DHR requires enough documentation to audit. Do not generate a DHR if no documentation artifacts exist yet.

---

## Trigger A — User Documentation Record and Support Knowledge Article

### User Documentation Record (UDR)

**Artifact:** User Documentation Record (UDR)
**Type:** Generated
**Spec:** `docs/specs/udr-spec.md` (5 hard gates)
**Template:** `docs/artifacts/udr-template.md`
**Prompt:** `docs/prompts/udr-prompt.md`
**Validator:** `docs/validators/udr-validator.md`

### Purpose

The UDR governs end-user documentation for a released capability. It ensures every released capability is documented, documentation claims trace to engineering artifacts, language is audience-appropriate, and documentation is task-oriented.

### Inputs

- Frozen RR (from REK)
- Frozen PRD (from PIK or EEK)
- Frozen WDD (from EEK) — for acceptance criteria
- `docs/principles/documentation-principles.md` (organizational documentation policy)

### Process

1. Confirm the RR is frozen. Do not proceed with a draft or unfrozen RR.
2. In a new AI session, provide: frozen RR + frozen PRD + frozen WDD + `docs/specs/udr-spec.md` + `docs/artifacts/udr-template.md` + `docs/principles/documentation-principles.md`. Use the UDR prompt (`docs/prompts/udr-prompt.md`).
3. Review the generated UDR. Confirm that every released capability has a documentation section, documentation claims trace to PRD requirements, language is appropriate for the stated audience, and tasks are covered.
4. Validate the UDR in a separate session using `docs/validators/udr-validator.md` and the spec.
5. On PASS: documentation owner reviews and freezes.
6. On FAIL: address blocking issues and re-generate or correct; re-validate.

### Freeze Points

- UDR must be frozen before it can be cited in DHR audits
- Frozen UDR provides the documentation evidence for the released capability

---

### Support Knowledge Article (SKA) — Post-Release

**Artifact:** Support Knowledge Article (SKA)
**Type:** Generated
**Spec:** `docs/specs/ska-spec.md` (4 hard gates)
**Template:** `docs/artifacts/ska-template.md`
**Prompt:** `docs/prompts/ska-prompt.md`
**Validator:** `docs/validators/ska-validator.md`

### Purpose

The SKA governs support knowledge base articles for new capabilities introduced by a release. These help support staff assist users with the new functionality.

### Inputs

- Frozen RR (from REK)
- Support ticket patterns (human input, if available)
- `docs/principles/documentation-principles.md`

### Process

1. Confirm the RR is frozen and the release introduced user-facing changes that warrant support articles.
2. In a new AI session, provide: frozen RR + support ticket patterns (if available) + `docs/specs/ska-spec.md` + `docs/artifacts/ska-template.md` + `docs/principles/documentation-principles.md`. Use the SKA prompt (`docs/prompts/ska-prompt.md`).
3. Review the generated SKA. Confirm the problem is stated from the user's perspective, resolution steps are actionable, the article is scoped to one problem, and traceability is present.
4. Validate in a separate session using `docs/validators/ska-validator.md` and the spec.
5. On PASS: documentation owner reviews and freezes.
6. On FAIL: address blocking issues; re-generate or correct; re-validate.

### Freeze Points

- SKA must be frozen before it can be cited in DHR audits
- Frozen SKA is the authoritative support article for the identified problem

---

## Trigger B — API Reference Record

**Artifact:** API Reference Record (ARR)
**Type:** Generated
**Spec:** `docs/specs/arr-spec.md` (5 hard gates)
**Template:** `docs/artifacts/arr-template.md`
**Prompt:** `docs/prompts/arr-prompt.md`
**Validator:** `docs/validators/arr-validator.md`

### Purpose

The ARR governs structured API documentation — endpoints, contracts, authentication, error handling. It can be generated after TDD freeze (documenting designed contracts) or after release (documenting released API).

### Inputs

- Frozen TDD (from EEK) — API contracts, interface definitions
- Frozen SAD (from EEK) — system boundaries
- `docs/principles/documentation-principles.md`

### Process

1. Confirm the TDD is frozen and contains API contract definitions.
2. In a new AI session, provide: frozen TDD + frozen SAD + `docs/specs/arr-spec.md` + `docs/artifacts/arr-template.md` + `docs/principles/documentation-principles.md`. Use the ARR prompt (`docs/prompts/arr-prompt.md`).
3. Review the generated ARR. Confirm that every public API endpoint is documented, request/response schemas are complete, authentication requirements are stated, and examples are provided.
4. Validate in a separate session using `docs/validators/arr-validator.md` and the spec.
5. On PASS: documentation owner reviews and freezes.
6. On FAIL: address blocking issues; re-generate or correct; re-validate.

### Freeze Points

- ARR must be frozen before it can be cited in DHR audits
- ARR should be frozen before or shortly after release for public APIs

---

## Trigger C — Support Knowledge Article (Post-Incident or On-Demand)

**Artifact:** Support Knowledge Article (SKA)
**Type:** Generated
**Spec:** `docs/specs/ska-spec.md` (4 hard gates)
**Template:** `docs/artifacts/ska-template.md`
**Prompt:** `docs/prompts/ska-prompt.md`
**Validator:** `docs/validators/ska-validator.md`

### Purpose

The SKA captures incident learnings or addresses recurring support patterns. When triggered by a PMR, the SKA translates technical incident findings into user-facing or support-staff-facing knowledge.

### Inputs

- Frozen PMR (from ODK) — incident findings and learnings
- Support ticket patterns (human input) — recurring issue data
- `docs/principles/documentation-principles.md`

### Process

1. Identify the source: frozen PMR or recurring support pattern.
2. In a new AI session, provide: frozen PMR or support ticket data + `docs/specs/ska-spec.md` + `docs/artifacts/ska-template.md` + `docs/principles/documentation-principles.md`. Use the SKA prompt (`docs/prompts/ska-prompt.md`).
3. Review the generated SKA. Confirm problem statement is from the user's perspective, resolution steps are actionable, scope is bounded, and traceability is present.
4. Validate in a separate session using `docs/validators/ska-validator.md` and the spec.
5. On PASS: documentation owner reviews and freezes.
6. On FAIL: address blocking issues; re-generate or correct; re-validate.

### Freeze Points

- SKA must be frozen before it can be cited in DHR audits

---

## Trigger D — Documentation Health Review

**Artifact:** Documentation Health Review (DHR)
**Type:** Generated
**Spec:** `docs/specs/dhr-spec.md` (5 hard gates)
**Template:** `docs/artifacts/dhr-template.md`
**Prompt:** `docs/prompts/dhr-prompt.md`
**Validator:** `docs/validators/dhr-validator.md`

### Purpose

The DHR is a periodic audit of documentation currency, coverage, and quality. It identifies gaps, stale documentation, and documentation for deprecated features that should be retired.

### Cadence

DHR should be generated at least semi-annually, aligned with the RRK health review cadence. Additionally, generate DHR after any major release that significantly changes user-facing behavior. If no RRK cadence is established, default to quarterly.

### Inputs

- All frozen UDRs, ARRs, SKAs for the service/product
- Current RR (what is released)
- Current SRP (what is running) — if available from RRK
- `docs/principles/documentation-principles.md`

### Process

1. Confirm that documentation artifacts exist to audit. Do not generate a DHR if no UDRs, ARRs, or SKAs have been produced.
2. In a new AI session, provide: all frozen documentation artifacts + current RR + current SRP (if available) + `docs/specs/dhr-spec.md` + `docs/artifacts/dhr-template.md` + `docs/principles/documentation-principles.md`. Use the DHR prompt (`docs/prompts/dhr-prompt.md`).
3. Review the generated DHR. Confirm coverage gaps are identified, currency is checked, accuracy sampling is performed, retirement candidates are listed, and health score is declared.
4. Validate in a separate session using `docs/validators/dhr-validator.md` and the spec.
5. On PASS: documentation owner reviews and freezes.
6. On FAIL: address blocking issues; re-generate or correct; re-validate.

### Freeze Points

- DHR findings may trigger new UDR, ARR, or SKA generation to address gaps
- DHR health score feeds into operational health assessment

---

## Downstream Handoffs

### To Insight & Evolution Kit (IEK, Layer 7)

**Handoff artifact:** Frozen DHR
**Purpose:** Documentation health patterns feed Portfolio Evolution Signals
**What IEK receives:** DHR coverage gaps, currency issues, and health scores may indicate systematic documentation debt.

### To Reliability & Resilience Kit (RRK, Layer 6)

**Handoff artifact:** Frozen DHR
**Purpose:** Documentation health contributes to operational health
**What RRK receives:** DHR health score provides documentation dimension of operational readiness.

---

## Freeze Points Summary

| Artifact | When Frozen | What It Gates |
|----------|------------|---------------|
| UDR | After RR freeze + validation | DHR audit input; documentation evidence for capability |
| ARR | After TDD or RR freeze + validation | DHR audit input; API documentation evidence |
| SKA | After RR/PMR freeze or on-demand + validation | DHR audit input; support knowledge base |
| DHR | After periodic audit + validation | Triggers gap-filling documentation; feeds IEK and RRK |

---

## Session Discipline

Follow these rules in every AI session:

| Rule | Why |
|------|-----|
| One artifact per session | Prevents context contamination across artifacts |
| Separate generation and validation sessions | Prevents self-validation bias |
| Include full frozen upstream artifacts | Do not summarize; the AI needs complete context |
| Include spec and template for generation sessions | The AI generates against the spec, not from memory |
| Include spec and validator for validation sessions | The validator judges against the spec, not against the generated content |

Do not ask the AI that generated an artifact to also validate it in the same session.

---

## Re-Entry Protocol

When a frozen artifact must be corrected:

1. Identify the artifact to be changed (UDR, ARR, SKA, or DHR).
2. Identify all downstream artifacts that reference it or depend on it.
3. Assess the impact:
   - UDR change: Does it affect DHR coverage assessment?
   - ARR change: Does it affect DHR coverage assessment? Are downstream integrations referencing this API documentation?
   - SKA change: Does it affect DHR coverage assessment?
   - DHR change: Does it affect IEK portfolio signals or RRK operational health?
4. Issue a new version of the artifact.
5. Re-validate the new version.
6. Re-validate all affected downstream artifacts that reference the changed artifact.
7. Document the change in the new version's document control section with a reference to the original and the reason for the correction.

---

## Amendment Procedure

A frozen artifact may be corrected in place without re-validation when **all** of the following criteria are met:

1. The correction does not affect any field evaluated by a hard gate.
2. The correction does not change scope, decisions, owners, or technical specifications.
3. The correction does not affect any field referenced by a downstream artifact.

**Procedure:** Make the correction and add an Amendment Log entry to the artifact's Document Control section: date, what changed, materiality criterion cited, and who authorized the change. No re-validation is required.

**If there is any ambiguity** about whether a change is non-material, treat it as material and issue a new artifact version. The amendment path must not become a workaround for the version protocol.

---

## Principle File Revision

When the principle file in `docs/principles/` changes, use the change categories defined in `aieos-governance-foundation/docs/principle-file-standard.md`:

| Change Category | Version Bump | Re-Entry Impact |
|----------------|-------------|-----------------|
| **Minor** (clarification only) | `v_.x -> v_.x+1` | No re-entry required; already-frozen artifacts remain valid |
| **Significant** (new requirement or tightened constraint) | `v1.x -> v1.x+1` | Review artifacts generated after the change against updated principles; already-frozen artifacts are grandfathered |
| **Breaking** (removal or loosening) | `vN.x -> vN+1.0` | Requires documentation owner authorization and documented business justification; re-entry may be warranted |

Every change to a principle file must bump the version field, even minor clarifications.

---

## Maintaining the Engagement Record

The Engagement Record (ER) is a project-level artifact that lives in the consuming project at `docs/engagement/er-{initiative}.md`. It spans all AIEOS layers and is maintained by each kit's operators as work passes through. The ER spec and format are defined in `aieos-governance-foundation/docs/engagement-record-spec.md`.

**DKK maintains the documentation and knowledge section of the ER.**

### What to Update

| Trigger | ER update |
|---------|-----------|
| UDR frozen | Add UDR ID to artifact table |
| ARR frozen | Add ARR ID to artifact table |
| SKA frozen | Add SKA ID to artifact table |
| DHR frozen | Add DHR ID to artifact table; note health score |
| Documentation gap identified in DHR | Record gap in key decisions section |

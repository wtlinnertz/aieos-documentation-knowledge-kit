# CLAUDE.md — Documentation & Knowledge Kit

## What This Repository Is

This is the **Documentation & Knowledge Kit** — an AIEOS kit that governs user-facing documentation, API references, support knowledge bases, and documentation health. It is Layer 13 of the AIEOS system, operating as a cross-cutting kit that interacts with multiple layers rather than occupying a single sequential position in the pipeline.

## Repository Structure

```
docs/
  principles/          # Organizational documentation quality policy (input material)
  specs/               # Content rules and hard gates per artifact type
  artifacts/           # Templates
  prompts/             # AI generation prompts
  validators/          # Quality gate definitions
  playbook.md          # Process definition with trigger points
  index.md             # Documentation entry point
  how-to-adapt.md      # Organizational adoption guidance
  how-to-use-with-ai.md # AI tool usage guide
  session-setup.md     # Per-artifact session setup checklists
  governance-model.md  # AIEOS structural rules (reference)
  entry-from-eek.md    # Boundary briefing from Engineering Execution Kit
  entry-from-rek.md    # Boundary briefing from Release & Exposure Kit
  entry-from-odk.md    # Boundary briefing from Operational Diagnostics Kit
examples/              # Worked examples
tests/                 # Structural integrity checks
```

## Artifact Types

This kit produces four governed artifact types:

1. **User Documentation Record (UDR)** — Governs end-user documentation for released capabilities. Generated after REK release (frozen RR) or after significant feature change.
2. **API Reference Record (ARR)** — Governs structured API documentation — endpoints, contracts, authentication, error handling. Generated after TDD freeze or after REK release.
3. **Support Knowledge Article (SKA)** — Governs support knowledge base articles — troubleshooting guides, FAQs, known issues. Generated after REK release, after ODK postmortem, or on-demand.
4. **Documentation Health Review (DHR)** — Periodic audit of documentation currency, coverage, and quality. Aligned with RRK health review cadence or after major release.

Each artifact type has exactly four governing files: spec, template, prompt, validator.

## Key Rules

- **Specs are the source of truth** — prompts and validators reference specs, never inline rules
- **Validators judge, they do not help** — no suggestions, no redesign
- **Freeze before promote** — upstream artifacts must be frozen before downstream generation
- **Separate generation and validation** — different AI sessions to prevent self-validation bias
- **No scope expansion** — downstream artifacts must not expand scope beyond upstream
- **No inferred information** — mark missing information explicitly, do not fill gaps
- **Cross-cutting triggers** — artifacts are triggered at different pipeline points, not in a single linear flow
- **Governance model sync** — `docs/governance-model.md` is a synchronized copy of `aieos-governance-foundation/governance-model.md` (canonical authority). Do not edit kit copy directly; update `aieos-governance-foundation` first, then sync all kit copies to match exactly. See governance-model.md section 15 for versioning and change protocol.
- **Engagement Record** — DKK maintains the documentation and knowledge section of the project's ER. Add artifact IDs as they freeze. See `docs/playbook.md` and `aieos-governance-foundation/docs/engagement-record-spec.md`.

## Artifact Flow

This kit uses trigger-based activation rather than a single linear flow:

```
Trigger A: RR frozen (from REK, Layer 5)
  -> User Documentation Record (UDR) -> validate -> freeze
  -> Support Knowledge Article (SKA) -> validate -> freeze
  (UDR and SKA may run in parallel)

Trigger B: TDD frozen (from EEK, Layer 4) or RR frozen (from REK)
  -> API Reference Record (ARR) -> validate -> freeze

Trigger C: PMR frozen (from ODK, Layer 8) or on-demand
  -> Support Knowledge Article (SKA) -> validate -> freeze

Trigger D: Periodic or after major release
  -> Documentation Health Review (DHR) -> validate -> freeze
  (requires existing frozen UDRs, ARRs, SKAs)
```

## Boundary Contracts

- **Inputs from EEK:** TDD (API contracts and interface definitions for ARR), SAD (system boundaries for ARR)
- **Inputs from REK:** Frozen RR (what was released — triggers UDR, ARR, SKA)
- **Inputs from PIK:** Frozen PRD (requirements traceability for UDR)
- **Inputs from ODK:** Frozen PMR (incident learnings for SKA)
- **Inputs from RRK:** SRP (current operational state for DHR)
- **Outputs to IEK:** DHR findings may feed into Portfolio Evolution Signals
- **Outputs to RRK:** DHR health score contributes to operational health assessment

## File Naming

| Type | Pattern |
|------|---------|
| Spec | `{type}-spec.md` |
| Template | `{type}-template.md` |
| Prompt | `{type}-prompt.md` |
| Validator | `{type}-validator.md` |

## Commit Message Style

Follow conventional commits: `docs: <description>`

## When Working on This Kit

- Read the playbook (`docs/playbook.md`) for the full process definition
- Read the governance model (`docs/governance-model.md`) for structural rules
- Check `docs/how-to-use-with-ai.md` for session setup instructions
- Use `docs/session-setup.md` for per-artifact setup checklists and pre-flight gate checks

## Building or Auditing AIEOS Kits

- `aieos-governance-foundation/docs/kit-structure-standard.md` — compliance checklist for building and auditing kits
- `aieos-governance-foundation/docs/philosophy.md` — design rationale for governance model decisions
- `aieos-governance-foundation/docs/layer-model.md` — layer model and kit registry

# aieos-documentation-knowledge-kit

Layer 13 of the AIEOS system — Documentation & Knowledge (Cross-Cutting)

This kit governs how user-facing documentation, API references, support knowledge bases, and documentation health are produced, validated, and maintained. It's a cross-cutting kit that operates across multiple layers of the AIEOS system rather than sitting in a single sequential position in the pipeline.

## What this kit governs

Documentation quality concerns arise at multiple points in the delivery lifecycle: after technical design (API contracts), after release (user docs, support articles), and periodically (health reviews). This kit provides structured governance for four distinct documentation activities:

- **User documentation** — Is every released capability documented for end users? Is the documentation accurate, audience-appropriate, and task-oriented? (triggered after release)
- **API reference documentation** — Are all public APIs fully documented with contracts, examples, and versioning? (triggered after TDD freeze or after release)
- **Support knowledge articles** — Are troubleshooting guides and FAQs actionable, scoped, and traceable to source artifacts? (triggered after release, after incidents, or on-demand)
- **Documentation health reviews** — Is the documentation corpus current, complete, and accurate? Are deprecated docs identified? (triggered periodically or after major releases)

## Artifact types

This kit produces four governed artifact types:

| Artifact | ID Prefix | Purpose |
|----------|-----------|---------|
| User Documentation Record (UDR) | UDR-{PROJECT}-{NNN} | Governs end-user documentation for released capabilities |
| API Reference Record (ARR) | ARR-{PROJECT}-{NNN} | Governs structured API documentation — endpoints, contracts, auth, errors |
| Support Knowledge Article (SKA) | SKA-{PROJECT}-{NNN} | Governs support knowledge base articles — troubleshooting, FAQs, known issues |
| Documentation Health Review (DHR) | DHR-{PROJECT}-{NNN} | Periodic audit of documentation currency, coverage, and quality |

Each governed artifact type has exactly four governing files: spec, template, prompt, validator.

---

## Cross-cutting nature

Unlike most AIEOS kits, this kit doesn't have a single upstream/downstream position. Artifacts are triggered at different points:

| Artifact | Trigger point | Pipeline position |
|----------|---------------|-------------------|
| UDR | RR frozen (after REK release) | After Layer 5 release |
| ARR | TDD frozen (during EEK phase) or RR frozen | After Layer 4 design or Layer 5 release |
| SKA | RR frozen, PMR frozen, or on-demand | After Layer 5 release, after Layer 8 postmortem, or any time |
| DHR | Periodic or after major release | Aligned with RRK health review cadence |

The kit can be adopted independently without requiring other AIEOS kits.

## Getting started

1. Read `docs/playbook.md` for the complete process definition with trigger points
2. Read `docs/how-to-use-with-ai.md` for session setup and AI tool guidance
3. See `docs/entry-from-rek.md` for the boundary briefing for the primary entry point

## Repository structure

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
tests/
  kit-test-plan.md     # Structural integrity checks and flow scenarios
CLAUDE.md              # AI operating instructions
```

## AIEOS layer

| Layer | Kit | Status |
|-------|-----|--------|
| 2. Product Intelligence | `aieos-product-intelligence-kit` | Built |
| 4. Engineering Execution | `aieos-engineering-execution-kit` | Built |
| 5. Release & Exposure | `aieos-release-exposure-kit` | Built |
| 6. Reliability & Resilience | `aieos-reliability-resilience-kit` | Built |
| 7. Insight & Evolution | `aieos-insight-evolution-kit` | Built |
| 8. Operational Diagnostics | `aieos-operational-diagnostics-kit` | Built |
| 9. Quality Assurance | `aieos-quality-assurance-kit` | Built |
| 10. Security & Compliance | `aieos-security-compliance-kit` | Built |
| 11. Data & Configuration | `aieos-data-configuration-kit` | Built |
| 12. Platform & Infrastructure | `aieos-platform-infrastructure-kit` | Built |
| 13. Documentation & Knowledge | `aieos-documentation-knowledge-kit` | Built |

See `aieos-governance-foundation/docs/layer-model.md` for the full layer model.

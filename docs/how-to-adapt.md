# How to Adapt This Kit

This kit provides the structure, rules, and prompts for documentation and knowledge governance. Adapting it to your organization means filling in the content that is specific to your context without modifying the governance structure.

---

## What to Adapt

### Organizational Principles

**File:** `docs/principles/documentation-principles.md`

This file defines your organization's documentation quality philosophy. Adapt it to reflect:

- **Audience taxonomy**: What audiences does your organization serve? End users, developers, administrators, support staff? What are the language expectations for each?
- **Documentation standards**: What constitutes sufficient documentation for a released capability? What level of task coverage is required? What style guide does the organization follow?
- **API documentation standards**: What level of detail is required for API documentation? Are interactive examples required? What request/response format standards apply?
- **Currency policy**: How often must documentation be reviewed? What is the maximum age before documentation is considered stale?
- **Traceability requirements**: How tightly must documentation be linked to engineering artifacts? Is every claim required to trace to a specific requirement or acceptance criterion?

Replace the default policies with your organization's actual policies. Keep the structure (numbered sections, clear policy statements) but change the content to match your standards.

### Trigger Points

The playbook defines four trigger points. If your organization has different activation criteria (for example, if API documentation is required at design time rather than after TDD freeze), update the playbook trigger descriptions accordingly.

### Audience Definitions

The UDR spec references a target audience. If your organization has a defined audience taxonomy (persona definitions, skill level classifications), adapt the spec's audience clarity requirements to match your taxonomy.


## What Not to Adapt

### Specs

The specs define what makes an artifact valid. Do not soften hard gates to make artifacts easier to produce. If a hard gate is failing consistently, that usually means the artifact is incomplete, not that the gate is wrong.

If you genuinely need to add a hard gate (your organization requires something the spec does not check), add it. Do not remove existing hard gates.

### Validator Logic

Validators evaluate against specs. If a validator is producing unexpected results, check whether the spec accurately captures your requirements and adjust the spec if needed, not the validator.

### Governance Model

`docs/governance-model.md` is a synchronized copy of the canonical governance model. Do not edit it. If you believe the governance model should change, update `aieos-governance-foundation/governance-model.md` and sync all kit copies.


## Adding Artifact Types

If your organization needs additional governed artifacts (e.g., a tutorial record, a video documentation record, a glossary), follow the four-file system:

1. Write the spec first. Define the hard gates before writing anything else
2. Write the validator. This forces you to verify the spec is evaluable
3. Write the template. Structure only, no content rules
4. Write the prompt. Generation behavior, references spec and template

Register the new artifact type in the playbook, index, and CLAUDE.md.


## Tool Bindings

This kit is tool-agnostic. Templates use generic placeholders for documentation platforms, knowledge base systems, and API documentation tools.

When adopting this kit, create a bindings document:

```
docs/bindings/
  documentation-platform-mapping.md    # Maps doc platform structure to UDR format
  api-docs-tool-mapping.md             # Maps API documentation tools to ARR format
  knowledge-base-mapping.md            # Maps knowledge base systems to SKA format
```

Bindings are not governed artifacts. They have no spec, validator, or prompt. update them when your tooling changes without touching the governed files.


## Independent Adoption

This kit is designed to be adoptable independently. You do not need other AIEOS kits to use it. If you are not using the full AIEOS pipeline, provide equivalent inputs:

- For UDR: any release record or changelog describing what was released, plus requirements documentation describing what was built
- For ARR: any API contract documentation (interface definitions, endpoint specifications)
- For SKA: any incident report or support ticket data describing recurring issues
- For DHR: any existing documentation corpus to audit against current system state


## First-Time Setup Checklist

- [ ] Read `docs/playbook.md` fully before beginning
- [ ] Review and adapt `docs/principles/` to match your organizational policies
- [ ] Identify which artifacts are relevant to your initiative (not all four may be needed)
- [ ] Determine trigger points for your delivery pipeline
- [ ] Identify the documentation owner
- [ ] Confirm upstream artifacts are available (RR for UDR, TDD for ARR, etc.)

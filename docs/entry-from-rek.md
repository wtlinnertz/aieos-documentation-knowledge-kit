# Entry from Release & Exposure Kit (REK)

**You are here because:** The Release Record (RR) is frozen, and the released capabilities need to be documented for end users, API consumers, and/or support staff.

**What you must bring:**

| Artifact | Status Required | Where to Find It | Which DKK Artifact It Feeds |
|----------|----------------|-----------------|----------------------------|
| Release Record (RR) | Frozen | REK `docs/artifacts/` in the consuming project | UDR, ARR, SKA |
| Product Requirements Document (PRD) | Frozen | PIK/EEK `docs/artifacts/` in the consuming project | UDR (requirements traceability) |
| Work Decomposition Document (WDD) | Frozen | EEK `docs/artifacts/` in the consuming project | UDR (acceptance criteria) |

**Not all inputs are needed for every artifact.** This entry point can trigger multiple DKK artifacts:

- **Released user-facing capabilities?** Generate the User Documentation Record (UDR).
- **Released public API?** Generate the API Reference Record (ARR) — or update an existing one generated from TDD.
- **New capabilities that support staff need to know about?** Generate a Support Knowledge Article (SKA).

**First artifact to generate:** User Documentation Record (UDR) — triggered by RR freeze

**Where to start:** `docs/playbook.md` — Trigger A (User Documentation Record)

**What changes at this boundary:**

- You shift from releasing the system to documenting it for consumers. The focus moves from "did the release succeed?" to "can users understand and use what was released?"
- The UDR is generated from the frozen RR — the capabilities as actually released, not as planned. If the release scope was reduced from the original plan, only the actually-released capabilities are documented.
- The PRD provides requirements traceability — ensuring documentation claims map to defined requirements, not to invented features.
- The WDD provides acceptance criteria — ensuring task documentation matches how the feature actually works.

**Common mistakes at this transition:**

| Mistake | How to Avoid |
|---------|--------------|
| Generating UDR from a draft RR | The RR must be frozen. A draft RR may not reflect the actual release. |
| Documenting planned features not in the RR | Only capabilities listed in the frozen RR are in scope. Features planned but not released are not documented. |
| Writing documentation without audience identification | The UDR requires an explicit target audience statement. Documentation language must be appropriate for the stated audience. |
| Describing features without task coverage | The UDR requires task-oriented documentation — how to accomplish each user-facing task, not just feature descriptions. |
| Skipping PRD traceability | Every documentation claim must trace to a PRD requirement and WDD acceptance criterion. Undocumented features and documented-but-unbuilt features both fail the accuracy_traceability gate. |

**If you arrived here without a complete upstream artifact:**

Stop. Return to REK, complete and freeze the RR, and then re-enter DKK. The User Documentation Record cannot provide accurate capability documentation without a complete release record. A pointer to incomplete RR content does not satisfy the entry requirement.

---

*For the full entry flow, see `docs/playbook.md`.*

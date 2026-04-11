# Entry from Engineering Execution Kit (EEK)

**You are here because:** The Technical Design Document (TDD) is frozen, and the API contracts defined in it need to be documented as an API Reference Record.

**What you must bring:**

| Artifact | Status Required | Where to Find It | Which DKK Artifact It Feeds |
|----------|----------------|-----------------|----------------------------|
| Technical Design Document (TDD) | Frozen | EEK `docs/artifacts/` in the consuming project | ARR (API Reference Record) |
| System Architecture Document (SAD) | Frozen | EEK `docs/artifacts/` in the consuming project | ARR (system boundary context) |

**Not all DKK artifacts require EEK inputs.** This entry point feeds only the API Reference Record. Other artifacts are triggered by different upstream kits:

- **TDD frozen?** Generate the API Reference Record (ARR) to document API contracts.
- **RR frozen (from REK)?** Generate UDR and/or SKA — see `entry-from-rek.md`.
- **PMR frozen (from ODK)?** Generate SKA — see `entry-from-odk.md`.

**First artifact to generate:** API Reference Record (ARR) — triggered by TDD freeze

**Where to start:** `docs/playbook.md` — Trigger B (API Reference Record)

**What changes at this boundary:**

- You shift from designing the system to documenting its interfaces. The focus moves from "how does it work internally?" to "how do consumers use it?"
- The ARR is generated from the frozen TDD — the API contracts as designed, not as aspirationally planned. If the TDD API contract sections are incomplete, the ARR will have coverage gaps.
- The ARR documents every public API endpoint. Internal-only interfaces are excluded unless the TDD explicitly marks them as consumer-facing.

**Common mistakes at this transition:**

| Mistake | How to Avoid |
|---------|--------------|
| Generating ARR from a draft TDD | The TDD must be frozen. A draft TDD may change, invalidating the API documentation. |
| Documenting internal interfaces as public API | The ARR covers only public/consumer-facing API endpoints as defined in the TDD. Internal service-to-service interfaces are excluded unless explicitly scoped in. |
| Missing error response documentation | The ARR requires complete error response schemas for every endpoint. If the TDD does not define error responses, the ARR will fail the request_response_completeness gate. |
| Skipping authentication documentation | Every endpoint must have authentication requirements stated. If the TDD defines a global auth model, that must be documented in the ARR. |

**If you arrived here without a complete upstream artifact:**

Stop. Return to EEK, complete and freeze the TDD, and then re-enter DKK. The API Reference Record cannot provide meaningful contract documentation without complete API contract definitions. A pointer to incomplete TDD content does not satisfy the entry requirement.

---

*For the full entry flow, see `docs/playbook.md`.*

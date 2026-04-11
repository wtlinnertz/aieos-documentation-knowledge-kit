# Entry from Operational Diagnostics Kit (ODK)

**You are here because:** A Postmortem Report (PMR) is frozen, and the incident learnings need to be captured as a Support Knowledge Article for the support team or end users.

**What you must bring:**

| Artifact | Status Required | Where to Find It | Which DKK Artifact It Feeds |
|----------|----------------|-----------------|----------------------------|
| Postmortem Report (PMR) | Frozen | ODK `docs/artifacts/` in the consuming project | SKA (Support Knowledge Article) |

**This entry point feeds only the Support Knowledge Article.** Other DKK artifacts are triggered by different upstream kits:

- **PMR frozen?** Generate a Support Knowledge Article (SKA) to capture incident learnings.
- **RR frozen (from REK)?** Generate UDR, ARR, and/or SKA — see `entry-from-rek.md`.
- **TDD frozen (from EEK)?** Generate ARR — see `entry-from-eek.md`.

**First artifact to generate:** Support Knowledge Article (SKA) — triggered by PMR freeze

**Where to start:** `docs/playbook.md` — Trigger C (Support Knowledge Article)

**What changes at this boundary:**

- You shift from investigating the incident to documenting its learnings for support and users. The focus moves from "what went wrong and why?" to "how do users and support staff handle this situation?"
- The SKA translates technical incident findings into user-facing or support-staff-facing knowledge. The PMR's technical analysis is input material, not the output format.
- The SKA must describe the problem from the user's perspective, not the implementation perspective. "The cache invalidation race condition caused stale data" becomes "Users may see outdated information for up to 5 minutes after making changes."

**Common mistakes at this transition:**

| Mistake | How to Avoid |
|---------|--------------|
| Generating SKA from a draft PMR | The PMR must be frozen. A draft PMR may have incomplete findings. |
| Writing the problem statement in implementation terms | The SKA problem statement must be from the user's perspective. Technical root cause details belong in the background section, not the problem statement. |
| Providing resolution steps that require engineering access | Support staff must be able to execute resolution steps without engineering escalation — unless escalation IS the resolution. |
| Creating a catch-all article | Each SKA addresses exactly one problem or closely related problem set. Do not combine unrelated incident learnings into a single article. |

**If you arrived here without a complete upstream artifact:**

Stop. Return to ODK, complete and freeze the PMR, and then re-enter DKK. The Support Knowledge Article cannot provide accurate incident learnings without a complete postmortem analysis. A pointer to incomplete PMR content does not satisfy the entry requirement.

---

*For the full entry flow, see `docs/playbook.md`.*

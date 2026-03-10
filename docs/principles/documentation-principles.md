# Documentation Principles

Version: v1.0

This document defines the organization's documentation quality standards and philosophy. It is input material for artifact generation within the Documentation & Knowledge Kit — not a governed artifact. Adapt this file to reflect your organization's actual documentation policies.

---

## 1. Accuracy

- Documentation must reflect the current state of the system, not a planned or aspirational state.
- Every documentation claim must be traceable to an engineering artifact (PRD requirement, WDD acceptance criterion, TDD contract, or RR release scope).
- Documentation that describes features not present in the system, or fails to describe features that are present, is inaccurate and must be corrected.
- When the system changes, affected documentation must be updated before the change is considered complete.

## 2. Audience-Appropriate Language

- Every documentation artifact must explicitly state its target audience.
- End-user documentation must not contain implementation jargon, internal system names, or technical details that users do not need.
- Developer documentation (API references) must use precise technical language appropriate for the developer audience.
- Support documentation must use language appropriate for support staff — more technical than end-user docs, but focused on diagnosis and resolution rather than implementation.
- When in doubt about the audience's technical level, err on the side of clarity over brevity.

## 3. Task-Orientation

- User documentation must be organized around tasks users need to accomplish, not around features the system provides.
- Each documented task must include: what the user wants to achieve, the steps to accomplish it, and expected outcomes.
- Feature descriptions are supplementary — they support task documentation, they do not replace it.
- Documentation that only describes what a feature does without explaining how to use it is incomplete.

## 4. Currency

- Documentation must carry version metadata: document version, applicable product version, and last-reviewed date.
- Documentation older than 6 months without a reviewed-and-current confirmation is considered potentially stale.
- When a new release changes documented behavior, affected documentation must be updated as part of the release cycle — not deferred.
- Deprecated or removed features must have their documentation marked for retirement within one release cycle.

## 5. Traceability

- Every documentation artifact must link to its source artifacts (RR, PRD, TDD, PMR, or support ticket reference).
- Traceability enables impact analysis: when a source artifact changes, all affected documentation can be identified.
- Support knowledge articles must link to the incident report, release record, or ticket pattern that triggered their creation.
- Documentation without traceability is untethered from the system it describes and will drift over time.

## 6. Completeness

- Every released capability must have corresponding documentation (user docs, API docs, or both as applicable).
- API documentation must cover every public endpoint including error cases, not just the success path.
- Support knowledge articles must cover resolution steps completely — partial resolution guidance that requires undocumented follow-up steps is incomplete.
- Documentation health reviews must be performed periodically to identify and address coverage gaps.

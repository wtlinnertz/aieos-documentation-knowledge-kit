# Example: Notification Service Documentation

This example demonstrates the Documentation & Knowledge Kit flow using the TaskFlow notification service scenario from the AIEOS worked example (`aieos-governance-foundation/examples/taskflow-full-flow/`).

---

## Scenario

The TaskFlow notification service has completed its release through REK (Layer 5). The frozen Release Record (RR-TASKFLOW-001) documents the released capabilities:

- Email notifications for task assignments
- In-app notification center with read/unread status
- Notification preferences API (enable/disable per channel)
- Webhook integration for external notification providers

The TDD (TDD-TASKFLOW-001) defines the notification API contracts. A postmortem (PMR-TASKFLOW-001) from a notification delivery delay incident exists.

---

## DKK Artifact Flow

### Trigger A — Post-Release Documentation

**UDR-TASKFLOW-001:** User Documentation Record covering all four released capabilities. Documents how end users configure notifications, view notification history, and manage preferences. Traces each capability to PRD requirements and WDD acceptance criteria.

**SKA-TASKFLOW-001:** Support Knowledge Article for "Users not receiving email notifications" — the most common support question after the notification service release. Problem stated from user perspective; resolution steps executable by support staff.

### Trigger B — API Documentation

**ARR-TASKFLOW-001:** API Reference Record documenting the notification preferences API. Covers endpoints: `GET /api/v1/notifications`, `POST /api/v1/notifications/preferences`, `GET /api/v1/notifications/preferences`, `DELETE /api/v1/notifications/{id}`. Each endpoint has method, path, parameters, request/response schemas, auth requirements, and examples.

### Trigger C — Incident Learning

**SKA-TASKFLOW-002:** Support Knowledge Article for "Notification delivery delays after system update" — sourced from PMR-TASKFLOW-001. Translates the technical root cause (message queue backpressure during deployment) into user-facing guidance.

### Trigger D — Periodic Health Review

**DHR-TASKFLOW-001:** Documentation Health Review auditing all frozen documentation artifacts against the current release state. Coverage audit confirms all four capabilities are documented. Currency check confirms all documentation is within the 6-month threshold. Accuracy sampling verifies 3 claims against current system behavior. Health score: 92/100 (coverage 95, currency 100, accuracy 80).

---

## Key Validation Points

| Artifact | Gate to Watch | Why |
|----------|--------------|-----|
| UDR | capability_coverage | All 4 RR capabilities must have documentation sections |
| UDR | task_completeness | Each capability needs tasks with steps, not just descriptions |
| ARR | contract_fidelity | All 4 API endpoints from TDD must be documented |
| ARR | example_coverage | Each endpoint needs at least one request/response example |
| SKA-001 | problem_statement_clear | Problem must be from user perspective, not "SMTP relay timeout" |
| SKA-002 | resolution_actionable | Support staff must be able to help users without engineering escalation |
| DHR | health_score_declared | Score methodology must include coverage, currency, accuracy dimensions |

---

## Running This Example

1. Start with the frozen RR-TASKFLOW-001 from the REK worked example
2. Generate UDR-TASKFLOW-001 following `docs/playbook.md` Trigger A
3. Generate ARR-TASKFLOW-001 following `docs/playbook.md` Trigger B (using frozen TDD)
4. Generate SKA-TASKFLOW-001 following `docs/playbook.md` Trigger A (post-release)
5. Generate SKA-TASKFLOW-002 following `docs/playbook.md` Trigger C (post-incident)
6. After all documentation is frozen, generate DHR-TASKFLOW-001 following `docs/playbook.md` Trigger D
7. Validate each artifact in a separate session using the corresponding validator

Each artifact must pass all hard gates before freeze.

# Shared Linear Comment Schema
Last Updated: 2026-02-16 13:15 CET

Use this schema for all orchestrator/worker comments in Linear to keep comments machine-parseable.

## Required Wrapper
- Include this marker line before any schema payload:
  - `<!-- AGENT_EVENT_V1 -->`
- Include one fenced YAML block after marker.

## Packet Types
- Orchestrator task packet comments:
  - `event: task_packet`
  - `packet_type`: `DEV_TASK` | `TEST_TASK` | `REVIEW_TASK`
- Worker handoff/update comments:
  - `event`: `handoff` | `not_ready` | `blocked` | `done`

## Required YAML Fields
- `tracking_mode`
- `task_identifier`
- `issue_id`
- `role`
- `event`
- `branch`
- `head_commit`
- `checks`
- `decision`
- `packet_version`

## Example (Developer Handoff)
````markdown
<!-- AGENT_EVENT_V1 -->
```yaml
tracking_mode: linear
task_identifier: UOW-022
issue_id: PAY-22
role: backend-developer
event: handoff
handoff_to: backend-tester
branch: codex/uow-022-webhook-idempotency
head_commit: abc1234
checks:
  - "pytest -q: pass"
  - "ruff check: pass"
decision: ready_for_testing
packet_version: 3
```
````

## Parsing Rule
- If multiple schema comments exist, consume the newest comment containing `AGENT_EVENT_V1`.

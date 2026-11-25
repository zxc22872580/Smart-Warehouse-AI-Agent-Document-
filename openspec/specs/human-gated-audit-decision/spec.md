# Human-Gated Audit and Decision Specification

## Purpose

Define finite recommendation dispositions, human confirmation before database writes, and append-only audit logging.

## Requirements

### Requirement: Confirmation-Before-Write Gate
`SmartWarehouseAgent.analyze()` MUST NOT write document records to the `documents` table; persistence SHALL occur only when `confirm_and_write()` is called with a non-empty `actor`.

#### Scenario: Clean receipt analyzed then confirmed by operator
- **GIVEN** a valid receipt fixture `TEST-001` with sufficient context and no rule violations
- **WHEN** `SmartWarehouseAgent.analyze()` completes
- **THEN** status is `PASS_RECOMMENDED`, `find_document("TEST-001")` remains empty, and 1 `ANALYZE` audit event is recorded
- **WHEN** `confirm_and_write(result, "tester")` is subsequently called
- **THEN** the document row is persisted and a `HUMAN_CONFIRMED_WRITE` event is appended (2 total audit events for the `trace_id`)

### Requirement: Confidence and Finding Escalation Gate
When any finding is present or minimum evidence confidence is below `0.75`, `SmartWarehouseAgent.analyze()` MUST set `human_required = True` and MUST NOT return `PASS_RECOMMENDED`.

#### Scenario: Low evidence confidence or anomaly finding
- **GIVEN** an analyzed document triggers at least one finding or has `confidence < 0.75`
- **WHEN** the decision status is computed
- **THEN** `human_required` is `True` and status is `REQUEST_CORRECTION` (if critical fields are missing) or `HUMAN_REVIEW_REQUIRED`

# Inventory Analytics and Domain Rules Specification

## Purpose

Define deterministic inventory reconciliation, exact duplicate checking, and hard warehouse validation rules separating confirmed facts from unimplemented statistical heuristics.

## Requirements

### Requirement: Exact Duplicate Detection and Write Blocking
The system SHALL detect exact duplicate `document_no` entries against SQLite `documents` history and MUST block duplicate persistence at the repository layer.

#### Scenario: Second submission of an already confirmed document
- **GIVEN** document `TEST-001` has already been confirmed and written to SQLite
- **WHEN** a second document with `DOCUMENT_NO: TEST-001` is analyzed
- **THEN** `analyze_document()` emits finding `DUPLICATE_DOCUMENT` and status becomes `HUMAN_REVIEW_REQUIRED`
- **AND** calling `confirm_and_write()` on the duplicate raises `ValueError` matching `DUPLICATE_DOCUMENT_WRITE_BLOCKED`

### Requirement: Outbound Available-Stock Verification
For `ISSUE` intent documents, the analytics module MUST compare requested item quantities against `on_hand - reserved` in the target warehouse inventory and flag insufficient stock.

#### Scenario: Outbound quantity exceeds available stock
- **GIVEN** `WH-A` inventory has `SKU-001` with available stock below `95`
- **WHEN** an outbound query (`出庫檢查`) requests `95 | PCS` of `SKU-001`
- **THEN** `analyze_document()` flags `INSUFFICIENT_STOCK`
- **AND** `SmartWarehouseAgent.analyze()` sets `status = HUMAN_REVIEW_REQUIRED`

### Requirement: Deterministic Required Fields and Item Rules
`evaluate_rules()` MUST check required header fields (`document_no`, `document_date`, `warehouse`, `pallet_type`), non-empty line items, positive quantities, allowed units (`PCS`, `BOX`, `EA`, `件`, `箱`), and allowed pallet types.

#### Scenario: Critical header fields and items missing
- **GIVEN** a document containing only `PALLET_TYPE: WOOD`
- **WHEN** `SmartWarehouseAgent.analyze()` evaluates rules
- **THEN** findings include `MISSING_DOCUMENT_NO`, `MISSING_DATE`, `MISSING_WAREHOUSE`, and `NO_ITEMS`
- **AND** the returned status is `REQUEST_CORRECTION`

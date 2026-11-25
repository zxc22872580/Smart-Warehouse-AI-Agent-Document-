# Document Intake and OCR Specification

## Purpose

Define file validation, traceability initialization, OCR adapter execution, and typed document schema parsing for warehouse receiving, issuing, and cycle-count documents.

## Requirements

### Requirement: Traceable File Intake and Empty-File Fail-Safe
The system SHALL compute a SHA-256 `source_hash` and assign a unique UUID `trace_id` for every uploaded file, and MUST fail safely when the input byte stream is empty.

#### Scenario: Empty file submitted for analysis
- **GIVEN** an operator submits an empty byte payload (`b""`) with filename `empty.pdf`
- **WHEN** `SmartWarehouseAgent.analyze()` validates the input
- **THEN** the system returns status `FAILED` with error `EMPTY_FILE` and `human_required = True`
- **AND** appends an `ANALYZE` event to the SQLite `audit_log` table

### Requirement: Explicit OCR Dependency Failure
`AutoOCRProvider` MUST fail explicitly with a descriptive error when an image payload requires Tesseract and the binary or `pytesseract` dependency is unavailable, rather than returning fabricated text.

#### Scenario: Raw image bytes without Tesseract installed
- **GIVEN** `AutoOCRProvider` receives non-PDF image bytes (`scan.png`) in an environment without Tesseract
- **WHEN** `SmartWarehouseAgent.analyze()` invokes OCR extraction
- **THEN** the system catches the dependency error and returns status `FAILED`
- **AND** the error message contains `TESSERACT` with `human_required = True`

### Requirement: Line-Level Evidence Linking During Schema Parsing
The document parser SHALL extract `document_no`, `document_date`, `warehouse`, `pallet_type`, and line `items` (`sku`, `name`, `quantity`, `unit`) into typed `Document` structures linked to line-level `evidence_ids`.

#### Scenario: Synthetic UTF-8 warehouse receipt parsed with evidence
- **GIVEN** a UTF-8 receipt fixture containing `DOCUMENT_NO`, `DATE`, `WAREHOUSE`, `PALLET_TYPE`, and `ITEM` lines
- **WHEN** `SyntheticOCRProvider` and `parse_document()` process the payload
- **THEN** each extracted field and item references corresponding line-level `evidence_ids`
- **AND** `confidence` is computed as the minimum confidence across collected `OCREvidence` spans

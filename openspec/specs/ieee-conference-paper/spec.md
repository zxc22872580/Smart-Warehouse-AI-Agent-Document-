# IEEE Conference Paper Specification

## Purpose

Define structural, formatting, diagramming, and evidence-honesty requirements for the IEEEtran two-column conference manuscript maintained for Overleaf and GitHub synchronization.

## Requirements

### Requirement: Overleaf-Ready IEEEtran Manuscript Package
The `overleaf/` directory MUST contain `smart_warehouse_ai_agent.tex` and `IEEEtran.cls` configured as a self-contained `\documentclass[conference]{IEEEtran}` project that compiles cleanly without external missing assets.

#### Scenario: Overleaf import or local pdflatex compilation
- **GIVEN** the `overleaf/` directory containing `smart_warehouse_ai_agent.tex` and `IEEEtran.cls`
- **WHEN** compiled with `pdflatex` on Overleaf or locally
- **THEN** all sections, tables, citations, and vector TikZ figures render without undefined references or text overflowing column boundaries

### Requirement: Strict Separation of Observed MVP Verification and Planned Benchmarks
The manuscript SHALL explicitly separate observed MVP engineering checks (Table II) from unexecuted benchmark experiments (Table III), preserving `Not Run` / `TODO` markers rather than fabricating empirical metrics.

#### Scenario: Reporting benchmark status in Section IV and Table III
- **GIVEN** formal B0, B1, and B2 comparative experiments have not been executed
- **WHEN** Section IV-B and Table III are inspected
- **THEN** all comparative empirical values remain marked `TODO` / `Not Run`
- **AND** Table II cites only verified checks from `tests/test_mvp.py` and project audits

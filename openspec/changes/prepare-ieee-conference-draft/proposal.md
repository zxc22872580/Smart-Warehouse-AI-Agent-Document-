# Proposal: Prepare IEEE Conference Draft and OpenSpec GitHub Workspace

## Why

The repository contains the Smart Warehouse AI Agent MVP (`app.py`, `agent/`, `ocr/`, `analytics/`, `domain/`, `database/`, `tests/test_mvp.py`) and architecture/audit documentation (`architecture.md`, `flowchart.md`, `DESIGN.md`, `proposal_audit.md`), while the IEEEtran conference draft (`smart_warehouse_ai_agent.tex`) and OpenSpec specifications (`openspec/`, `.agent/`) are not yet integrated into version control. In addition, the existing `.tex` draft has table text overflow in Tables I and II, a placeholder TODO for architecture/flowchart figures, and an unstandardized NIST AI 600-1 bibliography entry.

## What Changes

- Add an Overleaf-ready `overleaf/` workspace containing `IEEEtran.cls`, `smart_warehouse_ai_agent.tex`, and `overleaf/README.md`.
- Render the eight-module system architecture (`architecture.md`) and execution/exception flowchart (`flowchart.md`) as native vector TikZ figures inside `smart_warehouse_ai_agent.tex`.
- Fix Table I and Table II column wrapping (`\allowbreak` on long identifiers) so text stays strictly within IEEEtran column boundaries.
- Standardize `\bibitem{b14}` (NIST AI 600-1) with verified official NIST authors while preserving honest `Not Run` / `TODO` markers for unexecuted benchmarks and pending author metadata.
- Establish `openspec/` baseline specs (`config.yaml`, `specs/*`) and `.agent/` workflows/skills plus secret-free MCP configuration documentation (`docs/mcp_setup.md`, `.mcp.json.example`).

## Impact

- Affected directories: `overleaf/`, `openspec/`, `.agent/`, `docs/mcp_setup.md`, `.mcp.json.example`, `README.md`.
- Python MVP runtime behavior is unchanged; all six tests in `tests/test_mvp.py` continue to pass.

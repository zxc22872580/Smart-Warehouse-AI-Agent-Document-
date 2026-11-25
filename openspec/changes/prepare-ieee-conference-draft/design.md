# Design: Overleaf LaTeX Package & OpenSpec Alignment

## Context

`smart_warehouse_ai_agent.tex` must compile cleanly on Overleaf (Standard `pdflatex` with `IEEEtran.cls`) without external build tools (`mmdc`, Inkscape, or Python plotting dependencies). Meanwhile, `openspec/` must formalize the implemented MVP contracts separately from planned target capabilities.

## Decisions

1. **Native TikZ Figures in `smart_warehouse_ai_agent.tex`**:
   - Draw Fig. 1 (Eight-Module Architecture) and Fig. 2 (Execution & Exception Flowchart) directly in LaTeX using `tikz` (`arrows.meta`, `positioning`, `fit`, `shapes.geometric`), avoiding missing external raster assets on Overleaf.
2. **Table Column Overflow Remediation**:
   - Observed PDF inspection showed `DUPLICATE_DOCUMENT_WRITE_BLOCKED` overflowing Table II into the adjacent column and tight borders in Table I. Add `\_\allowbreak` and `p{...}` width adjustments with `\raggedright` so all identifiers wrap cleanly inside cell boundaries.
3. **Self-Contained `overleaf/` Subdirectory**:
   - Place `smart_warehouse_ai_agent.tex`, `IEEEtran.cls`, and `README.md` under `overleaf/` so Overleaf GitHub Sync or ZIP upload can target `overleaf/` directly without mixing Python source files into the Overleaf project root.
4. **OpenSpec + Antigravity + MCP Separation**:
   - Store specifications in `openspec/`, Antigravity skills/workflows in `.agent/`, and a secret-free `.mcp.json.example` + `docs/mcp_setup.md` so credentials are never committed to GitHub.

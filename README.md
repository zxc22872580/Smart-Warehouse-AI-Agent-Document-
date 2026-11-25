# Smart Warehouse AI Agent — IEEE Conference Paper & OpenSpec Workspace

IEEEtran two-column conference paper draft, OpenSpec specification workspace, and MCP configuration guide for **Smart Warehouse AI Agent: Document Understanding and Inventory Anomaly Decision Agent**.

- **Main Project Repository:** https://github.com/john19991225-commits/-
- **Main Manuscript:** [`smart_warehouse_ai_agent.tex`](smart_warehouse_ai_agent.tex)
- **LaTeX Class File:** [`IEEEtran.cls`](IEEEtran.cls)

## Directory Layout

- `smart_warehouse_ai_agent.tex` — IEEE conference paper draft (with native vector TikZ diagrams for Fig. 1 System Architecture and Fig. 2 Execution Flowchart, fixed table wrapping, and verified NIST AI 600-1 citation)
- `IEEEtran.cls` — Required IEEEtran document class
- `openspec/` — OpenSpec configuration (`config.yaml`), baseline specs (`specs/`), and change tracking (`changes/`)
- `.agent/` — Antigravity OpenSpec skills and slash-command workflows (`/opsx:propose`, `/opsx:apply`, `/opsx:archive`, `/opsx:explore`)
- `.mcp.json.example` & [`docs/mcp_setup.md`](docs/mcp_setup.md) — Secret-free MCP server configuration template and setup guide

## OpenSpec Validation

```powershell
cmd /c "openspec list --specs"
cmd /c "openspec validate --all --strict"
```

## Compile on Overleaf or Locally (Requires TeX Live / MiKTeX)

Upload `smart_warehouse_ai_agent.tex` and `IEEEtran.cls` to Overleaf (compiler: `pdfLaTeX`), or compile locally:

```powershell
pdflatex smart_warehouse_ai_agent.tex
pdflatex smart_warehouse_ai_agent.tex
```

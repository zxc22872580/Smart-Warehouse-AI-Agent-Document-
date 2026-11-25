---
name: mcp-overleaf-github
description: >-
  Runbook for configuring GitHub MCP and syncing the IEEEtran Overleaf draft
  (`smart_warehouse_ai_agent.tex`) with GitHub and Overleaf.
---

# MCP, GitHub, and Overleaf Sync Skill

## 1. Configuring MCP in Antigravity

Copy `.mcp.json.example` to `~/.gemini/config/mcp_config.json` (never commit secrets or tokens into the repository). Configure a GitHub Personal Access Token via environment variable `GITHUB_PERSONAL_ACCESS_TOKEN`.

## 2. Overleaf Synchronization Options

- **Option A (GitHub Sync in Overleaf):** Connect `https://github.com/john19991225-commits/-` in Overleaf or import the `overleaf/` directory.
- **Option B (Overleaf ZIP Upload):** Zip `smart_warehouse_ai_agent.tex` and `IEEEtran.cls` and upload via Overleaf -> *New Project* -> *Upload Project*, setting `smart_warehouse_ai_agent.tex` as the main document.
- **Compiler:** `pdfLaTeX` (standard Overleaf TeX Live).

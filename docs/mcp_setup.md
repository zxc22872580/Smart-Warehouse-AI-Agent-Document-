# MCP & OpenSpec Setup Guide

This guide explains how to connect **Model Context Protocol (MCP)** servers and **OpenSpec** for maintaining the Smart Warehouse AI Agent repository and IEEE conference draft on GitHub and Overleaf.

## 1. Antigravity MCP Configuration (`mcp_config.json`)

Copy `.mcp.json.example` to your local Antigravity global config (`~/.gemini/config/mcp_config.json`) and supply your own GitHub Personal Access Token (never commit real tokens to Git):

```json
{
  "mcpServers": {
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "<YOUR_PAT>"
      }
    }
  }
}
```

> **Note:** Node.js (with `npx`) is required for stdio MCP servers such as `@modelcontextprotocol/server-github` and the OpenSpec CLI (`@fission-ai/openspec`).

## 2. OpenSpec Validation

Install OpenSpec CLI (requires Node.js >= 20.19):

```powershell
npm install -g @fission-ai/openspec@latest
openspec list --specs
openspec validate --all --strict
```

## 3. GitHub Push & Overleaf Sync

1. Stage and push `openspec/`, `.agent/`, `overleaf/`, `docs/mcp_setup.md`, `.mcp.json.example`, and `README.md` to `https://github.com/john19991225-commits/-`.
2. In Overleaf, import from GitHub or upload `smart_warehouse_ai_agent.tex` + `IEEEtran.cls` as a ZIP package and compile with `pdfLaTeX`.

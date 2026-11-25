---
name: openspec-workflow
description: >-
  Spec-driven development workflow for Smart Warehouse AI Agent using OpenSpec
  (`openspec/config.yaml`, `openspec/specs/`, `openspec/changes/`). Activate when
  proposing, implementing, validating, or archiving feature or manuscript changes.
---

# OpenSpec Workflow Skill

Use this skill whenever modifying requirements, agent policies, or the IEEE conference manuscript in `overleaf/`.

## Core Rules

1. Preserve the strict boundary between **Implemented MVP** and **Planned Target Design**.
2. Never fabricate empirical benchmark metrics; unexecuted B0/B1/B2 benchmarks remain `Not Run` / `TODO`.
3. Every requirement in `openspec/**/spec.md` must use `### Requirement:` with RFC 2119 keywords (`MUST`/`SHALL`/`SHOULD`) and at least one `#### Scenario:` block with `GIVEN`/`WHEN`/`THEN`.

## Validation Commands

```powershell
openspec list --specs
openspec validate --all --strict
python -m compileall -q agent ocr analytics domain database tests scripts app.py
python -m unittest discover -s tests -v
```

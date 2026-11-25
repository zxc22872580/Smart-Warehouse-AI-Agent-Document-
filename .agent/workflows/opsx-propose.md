---
description: Propose a new OpenSpec change with proposal.md, design.md, delta specs, and tasks.md
---

# `/opsx:propose`

1. Read `openspec/config.yaml` and relevant `openspec/specs/*/spec.md`.
2. Create `openspec/changes/<change-id>/` with `.openspec.yaml`, `proposal.md`, `design.md`, `specs/<capability>/spec.md`, and `tasks.md`.
3. Ensure every delta spec uses `## ADDED Requirements` / `## MODIFIED Requirements`, `### Requirement:`, and `#### Scenario:` with `GIVEN`/`WHEN`/`THEN`.
4. Validate with `openspec validate --all --strict`.

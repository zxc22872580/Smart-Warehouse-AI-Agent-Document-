---
description: Apply tasks from an approved OpenSpec change and verify with tests
---

# `/opsx:apply`

1. Read `openspec/changes/<change-id>/tasks.md`, `design.md`, and `specs/`.
2. Execute unchecked tasks in order while preserving `NO_WMS_WRITE`, `NO_UNSUPPORTED_CLAIM`, and `BOUNDED_EXECUTION` invariants.
3. Mark completed tasks `[x]` in `tasks.md`.
4. Run `python -m unittest discover -s tests -v` and `openspec validate --all --strict`.

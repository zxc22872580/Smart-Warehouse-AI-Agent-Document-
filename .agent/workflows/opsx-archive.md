---
description: Archive a completed OpenSpec change and merge delta specs into openspec/specs/
---

# `/opsx:archive`

1. Verify all tasks in `openspec/changes/<change-id>/tasks.md` are checked `[x]` and tests pass.
2. Merge delta requirements into `openspec/specs/<capability>/spec.md`.
3. Move the completed change folder to `openspec/changes/archive/YYYY-MM-DD-<change-id>/` (or run `openspec archive <change-id>`).
4. Re-run `openspec validate --all --strict`.

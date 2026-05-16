---
name: file-creation-rules
description: Enforces file creation permissions and naming conventions for the RSI project. Use when creating new files, when the user asks to create files, or when working with task-related file naming.
---

# File Creation Rules

## File Creation Permission

**CRITICAL**: **ALWAYS ASK THE USER BEFORE CREATING ANY NEW FILES**

- Do NOT create files (scripts, documentation, data files, etc.) without explicit user permission
- If a file needs to be created, first ask: "Should I create [filename] to [purpose]?"
- Only create files after receiving explicit confirmation from the user
- This applies to all file types: R scripts, markdown files, data files, configuration files, etc.

## Task File Naming Convention

**IMPORTANT**: All files for the same task must use the **exact same filename** (task_name.md):

- `conversation_cursor/YYYYMM/YYYYMMDD/task_name.md`
- `to-do/YYYYMM/YYYYMMDD/task_name.md`
- `task_summary/YYYYMM/YYYYMMDD/task_name.md`

The task_name must start with a verb (e.g., "modify_solve_value_mean", "implement_feature", "refactor_pipeline")

## Example

Task "modify_solve_value_mean" created on 2026-01-05:

```
conversation_cursor/202601/20260105/modify_solve_value_mean.md
to-do/202601/20260105/modify_solve_value_mean.md
task_summary/202601/20260105/modify_solve_value_mean.md
```

All three files share the **exact same filename**: `modify_solve_value_mean.md`

## Examples

See [examples.md](examples.md) for examples.

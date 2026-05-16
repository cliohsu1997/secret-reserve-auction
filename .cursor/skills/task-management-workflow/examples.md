# Task Management Workflow Examples

## Creating Task Files

All three files use the same filename: `task_name.md`

```
conversation_cursor/202601/20260105/modify_solve_value_mean.md
to-do/202601/20260105/modify_solve_value_mean.md
task_summary/202601/20260105/modify_solve_value_mean.md
```

## File Content Focus

- **conversation_cursor**: HOW and WHY (technical decisions, design, rationale)
- **to-do**: What needs to be done (UNCOMPLETED tasks only)
- **task_summary**: What has been done (completed work, findings, results)

## Update Commands

- **"update"**: Updates the three task files
- **"update all"**: Updates task files + `structure/latest.md` + `progress/latest.md`

## Testing

When user says "test", clarify:
- Run existing tests from `tests/` folder?
- Write new test scripts?
- Both?

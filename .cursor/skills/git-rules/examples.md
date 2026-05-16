# Git Commit Rules Examples

## Commit Message Format

```bash
# Short commit
Add error handling to solve_value_mean

# With task reference
Update solve_value_mean (see task_summary/202601/20260105/modify_solve_value_mean.md)
```

## Multiple Changes

Commit each change separately:

```bash
git commit -m "Modify solve_value_mean algorithm"
git commit -m "Add error handling"
git commit -m "Update documentation"
```

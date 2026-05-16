---
name: git-rules
description: Git workflow rules for the RSI project. Use when working with git commands, committing changes, or checking repository status.
---

# Git Workflow Rules

## Read-Only Commands (No Authorization Required)

The following git commands can be run WITHOUT user authorization:

- `git status` - Check working tree status
- `git diff` - View changes
- `git log` - View commit history
- `git branch` - List branches
- `git remote -v` - View remotes

## Write Commands (Require Authorization)

The following git commands REQUIRE user authorization before running:

- `git add` - Stage files
- `git commit` - Commit changes
- `git push` - Push to remote
- `git pull` - Pull from remote
- `git checkout` - Switch branches
- `git merge` - Merge branches
- `git reset` - Reset changes

## Commit Guidelines

When asked to commit changes:

- ✓ Commit each subtask individually
- ✓ Each file or logical group of related changes should be committed separately
- ✓ Do NOT combine unrelated changes into a single commit
- ✓ Always ask before committing

## Commit Message Format

- ✓ Commit message starts with a verb (e.g., "Add feature", "Fix bug", "Refactor module")
- ✓ Keep commit message short (1 line, ~50 characters max)
- ✓ Reference the task_summary file in commit message when applicable

Example:
```
Update solve_value_mean (see task_summary/202601/20260105/task_name.md)
```

## Remote Repositories

| Repository | Remote Name | Purpose | Stores |
|------------|-------------|---------|--------|
| **GitHub** | `origin` | Main code repository | All project files |

## Examples

See [examples.md](examples.md) for examples.

---
name: task-management-workflow
description: Structured task workflow for this repository—proposals, to-do lists, task summaries, progress tracking, update procedures. Per project-workflow.mdc, agents MUST read this SKILL.md at the start of every conversation in this workspace (full file). Also use when the user mentions update, task, proposal, to-do, or task summary.
---

# Task Management Workflow

## Workflow Structure

This repository uses a structured workflow to track tasks systematically with three synchronized files per task.

## File Locations

All files for the same task must use the **exact same filename** (task_name.md):

- `conversation_cursor/YYYYMM/YYYYMMDD/task_name.md` - Technical proposals and design decisions
- `to-do/YYYYMM/YYYYMMDD/task_name.md` - Checklists and actionable steps
- `task_summary/YYYYMM/YYYYMMDD/task_name.md` - Task objectives, deliverables, and progress

**Task naming**: task_name must start with a verb (e.g., "modify_solve_value_mean", "implement_feature", "refactor_pipeline")

## Reading Project Context

Follow **`.cursor/rules/project-workflow.mdc`** for the full read order (this SKILL is step 1 there). Before creating task files, also read:

1. **structure/latest.md** — Current project structure and file descriptions
2. **progress/latest.md** — Active tasks and their status
3. **task_summary/YYYYMM/YYYYMMDD/[most_recent].md** — Most recent task summary

**README.md** — Optional overview at repo root.

## Creating Task Files

### 1. Create Proposal
**Location**: `conversation_cursor/YYYYMM/YYYYMMDD/task_name.md`
- Draft technical proposal
- Document design decisions and approach
- Focus on HOW and WHY (rationale, architecture)

### 2. Create To-Do List
**Location**: `to-do/YYYYMM/YYYYMMDD/task_name.md`
- Checklist with checkboxes for each subtask
- Contains only UNCOMPLETED tasks and next actions
- Focuses on what needs to be done

### 3. Create Task Summary
**Location**: `task_summary/YYYYMM/YYYYMMDD/task_name.md`
- Task objectives and deliverables
- Records completed work, current status, findings, and results
- Related files and dependencies
- Focuses on what has been done

## Content Division (Prevent Overlap)

- **TO-DO LIST**: Only UNCOMPLETED tasks and next actions. What needs to be done.
- **TASK SUMMARY**: Completed work, current status, findings, results. What has been done.
- **PROPOSAL**: Technical decisions, design choices, implementation approach, architectural rationale. HOW and WHY.

## Update Procedures

### "update" Command
Update these three files:
- ✓ `to-do/YYYYMM/YYYYMMDD/task_name.md` - Checklist of remaining actionable steps
- ✓ `task_summary/YYYYMM/YYYYMMDD/task_name.md` - Current state and progress summary
- ✓ `conversation_cursor/YYYYMM/YYYYMMDD/task_name.md` - Technical design and implementation decisions

### "update all" Command
Update the three files above PLUS:
- ✓ `structure/latest.md` - Update if project structure or file descriptions changed
- ✓ `progress/latest.md` - Update active/completed task status

**Structure updates**: When updating `structure/latest.md`, use **high-level description only** and **structure-only** modifications (folder layout, brief purpose). Do not add low-level implementation detail or non-structural content.

## Task Completion

When a task is complete:
- ✓ `conversation_cursor` - Finalize with implementation results
- ✓ `to-do` - Mark all items complete
- ✓ `task_summary` - Final deliverables and outcomes
- ✓ `progress/latest.md` - Move to completed section
- ✓ `structure/latest.md` - Update file descriptions if needed (high-level, structure only; see ``update all'' rule)

**IMPORTANT**: Do NOT automatically create new tasks after completing a task. Wait for explicit user instruction.

## Testing Rule

When the user says "test" or requests testing:
1. **Run existing tests** - Execute test scripts from the `tests/` folder
2. **Write test scripts** - Create new test files in the `tests/` folder

Always clarify with the user which action is intended, or do both if appropriate.

## Examples

See [examples.md](examples.md) for examples.

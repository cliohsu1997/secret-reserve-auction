# Cursor Skills Directory

This directory contains project-specific skills that Cursor will automatically detect and apply when relevant tasks are submitted.

## How Skills Work

- **Skills are NOT read at the start of conversations** - this optimizes token usage
- **Skills are automatically detected** when the agent determines they're relevant to the current task
- Skills are discovered based on their `description` field in the `SKILL.md` frontmatter

## Creating a New Skill

1. Create a new directory: `.cursor/skills/your-skill-name/`
2. Create a `SKILL.md` file with YAML frontmatter:

```markdown
---
name: your-skill-name
description: Brief description of what this skill does and when to use it
---

# Your Skill Name

[Your skill content here...]
```

## Skill Structure

Each skill should be a directory containing:
- `SKILL.md` (required) - Main skill instructions
- Optional supporting files (reference.md, examples.md, scripts/, etc.)

## Best Practices

- Keep `SKILL.md` under 500 lines
- Write descriptions in third person
- Include trigger terms in descriptions so the agent knows when to apply the skill
- Use progressive disclosure - put detailed info in separate reference files

For more details, see the Cursor documentation on creating skills.

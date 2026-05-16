# Skills Created from README.md

This document summarizes all skills extracted from README.md for review.

## Created Skills

### 1. **task-management-workflow**
**Location**: `.cursor/skills/task-management-workflow/SKILL.md`

**Purpose**: Manages the structured task workflow including creating proposals, to-do lists, task summaries, progress tracking, and update procedures.

**Triggers**: Creating new tasks, updating task status, managing task files, "update", "task", "proposal", "to-do", "task summary"

**Key Content**:
- File locations and naming conventions
- Reading project context workflow
- Creating task files (proposal, to-do, summary)
- Content division rules (prevent overlap)
- Update procedures ("update" vs "update all")
- Task completion workflow
- Testing rule

---

### 2. **file-creation-rules**
**Location**: `.cursor/skills/file-creation-rules/SKILL.md`

**Purpose**: Enforces file creation permissions and naming conventions.

**Triggers**: Creating new files, when user asks to create files, task-related file naming

**Key Content**:
- Always ask before creating files
- Task file naming convention (exact same filename across three locations)
- Task name must start with a verb

---

### 3. **r-package-development**
**Location**: `.cursor/skills/r-package-development/SKILL.md`

**Purpose**: Provides R package development setup and execution guidelines.

**Triggers**: Running R scripts, setting up R environment, using devtools, R package structure

**Key Content**:
- R environment paths (Windows)
- Running scripts in RStudio (devtools::load_all)
- Command line execution
- Package structure files (RSI.Rproj, DESCRIPTION, NAMESPACE)

---

### 4. **hpc4-execution**
**Location**: `.cursor/skills/hpc4-execution/SKILL.md`

**Purpose**: Manages HPC4 cluster execution including conda environment, package installation, AWS configuration, and SLURM job submission.

**Triggers**: Working on HPC4, submitting jobs, configuring conda environments, AWS on cluster

**Key Content**:
- Conda environment setup (rsi_clio)
- RSI package installation on HPC4
- AWS configuration on HPC4 (profile: clio)
- SLURM job submission with sbatch
- Log file monitoring

---

### 5. **aws-s3-data-management**
**Location**: `.cursor/skills/aws-s3-data-management/SKILL.md`

**Purpose**: Handles AWS S3 data management including S3 access, credentials, loading/writing files.

**Triggers**: Working with S3, loading data from S3, writing data to S3, configuring AWS credentials

**Key Content**:
- Reference to comprehensive guide (doc/aws_data_access_guide.md)
- Credentials requirements
- Common operations (load/write RDS, CSV)

---

### 6. **coding-style**
**Location**: `.cursor/skills/coding-style/SKILL.md`

**Purpose**: Enforces R and C++ code formatting standards.

**Triggers**: Writing R code, C++ code, formatting functions, coding style questions

**Key Content**:
- Break line for each argument in functions and calls
- Break line after arithmetic operations
- If statements: condition on new line within parentheses
- C++ error handling: use `std::numeric_limits<double>::quiet_NaN()`
- Keep comments minimal

---

### 7. **python**
**Location**: `.cursor/skills/python/SKILL.md`

**Purpose**: Python code standards and project layout (`python/`, `virtual env`, `code`). Poetry run via virtual env.

**Triggers**: Writing Python, running scripts via Poetry, `python/`, `virtual env`, `extract_intro_conclusion`

**Key Content**:
- Folder layout: `python/virtual env/`, `python/code/`
- Code style (R-like: one arg per line, etc.)
- Run: `poetry run python code/<script>.py` from `python/`

---

### 8. **git-commit-rules**
**Location**: `.cursor/skills/git-commit-rules/SKILL.md`

**Purpose**: Enforces git commit message format and structure.

**Triggers**: Committing changes, creating commit messages, user asks to commit

**Key Content**:
- Commit each subtask individually
- Commit message format (verb start, ~50 chars max)
- Reference task_summary in commit message
- Remote repository information

---

## Review Checklist

For each skill, verify:
- [ ] Description includes trigger terms
- [ ] Content is concise and actionable
- [ ] No overlap between skills
- [ ] All important information from README.md is captured
- [ ] Examples are clear and relevant

## Next Steps

1. Review each skill file
2. Test skill detection by mentioning trigger terms
3. Adjust descriptions if skills aren't being detected
4. Add more examples if needed
5. Split or merge skills if content organization needs improvement

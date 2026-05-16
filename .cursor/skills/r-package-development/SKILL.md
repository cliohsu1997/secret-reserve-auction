---
name: r-package-development
description: Provides R package development setup and execution guidelines for the RSI project. Use when running R scripts, setting up R environment, using devtools, or when working with R package structure, DESCRIPTION, NAMESPACE files.
---

# R Package Development

## R Environment

- **R Root Directory**: `C:\Program Files\R\R-4.5.3`
- **Rscript Path**: `C:\Program Files\R\R-4.5.3\bin\Rscript.exe`
- **R Executable**: `C:\Program Files\R\R-4.5.3\bin\R.exe`
- **Find it (PowerShell)**:

```powershell
where.exe Rscript.exe
Get-Command Rscript.exe | Select-Object -ExpandProperty Source
```

## Running Scripts

All scripts in `main/` are designed to be run from **RStudio** or **R console** using:

```r
devtools::load_all(".")  # Loads the RSI package
```

Scripts are typically run **interactively in RStudio**, not via command line.

## Command Line Execution

To run from command line if needed:

```powershell
& "C:\Program Files\R\R-4.5.3\bin\Rscript.exe" script_name.R
```

## Package Structure

Key files:
- **RSI.Rproj**: R project configuration
- **DESCRIPTION**: Package metadata and dependencies
- **NAMESPACE**: R package namespace and exported functions

## Examples

See [examples.md](examples.md) for examples.

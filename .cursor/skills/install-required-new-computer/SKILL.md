---
name: install-required-new-computer
description: Guides installation of R, RStudio, VS Code, Discord, AWS CLI, LaTeX (distribution + LaTeX Workshop in Cursor/VS Code), R build tools (Xcode Command Line Tools on macOS, Rtools on Windows), and Rcpp on a new Mac or Windows PC. Use when setting up a new computer, reinstalling dev tools, or when the user asks to install R, RStudio, VS Code, Discord, AWS CLI, LaTeX, or compilers for R packages.
---

# Install All Required for New Computer

Use this skill when setting up a new machine (macOS or Windows) with everything needed for R development, C++ in R, and common tools. Install **R build tools first** (required for compiling R packages and C++ code in R). After R is installed, install the **Rcpp** package from R.

## What to install by platform

| Item | macOS | Windows |
|------|--------|---------|
| **R build tools** | Xcode Command Line Tools (`xcode-select --install`) | Rtools (match R version; from CRAN) |
| **R** | CRAN .pkg (ARM64 or Intel from cran.r-project.org/bin/macosx/) | CRAN Windows .exe (cran.r-project.org/bin/windows/base/) |
| **RStudio** | RStudio Desktop for macOS (.dmg) | RStudio Desktop for Windows (.exe) |
| **VS Code** | VS Code for macOS (.dmg) | VS Code for Windows (.exe) |
| **Discord** | Discord for macOS | Discord for Windows |
| **AWS CLI** | AWSCLIV2.pkg or `brew install awscli` | AWSCLIV2.msi or `winget install Amazon.AWSCLI` |
| **LaTeX** | MacTeX: https://tug.org/mactex/ or BasicTeX: https://tug.org/mactex/morepackages.html (smaller) or `brew install --cask mactex` + **LaTeX Workshop** extension | MiKTeX: https://miktex.org/ or TeX Live: https://tug.org/texlive/ + **LaTeX Workshop** extension |
| **Rcpp** | From R: `install.packages("Rcpp", repos = "https://cloud.r-project.org")` | Same (from R, after Rtools is installed) |

Install the **LaTeX Workshop** extension in Cursor/VS Code on both platforms (Extensions → search “LaTeX Workshop”). All other items above are **per platform** as in the table.

---

# macOS

---

## 1. Xcode Command Line Tools (R build tools)

**What they are:** Compilers and build tools (clang, make, etc.) used to compile R packages and C++/Fortran code in R. Often called "R build tools" or "development tools for R."

**Install:**

```bash
xcode-select --install
```

In the dialog, click **Install** and accept the license. Wait for it to finish.

**Verify:**

```bash
xcode-select -p
clang --version
pkgutil --pkg-info=com.apple.pkg.CLTools_Executables
```

**Update later:** `softwareupdate --list` then `sudo softwareupdate --install "Command Line Tools for Xcode-X.X-X.X"` (use the exact label from the list).

---

## 2. R

**Download:** https://cran.r-project.org/bin/macosx/

- **Apple Silicon (M1/M2/M3/M4):** use the **ARM64** build.
- **Intel Mac:** use the **x86_64** (Intel) build. Do **not** install the ARM64 build on Intel.

Install the **.pkg** and follow the installer.

**Verify:** `R --version`

---

## 3. RStudio

**Download:** https://posit.co/download/rstudio-desktop/

Download **RStudio Desktop** for macOS and install the .dmg (drag to Applications). Install **after** R.

**Verify:** Open RStudio; it should detect R automatically.

---

## 4. VS Code

**Download:** https://code.visualstudio.com/

Download the **macOS** version (**.dmg** or **.zip**). Install to Applications.

**Optional – shell command:** In VS Code, open Command Palette (Cmd+Shift+P), run **Shell Command: Install 'code' command in PATH**.

**Verify:** Open Visual Studio Code from Applications.

---

## 5. Discord

**Download:** https://discord.com/download

Download the **macOS** version and install (drag to Applications).

**Verify:** Open Discord from Applications.

---

## 6. AWS CLI

**Install (macOS):**

Official standalone installer (recommended):

```bash
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /
rm AWSCLIV2.pkg
```

Or with Homebrew (if installed): `brew install awscli`

**Verify:**

```bash
aws --version
aws configure
```

Configure with your AWS Access Key ID, Secret Access Key, and default region (e.g. `ap-northeast-1`).

**Configure AWS (IAM access keys):**

1. **Create a new access key** (if you don’t have the secret for an existing key — AWS only shows the secret once at creation): IAM → **Users** → your user → **Security credentials** → **Access keys** → **Create access key** → choose “Command Line Interface (CLI)” → copy both **Access key ID** and **Secret access key** and store them safely.
2. **Configure the CLI** with the new key:
   ```bash
   aws configure --profile clio
   ```
   Enter the Access key ID, Secret access key, and region (e.g. `ap-northeast-1`).
3. **Test:** `aws s3 ls s3://rsi-khsu/ --profile clio`
4. **Then** deactivate or delete the old key in IAM (Access keys → Actions → Deactivate or Delete) so you don’t leave unused keys active.

**RSI project:** Use profile `clio`, region `ap-northeast-1`, bucket `rsi-khsu`. Scripts use `aws.signature::locate_credentials(profile = "clio", region = "ap-northeast-1")` and bucket `bucket_name <- "rsi-khsu"`.

---

## 7. LaTeX (compile in Cursor / VS Code)

**Goal:** Edit and compile LaTeX (e.g. project drafts) in Cursor or VS Code.

**LaTeX distribution (required to build PDFs):**

- **macOS:** Install **MacTeX** from https://tug.org/mactex/ (large download), or `brew install --cask mactex`. Adds `pdflatex`, `bibtex`, etc. to PATH (you may need to restart the terminal or add `/Library/TeX/texbin` to PATH).  
  **Note:** **BasicTeX** (https://tug.org/mactex/morepackages.html) is a smaller (~100 MB) alternative; it works for most documents. If a package is missing, install it with `sudo tlmgr install <package-name>`.
- **Windows:** Install **MiKTeX** (https://miktex.org/) or **TeX Live** (https://tug.org/texlive/).

**Extension in Cursor / VS Code:**

1. Open **Extensions** (Ctrl+Shift+X / Cmd+Shift+X).
2. Search for **LaTeX Workshop** (by James Yu).
3. Click **Install**.

Then open a `.tex` file; you can build with the default shortcut (e.g. Cmd+Option+B / Ctrl+Alt+B) or from the Command Palette: **LaTeX Workshop: Build LaTeX project**. See the project’s [latex-compilation](.cursor/skills/latex-compilation/SKILL.md) skill for the full pdflatex → bibtex → pdflatex cycle and auxiliary file cleanup.

**Verify:** Open a `.tex` file, run **LaTeX Workshop: Build LaTeX project**; a PDF should be produced (or errors shown in the output).

---

## Order of installation (recommended)

1. **Xcode Command Line Tools** (first; needed for R packages with C/C++)
2. **R**
3. **RStudio**
4. **VS Code**
5. **Discord**
6. **AWS CLI**
7. **LaTeX** (distribution + LaTeX Workshop extension in Cursor/VS Code)
8. **Rcpp package** (from R; see below)

---

## macOS quick checklist

- [ ] Xcode Command Line Tools (`xcode-select --install`)
- [ ] R (CRAN .pkg; choose ARM64 or Intel)
- [ ] RStudio (Posit download)
- [ ] VS Code (code.visualstudio.com)
- [ ] Discord (discord.com/download)
- [ ] AWS CLI (pkg or Homebrew)
- [ ] LaTeX (MacTeX or brew install --cask mactex + LaTeX Workshop extension)
- [ ] Rcpp package (from R; see below)

After all are installed, R packages that use C++ will compile using the Command Line Tools; no full Xcode app required.

---

# Windows

Install **Rtools first** (needed for compiling R packages and C++ code in R). Then R, RStudio, and the rest.

---

## 1. Rtools (R build tools on Windows)

**What they are:** Compilers and build tools (gcc, make, etc.) for building R packages with C/C++/Fortran on Windows. The Windows equivalent of Xcode Command Line Tools.

**Download:** https://cran.r-project.org/bin/windows/Rtools/

Use the **Rtools version that matches your R version** (e.g. Rtools43 for R 4.3.x, Rtools44 for R 4.4.x). Download the installer (e.g. **rtools43.exe** or **rtools44.exe**) and run it. During setup, check the option to **add Rtools to PATH** if offered.

**Verify:** Open a **new** Command Prompt or PowerShell and run:

```cmd
where gcc
R --version
```

---

## 2. R (Windows)

**Download:** https://cran.r-project.org/bin/windows/base/

Download the **latest R for Windows** installer (e.g. **R-4.x.x-win.exe**). Run it and complete the setup.

**Verify:** `R --version` in Command Prompt, or open R GUI.

---

## 3. RStudio (Windows)

**Download:** https://posit.co/download/rstudio-desktop/

Download **RStudio Desktop** for Windows (.exe). Install after R. RStudio will detect R automatically.

---

## 4. VS Code (Windows)

**Download:** https://code.visualstudio.com/

Download the **Windows** installer (.exe or .zip). Install. Optionally add **code** to PATH during setup or via Command Palette: **Shell Command: Install 'code' command in PATH**.

---

## 5. Discord (Windows)

**Download:** https://discord.com/download

Download the **Windows** version and run the installer.

---

## 6. AWS CLI (Windows)

**Download/install:** https://awscli.amazonaws.com/AWSCLIV2.msi

Run the MSI installer. Or use **winget** (if available): `winget install Amazon.AWSCLI`

**Verify:** Open a **new** Command Prompt and run:

```cmd
aws --version
aws configure
```

**Configure AWS (IAM access keys):** Same as macOS: create a new access key in IAM if needed (Security credentials → Access keys → Create access key), then run `aws configure --profile clio`, test with `aws s3 ls s3://rsi-khsu/ --profile clio`, then deactivate the old key in IAM.

---

## 7. LaTeX (Windows) — compile in Cursor / VS Code

**LaTeX distribution:** Install **MiKTeX** (https://miktex.org/) or **TeX Live** (https://tug.org/texlive/). **Extension:** In Cursor/VS Code, install **LaTeX Workshop** (James Yu). Then you can build LaTeX from the editor. See [latex-compilation](.cursor/skills/latex-compilation/SKILL.md) for the full build cycle.

---

## Windows order of installation (recommended)

1. **Rtools** (match your R version)
2. **R**
3. **RStudio**
4. **VS Code**
5. **Discord**
6. **AWS CLI**
7. **LaTeX** (MiKTeX or TeX Live + LaTeX Workshop extension)
8. **Rcpp package** (from R; see below)

## Windows quick checklist

- [ ] Rtools (cran.r-project.org/bin/windows/Rtools/; match R version)
- [ ] R (CRAN Windows .exe)
- [ ] RStudio (Posit download)
- [ ] VS Code (code.visualstudio.com)
- [ ] Discord (discord.com/download)
- [ ] AWS CLI (AWSCLIV2.msi or winget)
- [ ] LaTeX (MiKTeX or TeX Live + LaTeX Workshop extension)
- [ ] Rcpp package (from R; see below)

---

# Install Rcpp (macOS and Windows)

**Yes, install the Rcpp package.** It provides the interface for using C++ code in R and is required by many packages (including RSI). Install it **after** R and the platform’s R build tools (Xcode Command Line Tools on macOS, Rtools on Windows) are installed.

**From R (RStudio or terminal):**

```r
install.packages("Rcpp", repos = "https://cloud.r-project.org")
```

**Verify:**

```r
library(Rcpp)
evalCpp("2 + 2")  # should return 4
```

If installation fails, confirm that R build tools are installed and (on Windows) that Rtools is on PATH and that you started R **after** installing Rtools.

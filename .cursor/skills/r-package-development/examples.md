# R Package Development Examples

## Load Package

```r
devtools::load_all(".")
```

## Run Scripts

**In RStudio (preferred):**
```r
devtools::load_all(".")
source("main/0_clean_data/0_2_3_download_and_clean_product.R")
```

**Command line:**
```powershell
& "C:\Program Files\R\R-4.4.2\bin\Rscript.exe" script_name.R
```

# AWS S3 Data Management Examples

## Setup Credentials

```r
signature <- aws.signature::locate_credentials(
  profile = "clio",
  region = "ap-northeast-1"
)
Sys.setenv(
  "AWS_ACCESS_KEY_ID" = signature$key,
  "AWS_SECRET_ACCESS_KEY" = signature$secret,
  "AWS_DEFAULT_REGION" = signature$region
)
bucket_name <- "rsi-khsu"
```

## Create Directory

```r
library(RSI)
prefix <- "output/your-name/"
create_directory_if_not_exists(bucket = bucket_name, prefix = prefix)
```

## Load RDS

```r
# Basic
df <- aws.s3::s3readRDS(
  object = "cleaned/transaction_level_product.rds",
  bucket = bucket_name
)

# Large files
df <- aws.s3::s3readRDS(
  object = "output/large_file.rds",
  bucket = bucket_name,
  multipart = TRUE
)
```

## Load CSV

```r
library(readr)
df_csv <- aws.s3::s3read_using(
  object = "input/data.csv",
  FUN = read_csv,
  bucket = bucket_name
)
```

## Write RDS

```r
aws.s3::s3saveRDS(
  my_data,
  object = paste0(prefix, "my_data.rds"),
  bucket = bucket_name,
  multipart = TRUE  # For large files
)
```

## Write CSV

```r
write.csv(data_frame, "temp.csv", row.names = FALSE)
aws.s3::put_object(
  file = "temp.csv",
  object = paste0(prefix, "data.csv"),
  bucket = bucket_name
)
unlink("temp.csv")
```

## List Bucket

```r
# List all
aws.s3::get_bucket(bucket = bucket_name)

# List with prefix
aws.s3::get_bucket(
  bucket = bucket_name,
  prefix = "cleaned/",
  delimiter = "/"
)
```

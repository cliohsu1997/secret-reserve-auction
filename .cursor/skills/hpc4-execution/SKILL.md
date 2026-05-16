---
name: hpc4-execution
description: Manages HPC4 cluster execution including conda environment setup, RSI package installation, AWS configuration, and SLURM job submission. Use when working on HPC4, submitting jobs, configuring conda environments, or setting up AWS on the cluster.
---

# HPC4 Setup & Execution

## Conda Environment

Use the `rsi_clio` conda environment.

## Installing RSI Package on HPC4

Install the RSI package in the conda environment:

```bash
bash -lc 'set -euo pipefail;
ENV="/home/khsu/.conda/envs/rsi_clio";
export PATH="$ENV/bin:$PATH";
# Verify wrappers
command -v x86_64-conda-linux-gnu-c++ && command -v x86_64-conda-linux-gnu-cc;
# Clean lock then reinstall
rm -rf "$ENV/lib/R/library/00LOCK-RSI" || true;
"$ENV/bin/R" --vanilla -s -e "Rcpp::compileAttributes()";
"$ENV/bin/R" CMD INSTALL --preclean --with-keep.source .'
```

## AWS Configuration on HPC4

**Configuration**:
- AWS Profile name: `clio`
- Conda environment: `rsi_clio`

Configure AWS credentials for S3 access:

```bash
bash -lc 'ENV="/home/khsu/.conda/envs/rsi_clio"; export PATH="$ENV/bin:$PATH"; aws configure --profile clio'
```

Enter credentials when prompted:
- AWS Access Key ID
- AWS Secret Access Key
- Default region: `ap-northeast-1`
- Default output format: `json`

Verify the configuration:
```bash
aws s3 ls s3://rsi-khsu/ --profile clio
```

## Running Shell Scripts on HPC4

Submit jobs using SLURM with `sbatch`:

```bash
bash -c 'set -euo pipefail;
LOGDIR=/home/khsu/projects/RSI/logs;
JOB_SUB=$(sbatch hpc4/script_name.sh);
echo "$JOB_SUB";
JOBID=${JOB_SUB##* };
echo "JobID: $JOBID";
PATTERN="*-${JOBID}-*.out";
echo "Waiting for log file...";
while true; do
  FILE=$(ls -1 "$LOGDIR"/${PATTERN} 2>/dev/null | head -n1 || true);
  if [ -n "${FILE:-}" ]; then echo "Log file: $FILE"; break; fi;
  squeue -j "$JOBID" | sed -n "2p" || true;
  sleep 3;
done;
echo "Tailing last 100 lines (updates)";
tail -n 100 -f "$FILE"'
```

**Replace `script_name.sh`** with your actual script name.

## Examples

See [examples.md](examples.md) for examples.

# HPC4 Execution Examples

## Install Package

```bash
bash -lc 'set -euo pipefail;
ENV="/home/khsu/.conda/envs/rsi_clio";
export PATH="$ENV/bin:$PATH";
rm -rf "$ENV/lib/R/library/00LOCK-RSI" || true;
"$ENV/bin/R" --vanilla -s -e "Rcpp::compileAttributes()";
"$ENV/bin/R" CMD INSTALL --preclean --with-keep.source .'
```
## Remove R Lock

```bash
pkill -9 R
pkill -9 Rscript
sleep 3
mv /home/khsu/.conda/envs/rsi_clio/lib/R/library/00LOCK-RSI /home/khsu/.conda/envs/rsi_clio/lib/R/library/00LOCK-RSI.old_$(date +%s) 2>/dev/null && echo "Lock moved"
```

## Configure AWS

```bash
bash -lc 'ENV="/home/khsu/.conda/envs/rsi_clio"; export PATH="$ENV/bin:$PATH"; aws configure --profile clio'
```

## Submit Job

```bash
sbatch hpc4/estimate_data/gmm/check_identification_gmm.sh
```

## Monitor Job

```bash
bash -c 'set -euo pipefail;
LOGDIR=/home/khsu/projects/RSI/logs;
JOB_SUB=$(sbatch hpc4/estimate_data/gmm/check_identification_gmm.sh);
JOBID=${JOB_SUB##* };
PATTERN="*-${JOBID}-*.out";
while true; do
  FILE=$(ls -1 "$LOGDIR"/${PATTERN} 2>/dev/null | head -n1 || true);
  if [ -n "${FILE:-}" ]; then echo "Log: $FILE"; break; fi;
  sleep 3;
done;
tail -n 100 -f "$FILE"'
```

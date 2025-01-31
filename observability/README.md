# CDE Observability Demo Setup

Run the following CDE CLI commands.

```
cde job delete \
  --name skewJob

cde resource create \
  --type files \
  --name skewAppResource

cde resource upload \
  --name skewAppResource \
  --local-path observability/skewApp.py

cde job create \
  --type spark \
  --name skewJob \
  --application-file skewApp.py \
  --mount-1-resource skewAppResource \
  --executor-memory "2g" \
  --executor-cores 2 \
  --schedule-enabled true \
  --cron-expression "*/5 * * * *" \
  --schedule-start "2025-01-30" \
  --schedule-end "2025-02-01"

cde job run \
  --name skewJob
```

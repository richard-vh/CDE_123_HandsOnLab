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

"schedule": {
"enabled": false,
"user": "jprosser",
"cronExpression": "30 */1 * * *",
"start": "2024-11-24",
"end": "2024-11-24"
}


./setup/deploy_hol.sh pauldefusco pauldefusco 10 s3a://cde-hol-25-buk-b1dd6f64/data/cde-123-hol

# Deployment & Orchestration with Airflow in CDE

## Contents

6. [Promote to higher env using API by replicating repo and redeploy](https://github.com/pdefusco/CDE_SparkConnect?tab=readme-ov-file#6-promote-to-higher-env-using-api-by-replicating-repo-and-redeploy)
7. [Build Orchestration Pipeline with Airflow]()

## Instructions

### 6. Promote to higher env using API by replicating repo and redeploy

Now that the job has succeeded, deploy it into your PRD cluster.

Create and sync the same Git repo from the PRD Cluster:

```
cde repository create \
  --name sparkAppRepoPrdUser001 \
  --branch main \
  --url https://github.com/pdefusco/CDE_123_HOL.git \
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

```
cde repository sync \
  --name sparkAppRepoPrdUser001 \
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

Then create a CDE Spark Job leveraging the CDE repository as a dependency.

```
cde job create --name cde_spark_job_prd_user001 \
  --type spark \
  --mount-1-resource sparkAppRepoPrdUser001 \
  --executor-cores 2 \
  --executor-memory "4g" \
  --application-file pyspark-app.py\
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1 \
  --arg s3a://cde-hol-buk-d2ab0f50/data/cde-123-hol
```

```
cde job run --name cde_spark_job_prd_user001 \
  --executor-cores 4 \
  --executor-memory "2g" \
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

![alt text](../../img/move-job.png)

### 7. Build Orchestration Pipeline with Airflow

Create the CDE Spark jobs. Notice these are categorized into Bronze, Silver and Gold following a Lakehouse Data Architecture.

```
cde job create --name cde_spark_job_bronze_user001 \
  --type spark \
  --arg user001 \
  --arg s3a://go01-demo/data/cde-123-hol \
  --mount-1-resource sparkAppRepoPrdUser001 \
  --python-env-resource-name Python-Env-Shared \
  --executor-cores 2 \
  --executor-memory "4g" \
  --application-file de-pipeline/spark/001_Lakehouse_Bronze.py\
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

```
cde job create --name cde_spark_job_silver_user001 \
  --type spark \
  --arg user001 \
  --mount-1-resource sparkAppRepoPrdUser001 \
  --python-env-resource-name Python-Env-Shared \
  --executor-cores 2 \
  --executor-memory "4g" \
  --application-file de-pipeline/spark/002_Lakehouse_Silver.py\
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

```
cde job create --name cde_spark_job_gold_user001 \
  --type spark \
  --arg user001 \
  --arg s3a://go01-demo/data/cde-123-hol \
  --mount-1-resource sparkAppRepoPrdUser001 \
  --python-env-resource-name Python-Env-Shared \
  --executor-cores 2 \
  --executor-memory "4g" \
  --application-file de-pipeline/spark/003_Lakehouse_Gold.py\
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

In your editor, open the Airflow DAG "004_airflow_dag_git" and edit your username variable at line 54.

![alt text](../../img/username-dag.png)

Then create the CDE Airflow job. This job will orchestrate your Lakehouse Spark jobs above.

```
cde job create --name airflow-orchestration-user001 \
  --type airflow \
  --mount-1-resource sparkAppRepoPrdUser001 \
  --dag-file de-pipeline/airflow/004_airflow_dag_git.py\
  --vcluster-endpoint https://2cbcn8vs.cde-q7kss7bw.cde-hol.vayb-xokg.cloudera.site/dex/api/v1
```

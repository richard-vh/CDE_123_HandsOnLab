# CDE 1.23 Hands On Lab

![alt text](/img/new-ref-arch.png)

## About the CDE Lab

In these Labs you will gain hands-on experience the Cloudera Data Engineering Service. You will:

1. Develop a PySpark and Iceberg Application connecting to a Spark Virtual Cluster via Spark Connect using the JupyterLab IDE.
2. Prototype your Spark Application in a dedicated CDE DEV environment.
3. Use git to back up your code and push it to a dedicated CDE PRD environment.
4. Create an Airflow Pipeline to orchestrate multiple Spark Applications.
5. Monitor your Spark Applications with CDP Observability and the CDP Data Catalog.

## About the Cloudera Data Engineering (CDE) Service

CDE is the Cloudera Data Engineering Service, a containerized managed service for Cloudera Data Platform designed for Large Scale Batch Pipelines with Spark, Airflow and Iceberg. It allows you to submit batch jobs to auto-scaling virtual clusters. As a Cloud-Native service, CDE enables you to spend more time on your applications, and less time on infrastructure.

CDE allows you to create, manage, and schedule Apache Spark jobs without the overhead of creating and maintaining Spark clusters. With CDE, you define virtual clusters with a range of CPU and memory resources, and the cluster scales up and down as needed to run your Spark workloads, helping to control your cloud costs.

## Agenda & Times

1. CDE Architecture (xx minutes)
    * Introduction to the CDE Service
      * CDP Environment
      * CDP Service
      * Virtual Cluster
      * CDE Jobs
      * CDE Resource
      * Job Run
      * CDE Sessions
      * Apache Iceberg
      * CDE User Interface
    * Summary
2. CDE Development (xx minutes)
    * Lab 1. Spark Application Development
    * Lab 2. CDE Repositories, Jobs, and Monitoring
3. CDE Deployment (xx minutes)
    * Lab 3. Promote to higher env using API by replicating repo and redeploy
    * Lab 4. Build Orchestration Pipeline with Airflow
4. CDE Observability (xx minutes)
    * Lab 5. Monitoring Jobs with Cloudera Observability and CDE
    * Lab 6. Spark Job Governance with CDP Data Catalog
5. Additional Labs (xx minutes)
    * Lab x. Time dependant

## Step by Step Instructions

Detailed instructions are provided in the [step_by_step_guides](https://github.com/richard-vh/CDE_123_HandsOnLab/tree/main/step_by_step_guides/english).

* [Link to the English Guide](https://github.com/richard-vh/CDE_123_HandsOnLab/tree/main/step_by_step_guides/english)

## Setup Instructions

The HOL requires data and CDE dependencies (e.g. shared Files, Pyhton, Docker Resource) to be created before the event. The attached [Setup Guide](https://github.com/richard-vh/CDE_123_HOL/blob/main/setup/README.md) provides instructions for completing these requirements.

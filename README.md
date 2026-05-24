# End-to-End AWS Medallion Architecture Data Engineering Pipeline

## Overview

Built an end-to-end cloud-native data engineering pipeline using AWS services to process transactional and analytical datasets through a Medallion Architecture (Bronze → Silver → Gold).

The pipeline supports scalable ingestion, transformation, CDC processing, SCD Type-2 implementation, orchestration, and BI reporting workflows.

---

## Architecture
<img width="940" height="423" alt="image" src="https://github.com/user-attachments/assets/881b48c7-c7b7-413a-901f-f271191a57f5" />

<img width="560" height="589" alt="image" src="https://github.com/user-attachments/assets/1596c917-0d6d-421b-954d-8411fccefb39" />


### Bronze Layer

* Raw data ingestion into Amazon S3
* AWS DMS (CDC) replication from MySQL RDS
* JSON / CSV ingestion
* Partitioned by ingestion date

### Silver Layer

* AWS Glue + PySpark transformations
* Schema enforcement
* Null handling
* Deduplication
* Incremental loads
* SCD Type-2 implementation
* Parquet conversion with Snappy compression

### Gold Layer

* Amazon Redshift staging + target tables
* Stored procedures for SCD Type-2 merges
* Analytics-ready star schema
* Data marts for BI consumption

---

## Tech Stack

* AWS S3
* AWS Glue
* AWS DMS
* AWS Lambda
* AWS Step Functions
* Amazon Redshift
* Amazon RDS (MySQL)
* Amazon EventBridge
* Amazon SNS
* Amazon QuickSight
* PySpark
* SQL
* Python

---

## Key Features

* CDC pipelines using AWS DMS
* Medallion Architecture implementation
* Incremental ETL/ELT workflows
* Hash-based SCD Type-2 processing
* Step Functions orchestration
* Glue Job Bookmarks
* Predicate Pushdown optimization
* Partition pruning
* Parquet-based storage optimization
* Data Quality validations
* Automated orchestration and monitoring

---
<img width="628" height="379" alt="image" src="https://github.com/user-attachments/assets/36652147-879a-42cf-9818-8c5849e91f7c" />

## Optimizations Implemented

### DMS Batch Apply Optimization

Enabled batch apply mode to reduce creation of micro-files in S3 and improve downstream Glue performance.

### Predicate Pushdown

Reduced Glue scan volume by partition pruning based on ingestion date.

### Parquet + Snappy Compression

Reduced storage costs and improved query performance for analytical workloads.

### Hash-Based SCD Type-2

Used SHA-256 hashing strategy to detect row-level changes efficiently and optimize merge performance in Redshift.

---

## Challenges Solved

### Referential Integrity in Async Pipelines

Implemented Step Functions orchestration to ensure dimension loads completed before fact table processing.

### Slow SCD Type-2 Merges

Optimized Redshift merge strategy using hash-based delta detection and MERGE patterns.

### Duplicate Active Records

Used ROW_NUMBER() partition logic to correctly identify latest records during updates.

---

## Pipeline Flow

RDS/MySQL → AWS DMS → S3 Bronze → AWS Glue → S3 Silver → Redshift Gold → QuickSight


## Future Improvements

* Delta Lake integration
* Real-time streaming pipelines
* CI/CD automation
* Infrastructure as Code using Terraform
* Data observability integration

---

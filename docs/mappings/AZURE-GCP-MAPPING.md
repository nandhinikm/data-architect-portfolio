# Azure ↔ GCP Mapping (with the differences interviewers probe)

| Concern | Azure | GCP | Key difference to articulate |
|---|---|---|---|
| Object storage | ADLS Gen2 / Blob | Cloud Storage | ADLS has hierarchical namespace + POSIX-style ACLs; GCS is flat, IAM-based |
| Lakehouse/warehouse | Fabric, Synapse, Databricks | BigQuery (+ BigLake) | BigQuery is serverless with separated storage/compute; Fabric uses a capacity (CU) model |
| Spark | Databricks, Fabric Spark, Synapse Spark | Dataproc, Serverless Spark | Cluster vs serverless, startup time, cost model |
| Orchestration/ETL | ADF, Fabric pipelines | Cloud Composer (Airflow), Data Fusion, Workflows | ADF is low-code and connector-rich; Composer is code-first |
| Streaming ingest | Event Hubs (Kafka endpoint) | Pub/Sub, Managed Kafka | Partitions + checkpoints vs per-message ack |
| Stream processing | Stream Analytics, Fabric RTI, Spark SS | Dataflow (Beam) | Beam's unified batch/stream and event-time model |
| Real-time analytics | Fabric Eventhouse / ADX (KQL) | BigQuery streaming, Bigtable | KQL is purpose-built for telemetry |
| Governance | Purview | Dataplex, Data Catalog | Catalog + lineage + quality; scope differs |
| Identity | Entra ID, managed identity | Cloud IAM, service accounts, Workload Identity | RBAC+ACL layers vs IAM policy inheritance |
| Network isolation | Private endpoints, NSG, Firewall | Private Service Connect, VPC Service Controls | VPC-SC is an API-level exfiltration perimeter |
| Keys/secrets | Key Vault | Cloud KMS, Secret Manager | Rotation, HSM tiers |
| Monitoring | Azure Monitor, Log Analytics | Cloud Monitoring/Logging | KQL vs Logging query language |
| IaC | Bicep, Terraform | Terraform | Terraform is the common denominator |
| DR | ZRS/GRS/GZRS, UK South↔UK West | Multi-region / dual-region | Paired-region replication vs multi-region storage classes |
| BI | Power BI, semantic models | Looker | DAX vs LookML |
| ML/AI | Azure ML, AI Foundry | Vertex AI | |

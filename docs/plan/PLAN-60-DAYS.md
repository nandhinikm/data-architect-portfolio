# 60-Day Plan — UK Data Architect Portfolio

Pace: ~2–3 hrs/day. Days marked ⏱ are lighter buffers. Each day ends with a commit.
Rule: every day produces one artefact (diagram, ADR, code, test, or what-if answer). No artefact = day not done.

## Phase 1 — Foundations & scaffold (Days 1–6)
- [ ] D1 Monorepo, README, pre-commit, markdown lint, Mermaid rendering, CI skeleton (GitHub Actions)
- [ ] D2 Templates: ADR, C4, design doc, what-if, cost sheet (`docs/templates`)
- [ ] D3 Define a fictional UK client (retail bank or NHS trust) with NFRs: volume, latency, RPO/RTO, budget, regulation
- [ ] D4 Azure landing zone: management groups, subscriptions, hub-spoke, UK South primary / UK West DR; ADR on region choice
- [ ] D5 Terraform/Bicep baseline: resource groups, ADLS Gen2, Key Vault, Log Analytics, policy assignments
- [ ] D6 ⏱ Azure↔GCP mapping v1 (`docs/mappings`)

## Phase 2 — Lakehouse & modelling (Days 7–20) → projects/01
- [ ] D7 Medallion design (bronze/silver/gold), folder/partition strategy on ADLS Gen2, naming standards
- [ ] D8 ADR: Fabric vs Databricks vs Synapse (licensing, capacity, skills, lock-in)
- [ ] D9 Ingestion patterns: ADF/Fabric pipelines, CDC, full vs incremental, watermarking
- [ ] D10 Batch ingestion from a public UK dataset (ONS, data.gov.uk, Companies House) to bronze
- [ ] D11 Delta Lake internals note: transaction log, OPTIMIZE, Z-order/liquid clustering, VACUUM, time travel
- [ ] D12 Silver layer: cleansing, dedupe, schema enforcement/evolution
- [ ] D13 SCD Type 1/2/6 with MERGE; tests for late-arriving dimensions
- [ ] D14 Kimball star schema for gold; conformed dimensions
- [ ] D15 Data Vault 2.0 model of same domain; ADR: Kimball vs Data Vault vs OBT
- [ ] D16 Semantic layer: Direct Lake vs Import vs DirectQuery trade-offs
- [ ] D17 Performance: partitioning, small files, compaction, caching, skew
- [ ] D18 GCP equivalent: GCS + BigQuery + Dataform/dbt
- [ ] D19 ⏱ Lakehouse what-ifs (schema drift, duplicate loads, backfill, reprocessing)
- [ ] D20 Project 01 review: diagrams, cost table, README polish

## Phase 3 — Streaming (Days 21–28) → projects/02
- [ ] D21 Latency tiers; decide where streaming is justified
- [ ] D22 Event Hubs: partitions, consumer groups, Capture, Kafka endpoint, throughput sizing
- [ ] D23 ADR: Fabric Real-Time Intelligence vs Stream Analytics vs Spark Structured Streaming
- [ ] D24 Event time vs processing time, watermarks, late/out-of-order data
- [ ] D25 Delivery semantics: at-least-once, idempotent sinks, exactly-once limits
- [ ] D26 Lambda vs Kappa vs streaming medallion; schema registry and contracts
- [ ] D27 GCP: Pub/Sub + Dataflow (Beam) + BigQuery streaming
- [ ] D28 ⏱ Streaming what-ifs (poison messages, replay, hot partitions, consumer lag)

## Phase 4 — Governance, security, compliance (Days 29–38) → projects/03
- [ ] D29 Purview: catalog, scans, lineage, glossary, classification; owner/steward operating model
- [ ] D30 Data contracts and data products; ADR: data mesh vs central platform
- [ ] D31 Identity: Entra ID, managed identities, RBAC vs ACLs on ADLS, least privilege
- [ ] D32 Row/column-level security, dynamic masking, sensitivity labels, OneLake security
- [ ] D33 Networking: private endpoints, VNet integration, firewall, DNS, no public egress
- [ ] D34 Encryption: CMK vs PMK, Key Vault, rotation; ADR
- [ ] D35 UK GDPR / DPA 2018: lawful basis, DPIA, retention, erasure in an immutable lakehouse
- [ ] D36 Sector overlays: FCA/PRA, NHS DSPT, public sector (NCSC cloud principles), data residency
- [ ] D37 GCP: Dataplex, IAM, VPC Service Controls, CMEK, Cloud DLP
- [ ] D38 ⏱ Governance what-ifs (PII leak, access revocation, audit, erasure request)

## Phase 5 — DataOps, quality, observability (Days 39–46) → projects/04
- [ ] D39 IaC modules, dev/test/prod, state management
- [ ] D40 CI/CD for pipelines, notebooks, semantic models (GitHub Actions or Azure DevOps)
- [ ] D41 Data testing pyramid: unit, contract, quality (Great Expectations/Soda/dbt), reconciliation
- [ ] D42 Quality framework: dimensions, thresholds, quarantine, alerting, SLAs/SLOs
- [ ] D43 Observability: Azure Monitor, KQL, freshness checks, lineage impact analysis
- [ ] D44 ADR: ADF vs Fabric pipelines vs Airflow vs Databricks Workflows
- [ ] D45 GCP: Cloud Composer, Cloud Build, Dataform assertions
- [ ] D46 ⏱ DataOps what-ifs (bad deploy, rollback, upstream schema change, stuck pipeline)

## Phase 6 — Migration, DR, cost (Days 47–53) → projects/05
- [ ] D47 Migration strategy: 6Rs; on-prem SQL/Oracle/Teradata to Azure
- [ ] D48 Execution: DMS, self-hosted IR, parallel run, reconciliation, cutover and rollback
- [ ] D49 HA/DR: RPO/RTO tiers, ZRS/GRS/GZRS, UK South→UK West, runbook, game day
- [ ] D50 FinOps: Fabric capacity sizing, Databricks cluster policies, reservations, tiering, tagging
- [ ] D51 Cost model: dev/test/prod; cost per TB, per query, per user
- [ ] D52 GCP: BigQuery editions vs on-demand, multi-region DR, committed use
- [ ] D53 ⏱ Migration/DR/cost what-ifs

## Phase 7 — Capstone & interview packaging (Days 54–60) → projects/06
- [ ] D54 Capstone reference architecture, C4 levels 1–3
- [ ] D55 Review pack: NFR traceability matrix, risk register, assumptions log
- [ ] D56 AI/ML readiness: feature store, vector search, RAG data foundation
- [ ] D57 Stakeholder artefacts: exec one-pager, now/next/later roadmap, business case
- [ ] D58 Mock interviews: answer 20 what-ifs aloud, 5 min each
- [ ] D59 Repo polish: pinned repos, profile README, LinkedIn, CV bullets with measurable outcomes
- [ ] D60 Publish a write-up on one ADR; submit a talk to a UK community event

## Definition of done per day
Committed files, diagrams render, links valid, one "what changed my mind" note.

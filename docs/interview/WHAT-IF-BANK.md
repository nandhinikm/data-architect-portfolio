# What-If Interview Bank — Data Architect (UK, Azure-first, GCP notes)

How to answer every one: **Clarify → Detect → Contain → Fix → Prevent → Trade-off.** State assumptions and NFRs first. Add a GCP aside in one sentence.

## 1. Requirements & architecture approach
- Stakeholders disagree on latency (finance wants T+1, ops wants real time). How do you decide? → tiered latency, cost per tier, value of freshness.
- Requirements change after the design is signed off. → ADR supersession, change impact via NFR traceability.
- Build vs buy vs SaaS for ingestion (Fivetran/ADF/custom)? → TCO, skills, lock-in, connector coverage.
- Data mesh vs central platform in a 300-person org with 2 data teams? → maturity, domain ownership, federated governance cost.

## 2. Storage & lakehouse
- A bronze table has 40 million small files. → compaction/OPTIMIZE, Auto Optimize, ingestion batching, file-size targets.
- Two jobs write the same Delta table concurrently. → optimistic concurrency, conflict resolution, partition-scoped writes.
- Someone ran VACUUM with short retention and time travel broke. → retention policy, backups, shallow clones, guardrails.
- Schema drift from upstream (column renamed/type changed). → schema enforcement vs evolution, contracts, quarantine, alert.
- Need to reprocess 3 years of history without impacting prod. → backfill design, idempotency, isolated capacity, cost cap.
- ADLS hierarchical namespace off by mistake. → rename costs, ACL limits, migration path. GCP: flat namespace by design.

## 3. Modelling
- Late-arriving dimension rows. → inferred members, SCD2 rewrite, reprocess window.
- Fact grain changes mid-project. → new fact table vs restate, conformed dimensions, versioning.
- Data Vault vs Kimball for a regulated bank with many sources? → auditability, agility, query cost, business vault.
- Semantic model slows at 50 concurrent users. → aggregations, Direct Lake fallback to DirectQuery, capacity sizing, composite models.
- Same KPI defined differently by two departments. → metrics layer, governed semantic model, ownership.

## 4. Ingestion & integration
- Source system cannot support CDC; full extract takes 9 hours. → watermark on updated_at, hash diff, log-based alternatives, change windows.
- Source API rate-limits you. → backoff, incremental, parallelism cap, queue buffering.
- Self-hosted IR is a single point of failure. → HA nodes, patching, network path, monitoring.
- Duplicate files delivered by a vendor. → idempotent loads, file manifest, checksum, dedupe keys.
- Source goes offline for 3 days. → catch-up logic, SLA communication, backpressure.

## 5. Streaming
- Consumer lag grows to hours. → scale consumers/partitions, hot partition detection, backpressure, autoscale.
- Poison message blocks a partition. → dead-letter, schema validation at edge, retry policy.
- Events arrive 2 hours late. → watermarks, allowed lateness, reconciliation batch, correction events.
- Exactly-once claimed by vendor. → idempotent sinks, transactional offsets, end-to-end vs per-hop.
- Need to replay 7 days of events. → Event Hubs retention/Capture, replay isolation, dedupe. GCP: Pub/Sub seek/snapshots.
- Partition count chosen too low. → cannot increase freely on some SKUs; plan for growth, repartitioning strategy.

## 6. Security & identity
- A contractor leaves; how do you prove access is gone everywhere? → group-based RBAC, access reviews, PIM, audit logs.
- Storage account has public network access enabled. → Azure Policy deny, defender alerts, private endpoints only.
- Service principal secret leaked in a repo. → rotate, managed identity/OIDC federation, secret scanning, revoke tokens.
- Analysts need production data for testing. → masked/synthetic data, dynamic masking, subsetting.
- RBAC vs ACL conflict on ADLS (user can/cannot read). → evaluation order (RBAC then ACL), least privilege, group design.
- Key Vault outage or key deleted with CMK. → soft delete, purge protection, access impact, DR.

## 7. Governance & compliance (UK)
- Data subject erasure request for a record in bronze, silver, gold and backups. → PII isolation/tokenisation, crypto-shredding, delete via MERGE + VACUUM, backup retention disclosure.
- ICO asks where personal data lives. → Purview classification, lineage, data inventory, ROPA.
- Data must remain in the UK. → UK South/West, policy for allowed locations, replication checks, SaaS sub-processor review.
- Purview scan finds unclassified PII in a free-text column. → classification rules, remediation owner, quarantine.
- Cross-border transfer (UK→US) needed. → UK IDTA/Addendum, transfer risk assessment.
- NHS or FCA-regulated workload. → DSPT, DPIA, operational resilience/outsourcing expectations, audit trails.

## 8. Quality & observability
- Dashboard numbers are wrong; who finds out first? → freshness/volume/distribution tests, SLOs, alert routing.
- Quality check fails on 2% of rows. → quarantine vs fail-fast, thresholds per criticality, data owner workflow.
- Reconciliation mismatch after migration. → row counts, checksums, aggregates, tolerance, root-cause patterns.
- Upstream deploy broke a contract. → contract tests in CI, versioning, consumer notification.

## 9. DataOps & delivery
- Bad pipeline deployed to prod. → blue/green or feature flags, rollback, idempotent reruns, release gates.
- Notebook-based pipelines are untestable. → refactor to packages, unit tests, parameterised jobs.
- Environment drift between dev and prod. → IaC only, policy, drift detection.
- Terraform state corrupted/locked. → remote state with locking, backups, import, break-glass.
- Fabric workspace Git integration conflicts. → branching strategy, deployment pipelines, item-level merge limits.

## 10. Performance & cost
- Fabric capacity throttled at month-end. → smoothing/bursting, workload isolation, scheduling, scale up temporarily, capacity per domain.
- Databricks bill doubled. → cluster policies, auto-termination, job vs all-purpose compute, spot, tagging.
- BigQuery query scanned 50 TB. → partition/cluster, require partition filter, quotas, editions. Azure analogue: Synapse/Fabric scan cost and pruning.
- Storage cost growing 8% monthly. → lifecycle tiering, retention, compaction, duplicate datasets.
- Query slow after table growth. → statistics, file layout, clustering, materialised views.

## 11. HA / DR / resilience
- UK South region outage. → RPO/RTO by tier, GRS/GZRS, secondary capacity, runbook, DNS/endpoint switch.
- Accidental deletion of a container. → soft delete, versioning, immutable storage, restore drill.
- Ransomware on storage. → immutability, separate identity, backups, detection.
- DR test fails. → treat as finding; fix runbook and automation, retest quarterly.
- Deliver 99.9% SLA on a platform of 12 dependencies. → composite availability maths, weakest-link analysis.

## 12. Migration
- Teradata/Oracle to Azure in 12 months. → inventory, dependency graph, 6Rs per workload, parallel run, wave plan.
- Business refuses downtime. → CDC sync, cutover rehearsal, rollback criteria.
- Stored procedures with business logic. → translate vs re-write, test harness, equivalence tests.
- Dual-running costs exceed budget. → shorten parallel window, sampling reconciliation, decommission plan.

## 13. AI / ML readiness
- Data science asks for production data in notebooks. → governed feature layer, sandboxed workspace, masking.
- RAG over enterprise documents. → ingestion, chunking, ACL propagation to the index, deletion sync, freshness.
- Model drift detected. → monitoring, retraining triggers, lineage to training data.

## 14. Leadership & communication
- CTO asks "why not just use Snowflake?" → criteria-based comparison, org fit, exit cost, not tool tribalism.
- Team resists your standards. → enablement, templates, guardrails over gates, measure adoption.
- Budget cut of 30%. → ranked levers, risk of each, phased reductions.
- You made a wrong architectural call. → show detection, communication, correction, lesson.

## 15. Compare-and-choose questions to rehearse
Fabric vs Databricks vs Synapse | Kimball vs Data Vault | ADF vs Airflow | Event Hubs vs Kafka vs Pub/Sub | Delta vs Iceberg vs Parquet-only | RBAC vs ACL | Private endpoint vs service endpoint | Lambda vs Kappa | Batch vs micro-batch vs streaming | Mesh vs central

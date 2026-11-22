# Data Architect Portfolio (UK) — Azure-first, GCP-aware

![CI](https://github.com/nandhinikm/data-architect-portfolio/actions/workflows/ci.yml/badge.svg)

![CI](https://github.com/<YOUR-GITHUB-USERNAME>/data-architect-portfolio/actions/workflows/ci.yml/badge.svg)

Goal: demonstrate senior/principal data architect credibility through **decisions, trade-offs and evidence**, not tool screenshots.

## How to read this repo
| Folder | What it proves |
|---|---|
| `projects/01-lakehouse-medallion` | Storage, modelling, Fabric/Databricks/Synapse choices |
| `projects/02-streaming-realtime` | Event-driven design, exactly-once, late data |
| `projects/03-governance-security` | Purview, RBAC, masking, UK GDPR |
| `projects/04-dataops-cicd` | IaC, CI/CD, testing, observability |
| `projects/05-migration-dr-finops` | Migration, DR, cost control |
| `projects/06-capstone-uk-enterprise` | End-to-end reference architecture |
| `docs/interview` | What-if scenario bank with model answers |
| `docs/mappings` | Azure ↔ GCP service equivalence and trade-offs |

## Standard for every project (non-negotiable)
1. `README.md`: problem, constraints, NFRs (volume, latency, RPO/RTO, budget), outcome.
2. `architecture/`: C4 (context, container), data flow, Mermaid in-repo.
3. `adr/`: one ADR per significant decision, including rejected options.
4. `azure/`: Bicep or Terraform + pipeline code. `gcp/`: equivalent design note, plus Terraform for the key component.
5. `tests/`: data quality + infra validation.
6. `WHAT-IF.md`: failure and change scenarios with your answer.
7. Cost estimate table (monthly, per environment) with assumptions.

## Progress
See `docs/plan/PLAN-60-DAYS.md`. Tick off days in the tracker.

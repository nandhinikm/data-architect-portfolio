# ADR-0002: Folder structure
- Status: Accepted
- Date: 2026-11-22
- Deciders: Nandhini

## Context
Each project must show Azure implementation and GCP equivalents, plus architecture, decisions, tests and cost.

## Options considered
| Option | Pros | Cons | Cost | Risk |
|---|---|---|---|---|
| Folder per capability, with azure/ and gcp/ inside | Easy side-by-side comparison | More folders | Low | Empty gcp/ folders |
| Folder per cloud at the top level | Simple cloud separation | Splits one design across two places | Low | Designs drift apart |
| Flat repo with prefixes | Minimal nesting | Hard to navigate | Low | Clutter |

## Decision
One folder per capability with architecture/, adr/, azure/, gcp/ and tests/ inside.

## Consequences
Each project reads as one coherent design. GCP content may be a design note plus one Terraform component rather than a full build.

## Azure vs GCP note
This structure is what makes the comparison visible.

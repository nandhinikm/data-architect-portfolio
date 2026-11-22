# ADR-0001: Repository strategy
- Status: Accepted
- Date: 2026-11-22
- Deciders: Nandhini

## Context
I am building a public portfolio to show data architect credibility to UK hiring managers. A separate AI architect portfolio already exists. Reviewers will scan quickly, so the repo must be focused.

## Options considered
| Option | Pros | Cons | Cost | Risk |
|---|---|---|---|---|
| New dedicated repo | Clear positioning, clean history | Tooling must be copied | Low | Duplicated setup |
| Subfolder in AI architect monorepo | One repo to maintain, shared CI | Mixed message to reviewers | Low | Diluted focus |
| Many small repos per project | Easy to pin individually | Hard to keep consistent, scattered | Medium | Standards drift |

## Decision
New dedicated monorepo for data architecture. Cross-link to the AI architect repo from the README.

## Consequences
Positive: focused story, independent history. Negative: tooling copied once. Revisit if maintenance overhead becomes a problem.

## Azure vs GCP note
Not cloud-specific.

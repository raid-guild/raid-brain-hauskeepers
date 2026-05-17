# Maintenance SOPs & Playbooks Workstream Summary

**Date:** 2026-05-17  
**Workstream:** Maintenance SOPs & Playbooks  
**Scope:** Infrastructure management, operational runbooks, AI-assisted workflow documentation, architecture overview, repository map, complete handoff-ready SOP packet

---

## What Was Built

The SOP workstream produced a complete DAOhaus Maintenance & Transition Readiness Packet at `/daohaus-maintenance-sop/packet/`. The packet is structured as eight standalone documents that a new or departing maintainer can read in sequence or use as individual runbook references.

### Packet Structure

| Doc | Content |
| --- | --- |
| `01_transition_readiness_overview.md` | Purpose, intended audience, how to use the packet |
| `02_system_overview_architecture.md` | High-level narrative, core applications, contracts, indexing, data flow |
| `03_repository_application_inventory.md` | Active repos with purpose, deprecated repos, user-facing apps, supporting packages |
| `04_infrastructure_access_dependencies.md` | Full infrastructure table, access matrix, hosting, CI/CD, DNS, The Graph, RPC providers, billing, SPOFs |
| `05_maintenance_sops_operational_runbooks.md` | Routine cadence, deployment/rollback, subgraph operations, dependency maintenance, incident response, onboarding/offboarding |
| `06_ai_assisted_maintenance_workflows.md` | Issue lifecycle, agent branch workflow, automation outputs, human review gates, maintainer usage guidelines |
| `07_known_risks_open_items_maintenance_gaps.md` | Current risks, unowned responsibilities, fragile dependencies, pending decisions, recommended next actions |
| `08_stewardship_handoff_checklist.md` | Checklist for confirming access, reviewing inventory, verifying ownership, and recording transition notes |

---

## Key Content Produced

### Operating Model

The packet draws a clear boundary around what routine maintenance covers and what requires escalation. Routine maintainers work through GitHub pull requests, Railway deployments, and support intake. The following are explicitly not routine work: contract upgrades, DNS or registrar changes, The Graph multisig or billing changes, production secrets, and access-control changes. Calling this out as a boundary — not just a note — is what makes the packet useful to a new maintainer who might otherwise guess about scope.

### Deployment and Rollback Runbook

The deployment runbook covers the four Railway-hosted surfaces (admin app, website, docs, guide) with pre-merge review steps, post-merge verification, and a rollback path that uses git revert plus normal Railway deployment rather than Railway-specific rollback tooling. The key principle: if a production issue blocks normal usage, rollback is the priority over debugging. Debug the failed change after the surface is stable.

### Subgraph Operations Runbook

The subgraph section treats indexing changes as higher-risk than app or docs changes. Specific callouts: prefer additive schema changes (removing fields or changing field types can break apps querying existing subgraphs), deploy coordinated changes across all production networks when app queries depend on new schema, and verify the admin app can read DAO/proposal/member/treasury data after any subgraph deploy. External billing and deployment details point to `docs.daohaus.club/contributing/subgraphs` rather than duplicating steps that have their own canonical source.

### Dependency Maintenance

The runbook explicitly names known high-cost dependency areas rather than giving generic "review before updating" advice:

- WalletConnect proposal support: explicit keep/isolate/deprecate decision required before touching
- `wagmi` major upgrades: wallet-stack projects, not routine bumps
- Coinbase CDP / Axios advisories: track through upstream `wagmi` and connector updates
- `ethers-multisend`: needs decode behavior tests before replacement

Named anti-patterns: `npm audit fix --force`, treating a major `wagmi` upgrade as a patch, replacing WalletConnect support without validating proposal/session behavior.

### Onboarding and Offboarding

The onboarding section separates baseline access (GitHub repos, Railway, `@warcamp` Discord role) from task-specific access (Refactory, `@hauskeeper` role, The Graph or multisig access). This separation prevents over-provisioning: a maintainer doing deployment work does not need subgraph billing access, and one doing AI-assisted triage does not need The Graph multisig. Offboarding includes a key rotation step for shared or maintainer-owned keys when the departing person controlled them.

### AI-Assisted Workflow Integration

Section 06 documents how the Refactory-based AI maintenance system integrates into the normal operational flow — covering the issue lifecycle, agent branch and review conventions, human review gates, automation output cadence, and the system-of-record split (Refactory for intent/status, GitHub for code/merge, Railway for deployments, Prism for operational history).

---

## What This Means for RG

**The packet structure is reusable.** The eight-document layout — overview, architecture, repo inventory, infrastructure/access, runbooks, AI workflows, risks, handoff checklist — covers what any legacy web3 project maintenance engagement needs to document. RG can template this structure and adapt it to a new client without starting from scratch.

**Named anti-patterns are more valuable than generic advice.** Telling a future maintainer "don't do `npm audit fix --force`" with the specific reason (it can silently break wallet-stack behavior) is more useful than "review dependencies carefully." Concrete evidence from the DAOhaus codebase makes the runbook defensible, not just advisory.

**The access matrix and SPOF callouts are the highest-value sections for a transition.** An SOP can be generic, but an access matrix for a specific project — which systems exist, who holds access, and what breaks if that person is unavailable — is the document that actually enables handoff. This is the section future RG engagements should produce early, not at the end.

**Scope boundaries need to be explicit, not implied.** The "this is not routine maintainer work" callout — contract upgrades, DNS, multisig access — exists because a new maintainer might otherwise guess that these fall within their remit. Making it explicit prevents both over-reach and under-reaction during incidents.

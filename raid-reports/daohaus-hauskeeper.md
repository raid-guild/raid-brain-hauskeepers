---
title: DAOhaus Hauskeeper Raid
slug: daohaus-hauskeeper
client: DAOhaus
guild: Raid Guild
raid_status: completed
visibility: internal
date_start: 2026-04
date_end: 2026-05
service_areas:
  - legacy modernization
  - ai-assisted maintenance
  - maintainer enablement
  - operational documentation
  - community surface cleanup
tags:
  - daohaus
  - dark-factory
  - superprism
  - refactory
  - ai-assisted-maintenance
  - web3-infrastructure
  - sops
summary: Raid Guild modernized DAOhaus infrastructure, reduced its maintenance surface area, documented the operating model, and deployed a human-in-the-loop AI-assisted maintenance workflow.
hero_claim: A cohort AI automation spike became a client-funded maintenance engagement, then hardened into the beginning of a repeatable Refactory service offering.
source_repo: hauskeeper-raid-kb
related_outputs:
  - outputs/daohaus-raid-recap-case-study.md
  - outputs/ai-assisted-maintenance-service-one-pager.md
---

# DAOhaus Hauskeeper Raid

## Overview

The DAOhaus Hauskeeper raid was a Raid Guild infrastructure modernization and AI-assisted maintenance engagement for DAOhaus. The raid addressed a mature web3 project with live infrastructure, years of accumulated software history, scattered public and maintainer-facing surfaces, and a need to support future protocol maintainers without assuming a large standing team.

Raid Guild delivered a fixed-scope sprint across five workstreams:

- Codebase consolidation and modernization.
- Internal architecture and maintenance documentation.
- AI-assisted maintenance infrastructure.
- DAOhaus community and repo surface-area reduction.
- Maintenance SOPs and transition readiness materials.

The raid also served a second Raid Guild purpose: proving that Dark Factory and Superprism-style AI workflow experiments could be shaped into a repeatable client service. DAOhaus became the pilot case for an AI-assisted maintenance readiness offer built around cleaner software surfaces, agent-ready docs, SOPs, and a human-governed Refactory workflow.

## The Story

A few months before the DAOhaus raid, Raid Guild members piloted Dark Factory in the Raid Guild cohort. Dark Factory explored AI workflow automation: how agents, memory systems, and structured workflows could support software maintenance, knowledge capture, issue triage, and recurring operational work.

The cohort work created a strong question for Raid Guild: could this experimentation become a real service for a live client with production risk?

DAOhaus had the right shape for that test. The protocol and product suite still mattered, but the surrounding systems had become harder to maintain over time. Repos, packages, docs, public surfaces, Discord channels, DNS records, deployment systems, and operational knowledge had accumulated across many years and many contributors. DAOhaus needed a path toward maintainability, future stewardship, and protocol maintainer support.

Raid Guild shaped the engagement around that need. The work was not pitched as "let the agent run DAOhaus." It was framed as an infrastructure modernization and maintenance readiness sprint with AI-assisted workflows layered in after the system was made easier to understand.

That distinction became central to the raid's value. The best AI maintenance work did not begin with automation. It began with reducing complexity, clarifying active systems, documenting how the project works, and defining where humans must approve decisions.

The raid also hardened Superprism-side experimentation into the Superprism Refactory pattern: a deployable maintenance control plane that combines Codex execution, Prism Memory and Knowledge, Discord intake, GitHub review, Railway deployment context, and explicit human approval gates.

## Client Need

DAOhaus needed long-term maintenance readiness for a mature protocol software ecosystem.

Core needs:

- Identify and support protocol maintainers without depending on a large standing team.
- Reduce codebase complexity and dependency risk in the active admin app.
- Clarify which repos, docs, apps, DNS records, and Discord channels were active versus legacy.
- Preserve operational knowledge in durable docs and handoff materials.
- Make the system easier for future human maintainers and AI coding agents to navigate.
- Introduce AI-assisted workflows without giving production control to an unbounded autonomous agent.

The underlying pain was not only technical debt. It was operating-model debt: too many surfaces, too much implicit knowledge, and too little structured handoff context for future maintainers.

## Scope And Deliverables

### Scope Sold

DAOhaus funded a structured modernization, documentation, and maintenance readiness sprint executed by Raid Guild.

The sold scope included:

- **Codebase consolidation and modernization:** simplify the active app, update dependencies and tooling, reduce legacy SDK/package dependency, resolve key bugs, and redefine the deployment pipeline.
- **Internal architecture and maintenance documentation:** document repository structure, architecture, deployment, dependencies, constraints, and system maps for both human and AI-assisted maintenance.
- **AI-assisted maintenance infrastructure:** set up agentic development workflows for issue triage, code analysis, implementation assistance, monitoring, escalation, and GitHub issue management.
- **Community surface-area reduction:** clean and consolidate Discord, clarify active repositories, mark unused repositories as deprecated, clean public docs, and ensure public documentation reflects active tools and systems.
- **Maintenance SOPs and playbooks:** produce operational runbooks, access and infrastructure documentation, AI-assisted workflow guidance, architecture overview, repo inventory, and a complete transition readiness packet.

### Delivered

Raid Guild delivered:

- A standalone modernized DAOhaus admin app built with Vite, React, and TypeScript.
- Extraction from the prior NX/Webpack/Babel monorepo.
- Local inlining of internal `@daohaus/*` packages under the active app source.
- Major dependency modernization across React, TanStack Query, React Router, wagmi, viem, and RainbowKit.
- A simplified `app/`, `features/`, and `lib/` repo structure.
- Reduced path alias surface and clearer ownership boundaries for future human and AI maintainers.
- A layered documentation set including architecture, environment, verification, domain glossary, debugging, and local `AGENT.md` files.
- A reusable AI maintainer prompt for agent sessions.
- GitHub, docs, DNS, and Discord surface-area cleanup.
- A DAOhaus-specific Superprism Refactory instance for AI-assisted maintenance.
- A human-in-the-loop issue lifecycle from intake through review.
- Prism Memory and Prism Knowledge setup patterns for preserving operational history and curated reference docs.
- An eight-document Maintenance and Transition Readiness Packet.

## Outcomes

### For DAOhaus

DAOhaus received a clearer, more maintainable operating surface.

Important outcomes:

- The active admin app became independently deployable and easier to reason about.
- The repo structure was simplified for both humans and AI agents.
- Legacy and active public surfaces were more clearly separated.
- Discord, support, docs, and repo paths became easier to navigate.
- Maintenance responsibilities were documented in runbooks instead of held only in contributor memory.
- High-risk operational boundaries were made explicit.
- Future maintainers gained an access matrix, repo inventory, architecture context, and stewardship handoff checklist.
- AI-assisted maintenance became available through a controlled workflow rather than unbounded production automation.

### For Raid Guild

The raid created a reusable proof point for a new service category: AI-assisted maintenance readiness for mature web3 projects.

Important outcomes:

- Dark Factory cohort learning was converted into client-funded delivery.
- Superprism Refactory moved from concept toward a deployable maintenance platform pattern.
- The SOP packet structure became a reusable template for future maintenance engagements.
- Agent-ready documentation became a clearer billable deliverable.
- Human-in-the-loop AI maintenance became a stronger sales narrative than full automation.
- The raid produced reusable language for case studies, sales proof points, and future proposals.

## Learnings

### Codebase Simplification Is AI Readiness

Observation: AI agents are more effective when the repo has a clear semantic shape.

Evidence: The DAOhaus admin app was reorganized around `app/`, `features/`, and `lib/`, and the alias surface was reduced to three stable roots. Feature-specific utilities, hooks, and components were colocated instead of scattered through broad shared folders.

Why it matters: For future clients, modernization and AI readiness should not be scoped as separate unrelated efforts. Codebase simplification is part of the AI enablement layer.

### Local Agent Docs Outperform Remote Wikis During Maintenance

Observation: Colocated docs guide agents and maintainers at the moment they are editing code.

Evidence: The raid produced local `AGENT.md` files for major app, feature, and library areas, along with root-level architecture, debugging, environment, verification, and glossary docs.

Why it matters: A wiki may explain the project, but local docs guide the maintainer while they work. This is a repeatable deliverable for agent-ready repos.

### A Maintainer Prompt Is A First-Class Artifact

Observation: Operational instructions for AI agents are distinct from reference documentation.

Evidence: The raid produced a copyable LLM maintainer prompt that encodes reading order, layer ownership, routing assumptions, tracing discipline, and verification reporting.

Why it matters: A client can paste a maintainer prompt into future AI coding sessions or give it to contractors. It reduces variance in how agents approach the codebase.

### Symptom-Based Debugging Docs Are High Leverage

Observation: Bugs arrive as user symptoms, not architecture questions.

Evidence: The DAOhaus documentation included a debugging guide that maps real reports, such as proposal state issues or missing Safe balances, to likely code paths.

Why it matters: Debugging docs reduce time to first relevant file and are more useful during active maintenance than architecture-only docs.

### Human-In-The-Loop Is A Sales Feature

Observation: The most credible AI maintenance pitch is not full autonomy.

Evidence: The DAOhaus Refactory workflow requires human confirmation before status transitions, implementation, branch acceptance, pull request approval, merge, incident treatment, or production configuration changes.

Why it matters: Clients operating production systems are more likely to trust "the agent handles groundwork; humans handle decisions" than a claim that the system can run itself.

### Memory And Knowledge Need Separate Lanes

Observation: Operational history and curated reference material should not be collapsed into one pile.

Evidence: Prism separates Memory, which records what happened, from Knowledge, which stores stable reference material such as SOPs, runbooks, and architecture docs.

Why it matters: Future agent sessions need clean context. The promotion path from raw event to artifact to memory index to curated knowledge doc should be standard in AI-assisted maintenance engagements.

### Surface-Area Reduction Belongs In Maintenance Readiness

Observation: Legacy projects accumulate more than code debt.

Evidence: DAOhaus cleanup covered active and deprecated repos, public docs, Discord channels, DNS records, Railway-hosted surfaces, support paths, and community roles.

Why it matters: A maintainable project surface includes GitHub, docs, Discord, DNS, hosting, and support intake. Automation should come after the active surface is clarified.

### SOPs Should Name Dangerous Operations

Observation: Specific anti-patterns are more useful than generic caution.

Evidence: DAOhaus runbooks named concrete danger zones such as `npm audit fix --force`, routine treatment of major `wagmi` upgrades, and subgraph schema field removals.

Why it matters: Under maintenance pressure, operators need memorable, project-specific warnings with concrete failure modes.

### Access Matrices Should Be Produced Early

Observation: Access discovery is one of the highest-value parts of maintenance handoff.

Evidence: The DAOhaus SOP packet mapped systems such as GitHub, Railway, DNS, The Graph, Alchemy, WalletConnect, Sequence, and Discord bot credentials.

Why it matters: Access matrices reveal single points of failure before a crisis and give new maintainers an immediately useful operational map.

## Reusable Patterns

### Maintenance Readiness Packet

The eight-document packet structure is reusable for other legacy web3 maintenance engagements:

- Transition readiness overview.
- System overview and architecture.
- Repository and application inventory.
- Infrastructure, access, and dependencies.
- Maintenance SOPs and operational runbooks.
- AI-assisted maintenance workflows.
- Known risks and open maintenance gaps.
- Stewardship handoff checklist.

### Agent-Ready Documentation Layer

Repeatable doc set:

- `README.md` as front door.
- Architecture overview.
- Symptom-based debugging guide.
- Environment documentation.
- Verification guide.
- Domain glossary.
- Local `AGENT.md` files at meaningful folder boundaries.
- Copyable maintainer prompt.

### Human-In-The-Loop Issue Lifecycle

Reusable lifecycle:

```text
Inbox -> Triaging -> Ready for Agent -> Working -> Awaiting Review -> Approved
```

Revision loop:

```text
Awaiting Review -> Changes Requested -> Working -> Awaiting Review
```

Human gates should stay explicit at intake, implementation, branch acceptance, pull request review, merge, incident escalation, and production configuration changes.

### Refactory Instance Pattern

A client-specific Refactory instance can be deployed from a reusable Railway template while keeping runtime state isolated per client.

Reusable service pattern:

- Site/API control plane.
- Codex Runtime.
- Prism Memory.
- Discord adapter.
- Memory cron.
- Knowledge cron.
- Discord sync cron.

Instance-specific state:

- Secrets.
- Volumes.
- Codex auth.
- Discord credentials.
- Target repos.
- Cron schedules.
- Runtime artifacts.

### Memory And Knowledge Promotion Path

Reusable context lifecycle:

```text
raw event / execution -> artifact -> memory index -> curated knowledge doc
```

This gives future agents historical context without polluting the stable reference layer.

## Content Development

### Case Study Angles

- **Cohort to client:** Raid Guild members explored AI automation through Dark Factory, recognized client value, and turned the learning into a DAOhaus engagement.
- **Legacy protocol sustainability:** DAOhaus used Raid Guild to turn accumulated operational complexity into a maintainable system.
- **Human-centered AI maintenance:** The Refactory helps one maintainer act with more leverage while preserving human review over production-affecting decisions.
- **Productized raid learning:** The engagement produced reusable templates, SOP packet structures, prompts, and platform lessons.
- **Agent-ready modernization:** The most valuable AI work started before automation: simplifying the repo, documenting boundaries, and reducing public surface area.

### Sales Proof Points

- Raid Guild can modernize a mature web3 app while preserving active protocol functionality.
- Raid Guild can convert a messy repo and public surface into a clearer maintenance environment.
- Raid Guild can deploy AI-assisted workflows with explicit human governance.
- Raid Guild can produce handoff-ready SOPs, access matrices, and runbooks for future maintainers.
- Raid Guild can turn internal experimentation into a repeatable client offering.

### Social / Announcement Hooks

- Raid Guild took DAOhaus from legacy maintenance burden to agent-ready operating surface.
- The DAOhaus raid shows how AI-assisted maintenance works best: humans make decisions, agents do groundwork.
- Dark Factory started as a cohort spike. DAOhaus turned it into a client-proven maintenance pattern.
- The Refactory is not about replacing maintainers. It is about giving maintainers more leverage.
- The next frontier for mature protocols is not just new features. It is sustainable, documented, AI-assisted stewardship.

### Content Assets To Develop

- Public case study based on `outputs/daohaus-raid-recap-case-study.md`.
- Service offering page based on `outputs/ai-assisted-maintenance-service-one-pager.md`.
- Diagram of the Refactory maintenance loop.
- Before/after repo structure visual for the admin app.
- SOP packet table-of-contents visual.
- Example issue lifecycle from Discord intake to agent branch to human review.
- Quote prompts for DAOhaus and Raid Guild contributors.

## Related Links

### Source Docs

- `docs/proposal.md` — DAOhaus Infrastructure Modernization and AI-assisted Maintenance Workflow Initiative.
- `docs/000_scope.md` — DAOhaus and Dark Factory opportunity notes and workstream scope.
- `docs/005_agent_doc_plan.md` — agent-ready documentation planning.
- `docs/006_prompt_for_llm_maintainer.md` — reusable LLM maintainer prompt.
- `docs/007_repo_docs_overview.md` — repo documentation overview.
- `docs/008_issue_and_git_flow.md` — issue and Git workflow planning.
- `docs/009_sop_workstream_ideation.md` — SOP workstream ideation.
- `docs/010_dns_catalog.md` — DNS and hosting surface catalog.
- `docs/011_community_surface_plan.md` — community surface reduction plan.
- `docs/014_discord_cleanup.md` — Discord cleanup notes.
- `docs/015_prism_platform_stack.md` — Prism platform stack notes.
- `docs/016_prism_site_api_model.md` — Prism site/API model.
- `docs/017_prism_memory_knowledge_systems.md` — Prism Memory and Knowledge split.
- `docs/018_prism_template_instances.md` — Prism template and instance pattern.

### Summaries

- `summaries/MIGRATION_SUMMARY.md` — admin app migration summary.
- `summaries/2026-04-21_architecture-and-documentation-phase.md` — architecture and documentation phase.
- `summaries/2026-05-05_reduced-community-repo-surface-area.md` — repo, docs, Discord, and public surface cleanup.
- `summaries/2026-05-17_ai-assisted-maintenance-system.md` — Refactory and AI-assisted maintenance system.
- `summaries/2026-05-17_maintenance-sops-playbooks.md` — SOP and transition readiness packet.

### Outputs

- `outputs/daohaus-raid-recap-case-study.md` — internal recap and public case study seed.
- `outputs/ai-assisted-maintenance-service-one-pager.md` — service offering one-pager.

### Learnings

- `learnings.md` — accumulated raid learnings for Raid Guild and future clients.

### External Links

- `https://refactory.superprism.io/` — Superprism Refactory platform referenced by the DAOhaus AI-assisted maintenance workstream.
- `https://daohaus.club` — DAOhaus public website.
- `https://admin.daohaus.club` — DAOhaus admin app.
- `https://docs.daohaus.club` — DAOhaus docs.
- `https://guide.daohaus.club` — DAOhaus guide.

## Source Notes

This report is internal-facing. It includes service-offering, platform, and operational framing that may need review before public release.

Claims are drawn from local repo materials, especially `summaries/`, `learnings.md`, `docs/000_scope.md`, `docs/proposal.md`, Prism docs `015` through `018`, and the two output drafts in `outputs/`.

Metrics still to collect before public case study use:

- Number of repos labeled active, deprecated, or historical.
- Number of Discord channels before and after cleanup.
- Number of docs created or updated in the DAOhaus app repo and SOP packet.
- Dependency/version before-and-after table for the admin app.
- Time-to-onboard estimate for a new maintainer before and after the packet.
- Concrete examples of issues processed through the Refactory workflow.

Public-safety review needed:

- Confirm what can be said publicly about DAOhaus access gaps, billing systems, and single points of failure.
- Confirm whether Superprism Refactory details can be named at the current level.
- Confirm whether internal cohort and member-side project history should be attributed to specific people.
- Confirm which links should be public versus kept internal to Raid Guild.


# Service Offering Exploration Summary

**Date:** 2026-05-18  
**Workstream:** Service Offering Exploration  
**Scope:** How the DAOhaus Hauskeeper raid could become a repeatable Raid Guild offering

---

## Working Offer

Raid Guild helps mature protocols and software communities turn difficult-to-maintain systems into clearer, documented, agent-ready maintenance environments.

The DAOhaus raid suggests an offer that is not simply "AI maintenance." The stronger framing is maintenance readiness plus human-governed AI leverage:

> Clean up the operating surface, document how the system actually works, establish human approval gates, and deploy a workflow that lets AI agents handle triage, investigation, branch preparation, and knowledge retrieval without taking production decisions away from humans.

For Raid Guild, this could become a service line around legacy modernization, stewardship transition, and AI-assisted maintainer enablement.

## Potential Targets

### Mature Web3 Protocols

These are protocols with live contracts, active users, public docs, old repos, and reduced core-team capacity. They may still be valuable, but the people who originally understood the whole system have moved on, scaled back, or become bottlenecks.

Likely examples:

- Protocols that launched during a prior cycle and still have users or treasury.
- DAOs with active governance but aging frontends and docs.
- Public-goods infrastructure projects that need continuity but cannot justify a large standing engineering team.
- Protocols preparing to hand maintenance to a foundation, working group, vendor, or community maintainer.

### Lean Product Teams With Large Maintenance Surfaces

These teams may not describe themselves as "legacy," but they feel the same pain: many apps, packages, support channels, deployment targets, and dependencies, with only a few people able to safely touch them.

Likely examples:

- Small teams operating multiple frontends, docs sites, bots, subgraphs, and data services.
- Teams where support, dependency updates, and bug triage crowd out product work.
- Teams that want to use AI coding tools but know their repo and docs are too chaotic for safe delegation.

### Ecosystem Funders And Stewardship Programs

Funders may be strong buyers because their pain is portfolio-level: they need important infrastructure to stay usable without permanently funding full teams for every project.

Likely examples:

- Ecosystem foundations funding maintenance of older tools.
- Grant programs trying to keep public-goods apps available.
- Governance bodies that need to evaluate whether a project is ready for handoff.

## Pain Points To Target

### Operating Surface Sprawl

DAOhaus showed that maintenance debt is not only in code. It also lives in repos, Discord channels, docs, DNS records, hosting platforms, deployment workflows, support paths, credentials, and contributor memory.

Buyers may feel this as:

- "We do not know which repos are active."
- "The docs do not match the app."
- "Support requests arrive everywhere."
- "Only one person knows where the deployment or billing lives."
- "We cannot onboard a new maintainer without weeks of explanation."

### Risky Dependency And App Maintenance

Mature web3 apps often sit on fast-moving dependency stacks: wallet connectors, RPC providers, subgraphs, package managers, build tools, auth systems, and hosting services. Updates get delayed because they are risky, then become more expensive because they were delayed.

Buyers may feel this as:

- "Routine upgrades keep becoming architecture projects."
- "We are afraid to run `npm audit fix` because it might break wallet flows."
- "No one knows which dependencies are dangerous."
- "The app works, but every change feels brittle."

### Lost Context And Handoff Risk

DAOhaus needed a system that future maintainers could understand without relying on historical contributors. This is common in DAO and protocol ecosystems, where projects outlive the original delivery team.

Buyers may feel this as:

- "Our real documentation is in old Discord threads."
- "The person who knows the system is overloaded or leaving."
- "A new vendor would need to rediscover everything."
- "We have no clear escalation boundary between routine maintenance and protocol-risk work."

### AI Tool Readiness Gap

Many teams want to use AI coding agents, but their systems are not ready. The repo structure, docs, issue flow, and review process do not give an agent enough stable context or enough governance.

Buyers may feel this as:

- "AI tools are useful in isolated moments but unreliable across the project."
- "The agent can write code, but it does not know our architecture."
- "We cannot let an agent touch production-affecting work."
- "Every session starts from zero."

## Outcomes To Sell

### A Maintainable Operating Surface

The buyer gets a clearer map of what is active, what is deprecated, who owns what, where systems are deployed, and which channels are used for support and maintenance.

This is the simplest promise: the system becomes easier to operate.

### Faster Maintainer Onboarding

The buyer gets architecture docs, repo inventories, access matrices, runbooks, local agent docs, and a handoff checklist. A new maintainer can start from structured context instead of institutional memory.

This is especially relevant for DAOs, foundations, and projects moving between vendors or working groups.

### Safer AI-Assisted Maintenance

The buyer gets AI leverage without pretending the agent is the operator. Agents can help with intake, triage, investigation, branch preparation, documentation, and routine maintenance reports. Humans remain responsible for decisions, review, merge, deployment, secrets, contracts, DNS, access, and incident escalation.

This makes human-in-the-loop governance a selling point rather than an apology.

### Reduced Support And Triage Drag

The buyer gets a more coherent intake path from Discord, GitHub, docs, or other support surfaces into an issue lifecycle. The goal is less time spent discovering context and more time spent deciding what to do.

### Stewardship Readiness

The buyer gets a transition packet that makes the project legible to future stewards: maintainers, vendors, working groups, foundation staff, or ecosystem funders.

This outcome may be the strongest for mature protocols whose main risk is not feature velocity, but continuity.

## Shape Of The Offering

### 1. Diagnostic Sprint

**Purpose:** Give the client a clear picture of maintenance risk and readiness before committing to implementation.

Likely deliverables:

- Active/deprecated/historical repo inventory.
- Public surface map: docs, apps, Discord, DNS, hosting, bots, support paths.
- Infrastructure and access matrix.
- Dependency and maintenance risk notes.
- AI readiness assessment.
- Recommended implementation roadmap.

Best for clients who know they have a problem but do not yet know scope or budget.

### 2. Maintenance Readiness Sprint

**Purpose:** Clean up the surface and produce the durable maintainer context.

Likely deliverables:

- Repo and public-surface cleanup.
- Architecture and system overview.
- Environment, deployment, verification, and debugging docs.
- Local `AGENT.md` or equivalent maintainer guidance near key code areas.
- Maintainer prompt for future AI coding sessions.
- SOP packet with access matrix, runbooks, known risks, and handoff checklist.

Best for clients preparing for handoff, vendor transition, or reduced-team operations.

### 3. Refactory Implementation

**Purpose:** Deploy a client-specific AI-assisted maintenance workflow.

Likely deliverables:

- Client-specific Refactory instance.
- Discord or support-channel intake.
- GitHub issue and branch workflow.
- Prism Memory and Knowledge setup.
- Codex Runtime configuration and smoke test.
- Human approval gates for triage, implementation, review, merge, and escalation.
- Operator walkthrough and first-use support.

Best for clients that want ongoing AI-assisted maintenance rather than a static handoff packet.

### 4. Ongoing Maintenance Partnership

**Purpose:** Keep the system alive after the initial readiness work.

Likely deliverables:

- Monthly triage and maintenance cadence.
- Dependency review and small upgrade support.
- Support intake review.
- Knowledge promotion from incidents and fixes into stable docs.
- Quarterly access, risk, and surface-area review.
- Optional release support or maintainer office hours.

Best for clients with live users but limited internal maintainer capacity.

## Service Packaging Options

### Conservative Package

Sell a fixed-scope readiness sprint first. Include the diagnostic, docs, SOP packet, and maintainer prompt. Offer Refactory deployment as an add-on.

Why this may work: it is easier for cautious clients to buy documentation, handoff, and risk reduction before committing to a live AI workflow.

### Full Package

Sell the DAOhaus-style bundle: modernization, surface cleanup, SOP packet, and Refactory deployment in one engagement.

Why this may work: it creates a stronger before-and-after transformation and gives Raid Guild more control over the quality of the final maintenance environment.

### Retainer-Led Package

Sell an initial setup sprint followed by a monthly maintenance retainer.

Why this may work: the value of the Refactory increases when it is part of a recurring operating rhythm. Memory and knowledge stay useful because they continue to be maintained.

## Positioning Notes

### Lead With Continuity, Not Novelty

The buyer's real fear is usually not "we are behind on AI." It is "this important system is getting harder to safely maintain." AI is part of the solution, but continuity is the buying reason.

### Keep The Human-In-The-Loop Frame

For production systems, "AI agent handles everything" creates distrust. DAOhaus gives Raid Guild better language:

- Agents do groundwork.
- Humans make decisions.
- GitHub remains the code review and merge source of truth.
- Runbooks name what is routine and what requires escalation.

### Treat Codebase Simplification As AI Enablement

DAOhaus showed that agent readiness starts before the agent. Cleaner repo structure, fewer aliases, colocated feature code, symptom-based debugging docs, and clear domain language all make AI sessions more useful.

This should be central in the sales story: Raid Guild is not just attaching AI to a messy system. It is shaping the system so AI and humans can maintain it together.

### The Access Matrix Is A Hidden High-Value Deliverable

Clients may undervalue this at the start, but the access matrix reveals the real maintenance model: who controls hosting, billing, DNS, graph deployments, RPC providers, wallets, Discord roles, and production secrets.

For stewardship handoff, this may be the most important artifact.

## What Else Is Relevant For Raid Guild

### This Could Become A Repeatable Guild Capability

The DAOhaus raid proves several capabilities at once:

- Legacy app modernization.
- Web3 dependency and infrastructure cleanup.
- Operational documentation.
- Community surface reduction.
- Human-governed AI workflow deployment.
- Maintainer transition support.

Packaged well, this is a distinct service line rather than a one-off story.

### It Fits Raid Guild's Existing Strengths

Raid Guild is credible here because the work requires more than one discipline. A good engagement needs product judgment, web3 engineering, DevOps, documentation, DAO operations, community context, and support workflow design.

That is hard for a generic AI automation vendor to deliver.

### It Creates Sales Material From Real Delivery

DAOhaus can support several future assets:

- Public case study.
- Service one-pager.
- Refactory workflow diagram.
- SOP packet table of contents.
- Before/after repo structure visual.
- Example issue lifecycle from Discord intake to agent branch to human review.
- Proposal template for similar clients.

### Metrics Should Be Captured Next Time

Future engagements should measure:

- Number of repos classified active/deprecated/historical.
- Number of docs created or updated.
- Number of Discord/support surfaces consolidated.
- Time for a new maintainer to find the right code path for a common symptom.
- Number of issues processed through the AI-assisted workflow.
- Dependency or toolchain versions before and after modernization.
- Access or ownership gaps discovered and resolved.

DAOhaus created the pattern, but stronger metrics will make the next sale easier.

## Open Questions

- What is the smallest package Raid Guild can sell that still creates a meaningful before-and-after?
- Should Refactory be positioned as a Raid Guild service, a Superprism product, or a joint delivery pattern?
- How much code modernization belongs in the default offer versus a separate technical workstream?
- Which intake channels should be supported first beyond Discord?
- What pricing model fits: fixed sprint, phased package, retainer, or funder-sponsored maintenance program?
- Which claims from the DAOhaus work are public-safe, and which should stay internal?
- Who owns ongoing operation of the Refactory instance after handoff?

## What This Means For RG

The DAOhaus raid points toward a credible, sellable service: AI-assisted maintenance readiness for mature web3 systems.

The strongest offer is not "we install an agent." It is "we help important systems become maintainable again, then give maintainers AI leverage inside a governed workflow."

That distinction matters. It lets Raid Guild speak to real buyer pain: continuity, handoff, reduced maintainer load, safer operations, and stewardship of live infrastructure. The AI component becomes more believable because it is grounded in cleanup, documentation, SOPs, and explicit human review.

## Source Notes

This summary draws from:

- `raid-reports/daohaus-hauskeeper.md`
- `outputs/ai-assisted-maintenance-service-one-pager.md`
- `summaries/2026-05-17_ai-assisted-maintenance-system.md`
- `summaries/2026-05-17_maintenance-sops-playbooks.md`
- `ideas/raid_report_product_scope.md`
- `AGENT.md`

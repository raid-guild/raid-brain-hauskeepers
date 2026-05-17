# DAOhaus Hauskeeper Raid Recap And Case Study Seed

## Working Positioning

The DAOhaus Hauskeeper raid is a strong internal case study for how Raid Guild can turn exploratory member-led AI work into a client-funded maintenance engagement, then turn that engagement back into reusable service infrastructure.

The simplest story:

> A cohort spike became a client engagement. A client engagement became a hardened operating model. The operating model became the beginning of a repeatable AI-assisted maintenance service.

This document is internal-facing for now, but it is structured so pieces can later become public case study content, proposal language, sales collateral, or a Raid Guild learning post.

## Origin Story

A few months before the DAOhaus raid, Raid Guild members piloted a project in the Raid Guild cohort called Dark Factory. The project was a spike on AI workflow automation: how autonomous and semi-autonomous development tools could help with software maintenance, knowledge capture, issue triage, and recurring operational work.

The spike was not just theoretical. Members saw enough promise to ask a sharper question: could this become a real maintenance offering for a live client with actual production risk?

DAOhaus was a natural proving ground. The protocol and product suite had real usage, long history, and active value, but also the kind of accumulated complexity that makes maintenance hard:

- Years of repo, package, and dependency history.
- Public surfaces spread across apps, docs, Discord, DNS, and GitHub.
- Operational knowledge held by a small number of contributors.
- A need to identify and support protocol maintainers without assuming a large standing team.
- A desire to use AI-assisted workflows without giving production control to an unbounded agent.

Raid Guild crafted the engagement around this need: modernize DAOhaus, reduce its maintenance surface area, document the system for human and AI operators, and deploy a human-in-the-loop AI maintenance workflow that could help future maintainers do more with less.

The raid also hardened member-side experimentation. Dark Factory ideas, related Superprism work, and the needs surfaced by DAOhaus converged into what became the Superprism Refactory: a deployable maintenance control plane that combines Codex execution, Prism Memory and Knowledge, Discord intake, GitHub review, Railway deployment context, and human approval gates.

## What DAOhaus Bought

DAOhaus funded a fixed-scope infrastructure modernization and AI-assisted maintenance sprint executed by Raid Guild. The work was organized into five major workstreams.

### 1. Codebase Consolidation And Modernization

Raid Guild rebuilt the DAOhaus admin app as a standalone Vite, React, and TypeScript application, extracting it from the prior NX/Webpack/Babel monorepo. Internal `@daohaus/*` packages were inlined as local source, dependency layers were simplified, and major dependencies were modernized, including React, TanStack Query, React Router, wagmi, viem, and RainbowKit.

The repo was then reorganized around a cleaner `app/`, `features/`, and `lib/` architecture. This reduced the path alias surface, removed duplicate namespaces, colocated feature-specific code, and made the codebase easier for both humans and AI agents to navigate.

### 2. Architecture And Agent-Ready Documentation

The raid produced a layered documentation system:

- A root `README.md` as the front door.
- System architecture, environment, verification, domain glossary, and debugging docs.
- Local `AGENT.md` files colocated with major code areas.
- A reusable LLM maintainer prompt that encodes reading order, ownership boundaries, and fix-reporting discipline.

This was not generic documentation. It was documentation designed for the way maintenance actually happens: a maintainer or coding agent starts with a symptom, finds the likely files, understands the local ownership rules, makes a bounded change, and reports what was verified.

### 3. Reduced Community And Repository Surface Area

DAOhaus had accumulated many public and maintainer-facing surfaces over time. The raid mapped active, deprecated, and historical repositories; clarified canonical GitHub surfaces; cleaned public docs; reviewed DNS and hosting records; and consolidated Discord channels around a smaller active operating model.

The outcome was a smaller, clearer project surface. Users know where to ask for help. Maintainers know which repos and apps are active. AI agents have fewer false paths to chase.

### 4. AI-Assisted Maintenance System

The raid deployed a DAOhaus-specific instance of the Superprism Refactory platform. The stack connects:

- Discord and Refactory intake.
- A control plane for requests, tasks, workflows, artifacts, and agent session state.
- Codex Runtime for agent execution.
- Prism Memory and Prism Knowledge for operational history and curated reference material.
- GitHub for branch, pull request, review, and merge state.
- Railway for deployed service context and verification.

The system is intentionally human-in-the-loop. The agent does not run DAOhaus. It helps with triage, investigation, branch preparation, implementation assistance, reporting, and maintenance context. Humans approve status transitions, branches, pull requests, merges, incidents, and production-affecting changes.

### 5. Maintenance SOPs And Transition Readiness Packet

The raid produced an eight-document DAOhaus Maintenance and Transition Readiness Packet:

- Transition overview.
- System architecture.
- Repository and application inventory.
- Infrastructure, access, and dependencies.
- Operational runbooks.
- AI-assisted maintenance workflows.
- Known risks and open gaps.
- Stewardship handoff checklist.

The packet makes maintenance responsibilities explicit. It separates routine maintainer work from exceptional changes such as contract upgrades, DNS or registrar changes, The Graph billing and multisig changes, production secrets, and access-control updates.

## What Was Delivered

At a practical level, the raid delivered:

- A simplified, independently deployable DAOhaus admin app.
- Modernized dependencies and wallet stack.
- A clearer repo structure optimized for human and AI maintainers.
- LLM-optimized documentation and local agent guidance.
- A symptom-based debugging guide.
- A reusable AI maintainer prompt.
- A mapped and reduced GitHub, docs, DNS, and Discord surface.
- A deployed AI-assisted maintenance system on the Superprism Refactory stack.
- A human-in-the-loop issue lifecycle from intake through review.
- Memory and Knowledge systems for preserving operational context.
- Complete maintenance SOPs and handoff materials.
- A reusable packet structure and platform pattern for future Raid Guild engagements.

## Why This Mattered For DAOhaus

DAOhaus did not just need code cleanup. It needed a maintainable operating model for mature protocol software.

The raid reduced maintenance risk in several ways:

- Fewer active systems to understand.
- Clearer ownership boundaries.
- Lower onboarding cost for new maintainers.
- Less dependency and package indirection.
- Better documentation at the exact places maintainers and agents work.
- Explicit escalation boundaries for risky operational changes.
- A structured path for AI assistance without surrendering human judgment.

The most important maintenance shift was from implicit knowledge to durable operating context. Before the raid, much of the system depended on historical familiarity. After the raid, a new maintainer can start from the repo map, SOP packet, access matrix, debugging guide, and Refactory workflow.

## How The Raid Hardened The Refactory

DAOhaus gave the Dark Factory and Superprism ideas a real test environment.

The engagement forced the platform to answer operational questions that do not always appear in a prototype:

- What is the system of record for a request?
- Which state belongs in GitHub, Refactory, Railway, or Prism Memory?
- How does an agent know what context is stable enough to trust?
- Where must a human approve the next step?
- What should be memory, and what should be knowledge?
- Which setup steps are truly reusable, and which remain instance-specific?
- How does a client-specific maintenance system get deployed without leaking template state?

The resulting Superprism Refactory pattern is more concrete because of this raid. It is no longer just an automation concept. It is a seven-service Railway stack with a control plane, Codex runtime, memory and knowledge services, Discord adapter, and recurring sync/indexing jobs. Each new client can receive its own instance with its own secrets, volumes, target repos, auth, Discord configuration, and cron schedules.

DAOhaus also surfaced the honest friction points. Codex device auth still requires a manual operator step. Runtime services need clear internal and admin API boundaries. Cron setup and Discord sync require post-deploy checks. Those learnings make the future offering stronger because they turn hidden operational risk into a repeatable setup checklist.

## Key Learnings

### Codebase simplification is AI readiness

AI agents work better when repo structure is obvious. The `app/`, `features/`, and `lib/` split, shallow folders, feature colocation, and reduced alias surface were not just cleanup. They made the codebase easier for agents to inspect, edit, and reason about.

### Documentation should be written for repeated agent use

Docs for AI-assisted maintenance are not only for humans reading once. Agents read docs repeatedly. Short, colocated `AGENT.md` files, explicit ownership boundaries, symptom-driven debugging docs, and copyable maintainer prompts all compound across future sessions.

### Human-in-the-loop is a feature

The strongest pitch is not "fully automated maintenance." It is "the agent handles groundwork; humans handle decisions." This is more accurate, less risky, and more persuasive to clients who operate production systems.

### Memory and Knowledge need separate lanes

Operational history and curated reference material should not be collapsed into one pile. Memory records what happened. Knowledge records how things work. The promotion path from raw event to artifact to memory index to curated knowledge doc is a reusable pattern.

### Surface-area reduction belongs in maintenance readiness

Legacy projects do not only accumulate code debt. They accumulate Discord channels, old docs, stale DNS records, deprecated repos, abandoned packages, and unclear support paths. Reducing that surface is part of making the project maintainable.

### SOPs should name dangerous operations

Specific anti-patterns are more useful than generic caution. "Do not run `npm audit fix --force`" with a concrete reason is better than "be careful with dependencies." The same applies to `wagmi` major upgrades, subgraph schema changes, and access-control work.

### Access matrices should be produced early

The access matrix is one of the highest-value handoff artifacts. It reveals single points of failure and tells a maintainer who controls GitHub, Railway, DNS, The Graph, RPC providers, Discord bot credentials, and related systems.

## Potential Public Case Study Angles

Future public-facing content could emphasize different narratives depending on the audience:

- **Cohort to client:** Raid Guild members explored AI automation in Dark Factory, recognized client value, and converted the learning into a real DAOhaus engagement.
- **Legacy protocol sustainability:** DAOhaus used Raid Guild to turn accumulated software and operational complexity into a maintainable system.
- **Human-centered AI maintenance:** The Refactory helps one maintainer act with more leverage while preserving human review over production-affecting decisions.
- **Productized raid learning:** The engagement did not end as a one-off. It produced reusable templates, SOP packet structures, prompts, and platform lessons.
- **Agent-ready software modernization:** The best AI maintenance work started before automation: simplifying the repo, documenting boundaries, and reducing public surface area.

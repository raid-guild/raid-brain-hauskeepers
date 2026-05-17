# Learnings

Accumulated learnings from the DAOhaus raid. Each entry includes the observation, concrete evidence, and why it matters for Raid Guild or future clients.

Maintained via Workflow 2 in `CLAUDE.md`. Append new entries — don't rewrite existing ones.

---

## Codebase Structure for AI Maintainability

### Structure codebases for intent, not history

_First captured: April 2026_

DAOhaus had a decade of accumulated structure that made sense historically but was hard for both humans and AI agents to navigate. We reorganized around `app/` / `features/` / `lib/` and reduced the alias surface from ~12 competing paths to 3 stable roots (`@/lib/*`, `@/app/*`, `@/features/*`).

AI agents navigate by pattern-matching. A flat, semantically clear structure reduces the cognitive overhead (and token cost) of every agent operation. This is a concrete selling point for the AI maintenance offering: the codebase simplification sprint _is_ the AI readiness sprint.

---

### Keep directories shallow and feature-colocated

_First captured: April 2026_

The original DAOhaus repo had shared folders with dozens of files. Finding anything required knowing the history. We moved feature-specific utilities, hooks, and components into their feature folders — only truly shared code stays in `lib/`.

An agent asked to work on the proposal feature can read `features/proposal/` and have everything it needs. No cross-repo hunting. Reduces context window usage per agent session.

---

### Write documentation for LLMs, not just humans

_First captured: April 2026 — expanded April 2026_

Most documentation is written for humans to read once. AI agents re-read docs on every session. Practices that improved agent output: consistent heading structure, explicit statement of assumptions and constraints, documenting "why" decisions were made (not just what), keeping docs colocated with the code they describe.

LLMs reason over text. Well-structured, explicit documentation measurably improves the quality of AI agent output. This is a service RG can deliver — LLM-optimized documentation is a distinct deliverable, not just a side effect of writing good docs.

In practice, the docs layer that delivered the most signal per word was the local `AGENT.md` file — short, scoped to one folder, answering: what belongs here, what doesn't, where to look next. Ten of these files now cover the major feature and library areas in the DAOhaus repo. The format is repeatable across any project with a meaningful folder structure.

---

### Colocated docs outperform remote wikis for AI agents

_First captured: April 2026_

We placed `AGENT.md` files directly inside the folders they describe rather than consolidating everything into a central wiki or `docs/` directory. During editing, an agent reading nearby files naturally encounters the relevant guide. A remote wiki requires a deliberate lookup that agents frequently skip.

For clients who already have a Notion or Confluence wiki, the pitch is direct: the wiki describes the project, `AGENT.md` files guide the agent while it works. Both can coexist; they serve different moments. Colocated docs also go stale more slowly because the cost of updating them is low — they live in the same PR as the code change.

---

### A reusable LLM system prompt is a first-class deliverable

_First captured: April 2026_

We produced a copyable system/developer prompt block (`docs/006_prompt_for_llm_maintainer.md`) that encodes reading order, layer ownership, and fix-reporting discipline for the DAOhaus repo. Any agent or contractor dropped into the codebase can use it immediately without a separate orientation session.

This prompt template is distinct from documentation — it is operational instruction, not reference material. It is the thing a client pastes into their AI coding tool to get consistent, on-pattern behavior. RG can offer it as a named deliverable ("AI onboarding prompt") in maintenance setup engagements. It is low cost to produce and high value to the client because it compounds: every future agent session benefits from it.

---

### Symptom-based debugging docs are more useful than architecture docs during active maintenance

_First captured: April 2026_

We created `docs/DEBUGGING.md` as a symptom-to-file mapping: "proposal action state is wrong → start here," "Safe balances missing → check this hook." This is structurally different from `docs/ARCHITECTURE.md`, which explains how the system works.

During a maintenance engagement, bugs arrive as user reports, not architecture questions. A debugging guide that maps real symptoms to likely code paths reduces the time from report to first relevant file. In testing against the DAOhaus repo, a new engineer with a bug report could identify an initial file path in under a minute using the guide. Architecture docs explain the happy path; debugging docs are used when the happy path has failed.

---

### Build documentation in two passes: ship fast, then gap-analyze

_First captured: April 2026_

The first pass produced ten `AGENT.md` files and a root-level architecture doc quickly, focusing on the most stable and high-value folders. A second pass — done as a fresh-eyes review — caught stale doc indexes, non-portable Markdown links, and five areas lacking coverage that would have quietly degraded agent usefulness over time.

The two-pass approach avoids two failure modes: spending too long on documentation before it has been tested in practice, and shipping docs that deteriorate immediately because no one audited them after the first rush. For future engagements, budget the second pass explicitly — it is not overhead, it is where the quality lands.

---

## Dependency Modernization

### Bundle major upgrades into a single structured sprint

_First captured: April 2026_

Clients often have many outdated dependencies and resist upgrading because each change feels risky. We ran wagmi v1→v2, react-query v3→v5, react-router v6→v7, React 18→19, and replaced the bespoke wallet layer with RainbowKit — all in one structured sprint.

The overhead of upgrading is mostly in understanding the system, not in the changes themselves. Bundling pays that cost once. Incremental upgrades pay it repeatedly. This framing helps clients get comfortable with the sprint model.

---

### Inline packages as local source when possible

_First captured: April 2026_

The DAOhaus monorepo had many `@daohaus/*` internal packages that added indirection without value (only consumed by one app). We inlined them as local source under `src/lib/`.

Eliminates an entire layer of build complexity. Makes the dependency graph obvious. Makes AI agents' lives much simpler — no jumping between package repos. For clients with internal monorepos, this is often one of the highest-leverage simplifications available.

---

## Order of Operations

### Do codebase simplification before setting up AI tooling

_First captured: April 2026_

AI agents are more effective on clean, well-structured codebases. Setting up agentic tooling on a messy codebase means the agent inherits all the confusion. The right order: simplify and document first, then automate.

For future client proposals, this has scoping implications. The codebase modernization sprint and the AI maintenance setup are distinct phases — and the former is a prerequisite for the latter to deliver full value.

---

## Anti-Patterns to Avoid

| Anti-pattern                                  | What went wrong                                                                               | Better approach                                                           |
| --------------------------------------------- | --------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Running `npm audit fix --force`               | Produces unexpected breaking upgrades, especially in wallet stacks                            | Audit manually, group changes by risk tier, validate each tier separately |
| Treating `wagmi 2.x → 3.x` as a routine patch | Major wallet-stack upgrades affect connector behavior, RainbowKit integration, and Safe flows | Treat as a dedicated wallet integration project with regression testing   |
| Removing or renaming subgraph schema fields as a patch | Fields removed from a subgraph schema silently break apps still querying the old field       | Prefer additive schema changes; audit app queries before any field removal or type change |

---

## AI Maintenance Platform Design

### The agentic maintenance platform is a deployable template, not a bespoke build

_First captured: May 2026_

The Prism Railway Template packages the seven-service agentic maintenance stack (site/API, codex-runtime, prism-memory, discord-adapter, memory-cron, knowledge-cron, discord-sync-cron) into a single Railway template deploy. Each client instance gets its own project, secrets, volumes, and cron configuration — none of which bleeds back into the template.

This changes the economics of the offering. The first engagement bears the setup cost. Subsequent engagements start from a working template and configure rather than build. The template is RG's productized infrastructure for AI-assisted maintenance and should be treated as a maintained internal asset, not a one-off per client.

---

### Human-in-the-loop is a sales feature, not a limitation

_First captured: May 2026_

The DAOhaus maintenance system does not replace the human maintainer — it reduces the groundwork (triage, investigation, branch preparation, reporting) so the maintainer's time goes to decisions. Every gate where status advances requires explicit human confirmation: intake to triage, triage to implementation, branch to review, review to merge.

Framing the system as "the agent handles groundwork, you handle decisions" is more accurate and more persuasive than "fully automated maintenance." Clients who have been burned by runaway automation respond better to a human-in-the-loop architecture. This framing should be the default pitch for AI maintenance setup engagements.

---

### Memory/knowledge split should be a standard setup deliverable

_First captured: May 2026_

Prism distinguishes Memory (time-based operational record — transcripts, digests, agent outputs, activity history) from Knowledge (curated retrievable docs — SOPs, runbooks, architecture notes, stable summaries). The split has a defined promotion path: raw event → artifact → memory index → curated knowledge doc.

Without this distinction, operational noise pollutes the reference layer and future agent sessions surface irrelevant history when querying for "how does this work." For RG engagements, setting up this split early is low cost and compounds: every session benefits from a clean knowledge layer. It should be a line item in the engagement setup checklist, not an afterthought.

---

### Codex device auth is the primary friction point in agentic Railway deployments

_First captured: May 2026_

Codex device auth is a one-time manual step: SSH into the `codex-runtime` service, run the auth flow with `CODEX_HOME` pointing at the mounted volume, and complete the device auth. This step cannot be scripted into a Railway template deploy because it writes account auth into the volume through an interactive device-auth flow.

In practice, this means every new Prism instance requires a human operator on the keyboard for roughly 5–15 minutes after deploy. Budget for it, document it explicitly in the handoff, and do not assume it is automated. Future template iterations should front-load this step in the bring-up checklist rather than letting operators discover it mid-setup.

---

### Two distinct API surfaces prevent agentic misconfiguration

_First captured: May 2026_

The Prism site/API exposes `/admin/*` routes (require an authenticated browser session) and `/agent/*` routes (require a service token via `x-service-token`). Using a service token against an `/admin/*` route returns a `401` that looks like a permissions error but is actually a wrong-surface error.

Runtime agents should always use `PRISM_AGENT_API_BASE_URL` and `PRISM_AGENT_SERVICE_TOKEN`, not admin session credentials. This two-surface separation is a pattern worth standardizing in any multi-service agentic platform RG builds: clear internal and external API boundaries reduce misconfiguration and make auth failures diagnosable.

---

## SOP and Playbook Design

### The 8-document SOP packet structure is reusable across legacy web3 maintenance engagements

_First captured: May 2026_

The DAOhaus Maintenance & Transition Readiness Packet is organized into: overview, system architecture, repo/app inventory, infrastructure/access/dependencies, operational runbooks, AI-assisted workflows, known risks and open items, and stewardship handoff checklist. Each section is standalone — a maintainer can read one without the others.

This structure covers what any legacy web3 maintenance engagement needs to document. RG can template it and adapt section contents to a new client without restructuring. The inventory, access matrix, and risk callout sections are the most project-specific; the runbook and AI workflow sections are the most portable.

---

### Named anti-patterns outperform generic caution in operational runbooks

_First captured: May 2026_

The DAOhaus runbooks name specific dangerous operations with reasons: "Don't run `npm audit fix --force` — it produces silent breaking upgrades in wallet stacks." "Don't treat `wagmi` major upgrades as routine patches — they affect connector behavior, RainbowKit integration, and Safe flows." "Don't remove subgraph schema fields without auditing app queries first."

Generic guidance ("review dependencies carefully," "be cautious with schema changes") is ignored under maintenance pressure. Specific, named anti-patterns with concrete failure modes stay with the operator. For future SOP engagements, surface project-specific anti-patterns during the investigation phase and encode them explicitly — they are the most durable content in the runbook.

---

### The access matrix is the highest-value section for handoff — produce it early

_First captured: May 2026_

An access matrix maps each infrastructure system to its current holders, access level, and how access is granted or revoked. For DAOhaus this covers GitHub org and repos, Railway, DNS, The Graph multisig, Alchemy, WalletConnect, Sequence, and Discord bot credentials. Without this document, a new maintainer has no reliable way to know who holds what or what breaks if that person is unavailable.

Generic SOPs are reproducible from first principles. An access matrix for a specific client is not — it requires discovery work that is hardest to do during a crisis. RG should produce the access matrix in the first week of a maintenance engagement, not as a handoff deliverable. It surfaces single points of failure early and gives the client something immediately actionable.

---

### Explicit scope boundaries prevent both over-reach and under-reaction

_First captured: May 2026_

The DAOhaus SOP packet draws an explicit line around what is "not routine maintainer work": contract upgrades, DNS and registrar changes, The Graph multisig or billing changes, production secrets, and access-control changes. These are not mentioned once and assumed understood — they appear at the start of the operating model section and in the exceptional change runbook.

Without explicit boundaries, a new maintainer may attempt changes outside their lane (over-reach) or freeze during an incident because they're unsure whether a fix is in scope (under-reaction). Both failure modes are avoidable. For future SOP engagements, scope boundary callouts should be a named section, not implied by what the runbooks cover.

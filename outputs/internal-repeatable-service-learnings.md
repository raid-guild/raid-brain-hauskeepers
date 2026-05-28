# Internal Learnings: Repeating The DAOhaus Raid As A Service Offering

## Draft Status

Internal Raid Guild strategy draft. This is not public copy. It includes delivery patterns, packaging assumptions, operational friction, and open service-design questions that should inform future proposals and delivery planning.

## Purpose

The DAOhaus Hauskeeper raid proved a repeatable service pattern:

> Raid Guild can help mature web3 teams move from legacy complexity to progressive automation by simplifying the operating surface, documenting durable context, establishing human approval gates, and deploying AI-assisted workflows that help maintainers do more without surrendering production judgment.

The public story should stay crisp: progressive automation, human-governed AI, clearer maintenance foundations. Internally, the value is more specific. DAOhaus showed what Raid Guild can package, what artifacts should become templates, what risks need to be scoped early, and where delivery still depends on experienced operators.

## What DAOhaus Proved

DAOhaus proved that AI-assisted maintenance is not a standalone automation install. It is a combined modernization, documentation, operations, and workflow engagement.

The raid proved five connected capabilities:

- **Legacy app modernization:** Raid Guild can simplify a mature web3 app surface, reduce package indirection, modernize dependency layers, and make the active codebase easier for future maintainers and agents to inspect.
- **Agent-ready documentation:** Raid Guild can produce docs for repeated use by humans and AI agents, including architecture context, debugging guidance, local maintainer instructions, and reusable agent prompts.
- **Surface-area reduction:** Raid Guild can map and clarify active, deprecated, and historical project surfaces across GitHub, docs, Discord, DNS, hosting, and support paths.
- **Human-governed AI workflow deployment:** Raid Guild can deploy a client-specific Refactory instance that supports intake, triage, context retrieval, branch preparation, implementation help, reporting, memory, knowledge, and review.
- **Transition readiness:** Raid Guild can create SOPs, access matrices, operational runbooks, risk callouts, and stewardship handoff materials that make a mature protocol easier to maintain after the engagement.

The strongest internal takeaway is this:

> Codebase simplification and operating-model cleanup are not prep work around the AI offer. They are the AI offer.

Agents perform better when the repo has a clear shape, docs live near the work, support intake has a defined path, and humans know which decisions must stay gated.

## Best-Fit Clients

This service is strongest for teams with live software, real users, and too much operational knowledge trapped in old systems.

### Mature Web3 Protocols

These teams still have active infrastructure, but the people who originally understood the whole system may have moved on, scaled back, or become bottlenecks.

Good signals:

- Active users or treasury.
- Aging frontends, docs, bots, subgraphs, or support channels.
- Reduced core-team capacity.
- Unclear ownership across repos, infra, billing, and credentials.
- Desire to use AI tools, but concern that the system is too messy for safe delegation.

### DAOs Preparing For Stewardship Transition

These clients need to hand responsibility to a maintainer, vendor, foundation, working group, or community steward.

Good signals:

- A few historical contributors hold most operating context.
- No current access matrix.
- Support paths are unclear.
- The DAO needs continuity more than new feature velocity.

### Lean Product Teams With Large Maintenance Surfaces

These teams may not call themselves legacy, but they feel the same pain: too many apps, packages, docs, channels, and dependencies for the number of active maintainers.

Good signals:

- Recurring support and bug triage crowd out product work.
- Dependency upgrades feel risky.
- AI tools are useful in isolated moments but unreliable across the project.

### Ecosystem Funders And Public-Goods Stewards

These buyers think at the portfolio level. They need useful infrastructure to stay available without permanently funding large standing teams.

Good signals:

- Multiple funded projects need handoff or maintenance.
- The funder needs a readiness score or gap report before allocating follow-on funding.
- There is a need to compare maintenance risk across projects.

## Recommended Package Shapes

### 1. Diagnostic Sprint

Purpose: give the client a clear picture of maintenance risk and implementation scope before larger work begins.

Deliverables:

- Active, deprecated, and historical repo inventory.
- Public surface map: apps, docs, Discord, DNS, hosting, bots, support paths.
- Infrastructure, billing, ownership, and access matrix.
- Dependency and maintenance risk notes.
- AI readiness assessment.
- Recommended implementation roadmap.

Use when the client knows something is wrong but does not yet know the budget, scope, or risk profile.

### 2. Maintenance Readiness Sprint

Purpose: clean the operating surface and produce durable maintainer context.

Deliverables:

- Repo and public-surface cleanup.
- Architecture and system overview.
- Environment, deployment, verification, and debugging docs.
- Local maintainer guidance near important code areas.
- Copyable AI maintainer prompt.
- SOP packet with access matrix, runbooks, known risks, and handoff checklist.

Use when the client is preparing for handoff, vendor transition, reduced-team operations, or future AI-assisted workflows.

### 3. Refactory Implementation

Purpose: deploy a client-specific AI-assisted maintenance workflow.

Deliverables:

- Client-specific Refactory instance.
- Discord or support-channel intake.
- GitHub issue, branch, review, and merge flow.
- Memory and Knowledge setup.
- Codex Runtime configuration and smoke test.
- Human approval gates for triage, implementation, review, merge, and escalation.
- Operator walkthrough and first-use support.

Use when the client wants an ongoing workflow, not only a static handoff packet.

### 4. Ongoing Maintenance Partnership

Purpose: keep the system alive after setup.

Deliverables:

- Monthly triage and maintenance cadence.
- Dependency review and small upgrade support.
- Support intake review.
- Knowledge promotion from fixes and incidents into stable docs.
- Quarterly access, risk, and surface-area review.
- Optional release support or maintainer office hours.

Use when the client has live users but limited internal maintainer capacity.

## Recommended Default Sales Path

The safest commercial path is phased:

1. Sell a **Diagnostic Sprint** to map risk and scope.
2. Convert into a **Maintenance Readiness Sprint** for cleanup, docs, and SOPs.
3. Add **Refactory Implementation** once the operating surface has enough shape.
4. Offer **Ongoing Maintenance Partnership** as the continuity layer.

The full DAOhaus-style bundle is powerful, but it requires a client that already trusts the direction and has budget for modernization plus workflow deployment. For colder prospects, a diagnostic first step is easier to buy and gives Raid Guild a better basis for scoping.

## Standard Delivery Phases

### Phase 1: Discovery And Surface Map

Inputs needed:

- Repo/org access.
- Docs and site links.
- Discord/support channel map.
- Hosting, DNS, deployment, indexer, and provider list.
- Known owners and access holders.
- Existing proposals, scopes, and architecture notes.

Outputs:

- Active/deprecated/historical system map.
- Access and ownership matrix.
- Known risk list.
- Public-safe and internal-sensitive claim boundaries.

Produce the access matrix early. It reveals single points of failure before the team is deep in implementation.

### Phase 2: Codebase And Repo Readiness

Inputs needed:

- Active app/repo list.
- Dependency and toolchain state.
- Known bugs or support symptoms.
- Deployment and verification paths.

Outputs:

- Simplified repo structure where scoped.
- Reduced package, alias, and dependency indirection.
- Modernized dependencies where appropriate.
- Symptom-based debugging guide.
- Verification checklist.

Do this before leaning hard on AI tooling. A confusing repo creates confusing agent sessions.

### Phase 3: Agent-Ready Docs And SOP Packet

Outputs:

- Root documentation map.
- Architecture overview.
- Environment and deployment docs.
- Debugging guide.
- Domain glossary.
- Local maintainer guidance.
- AI maintainer prompt.
- Eight-document SOP and transition readiness packet.

The reusable packet structure:

- Transition readiness overview.
- System overview and architecture.
- Repository and application inventory.
- Infrastructure, access, and dependencies.
- Maintenance SOPs and operational runbooks.
- AI-assisted maintenance workflows.
- Known risks and open maintenance gaps.
- Stewardship handoff checklist.

### Phase 4: Refactory Deployment

Outputs:

- Client-specific Refactory instance.
- Intake adapter configuration.
- Memory and Knowledge lanes.
- GitHub workflow integration.
- Human approval gates.
- Smoke-tested agent runtime.
- Operator walkthrough.

Standard lifecycle:

```text
Inbox -> Triaging -> Ready for Agent -> Working -> Awaiting Review -> Approved
```

Revision loop:

```text
Awaiting Review -> Changes Requested -> Working -> Awaiting Review
```

Human gates should remain explicit at intake, implementation, branch acceptance, pull request review, merge, incident escalation, and production configuration changes.

### Phase 5: Handoff And First Operating Cycle

Outputs:

- Maintainer walkthrough.
- First intake/triage run.
- Knowledge promotion check.
- Open risks and next actions.
- Ownership decision for ongoing Refactory operation.

Do not treat deployment as the end. The first operating cycle is where workflow gaps become visible.

## Standard Artifacts To Template

Raid Guild should create reusable templates for:

- Diagnostic report.
- Active/deprecated/historical repo inventory.
- Public surface map.
- Infrastructure and access matrix.
- Dependency risk table.
- Architecture overview.
- Symptom-based debugging guide.
- Local maintainer guidance file.
- AI maintainer prompt.
- Eight-document SOP packet.
- Refactory setup checklist.
- Human approval gate checklist.
- Memory/Knowledge promotion guide.
- Handoff checklist.
- Public case study intake questionnaire.

The access matrix, SOP packet, maintainer prompt, and Refactory setup checklist are the highest priority templates.

## Risks And Constraints

### Public Claims Need Review

Avoid unsupported metrics, implied client testimonials, or language that makes the client sound broken or rescued. Public framing should be continuity, progressive automation, and stronger stewardship.

### AI Scope Must Stay Bounded

The default claim is not autonomous maintenance. The default claim is:

> The agent handles groundwork; humans handle decisions.

Contract upgrades, DNS and registrar changes, Graph multisig or billing changes, production secrets, access-control changes, and incident authority should remain outside routine AI-assisted flow unless explicitly scoped.

### Refactory Setup Still Has Operator Friction

Codex device auth is a manual post-deploy step. It requires a human operator to complete auth against the mounted runtime volume. Budget for it and document it in every bring-up checklist.

Future deployments also need post-deploy checks for cron jobs, Discord sync, internal/admin API boundaries, secrets, volumes, and target repo configuration.

### Code Modernization Scope Can Expand Quickly

Dependency work can become architecture work, especially in wallet stacks, indexers, and web3 provider layers. Scope modernization by risk tier and name anti-patterns early.

Examples from DAOhaus:

- Do not run `npm audit fix --force` as routine remediation.
- Treat major wallet-stack upgrades as dedicated integration projects.
- Prefer additive subgraph schema changes unless app queries have been audited.

### Documentation Needs A Second Pass

First-pass docs capture coverage. Second-pass docs catch gaps, stale indexes, bad links, and unclear ownership boundaries. Budget for both.

## Metrics To Capture Next Time

DAOhaus produced the pattern, but future sales will be stronger with measured before/after evidence.

Track:

- Number of repos classified active, deprecated, and historical.
- Number of docs created or updated.
- Number of support or Discord surfaces consolidated.
- Dependency and toolchain versions before and after modernization.
- Time for a new maintainer to identify likely files for a common symptom.
- Number of issues processed through the AI-assisted workflow.
- Number of access or ownership gaps found and resolved.
- Number of knowledge artifacts promoted from operational activity.

Capture metrics during delivery, not after the fact.

## Public-Safe Sales Narrative

Use this as the external story:

> Mature protocols do not need blind autonomy. They need a credible road to progressive automation. Raid Guild helps teams clarify their operating surface, document durable context, modernize what blocks maintenance, and deploy AI-assisted workflows where agents handle groundwork and humans approve meaningful decisions.

Short version:

> Legacy complexity -> clearer systems -> governed AI assistance -> better maintainer leverage.

Avoid:

- "Fully autonomous maintainer."
- "We rescued the protocol."
- Unsupported speed, cost, or reliability claims.
- Detailed access gaps unless the client approves them.

## Open Decisions

- What is the smallest sellable package that still creates meaningful before/after value?
- Should Refactory be positioned as a Raid Guild service component, a Superprism product, or a joint delivery pattern?
- How much code modernization belongs in the default package versus a separate technical workstream?
- Which intake channels beyond Discord should be supported first?
- Who owns ongoing operation of the Refactory instance after handoff?
- What pricing model fits best: fixed sprint, phased package, retainer, or funder-sponsored maintenance program?
- Who inside Raid Guild owns the service line and template maintenance?
- Which metrics become mandatory for every future engagement?

## Recommended Next Actions

- Approve the phased package model or choose an alternate default.
- Identify one owner for the service offer and one owner for Refactory deployment readiness.
- Build reusable templates for the SOP packet, access matrix, maintainer prompt, diagnostic report, and Refactory setup checklist.
- Create a public service page from the approved case study language.
- Identify 3-5 likely next pilot clients or ecosystem funders.
- Define the minimum metrics captured during every future engagement.
- Decide how Raid Guild and Superprism should co-brand the offer.


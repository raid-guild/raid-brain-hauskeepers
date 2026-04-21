# Architecture & Documentation Phase Summary

**Date:** April 21, 2026
**Source docs:** `docs/005_agent_doc_plan.md`, `docs/006_prompt_for_llm_maintainer.md`, `docs/007_repo_docs_overview.md`

---

## What We Did

This phase focused on making the HAUS Admin repo navigable for both human developers and LLM coding agents. The work proceeded in two passes: an initial rollout of local navigation docs, then a gap analysis and expansion plan to improve coverage and discoverability.

### Deliverables Produced

**High-level docs (repo root and `docs/`):**

- `README.md` — updated as the front door: setup basics, project shape, and a full docs map
- `docs/ARCHITECTURE.md` — system-level map covering boot flow, routing, data flow, transaction flow, and dependency boundaries
- `docs/DEBUGGING.md` — symptom-to-file recipes for common bug reports (DAO route not loading, proposal data wrong, summon tx fails, Safe balances missing, etc.)
- `docs/DOMAIN_GLOSSARY.md` — definitions for project vocabulary: DAO, Baal, Safe, summon, ragequit, shares, loot, shaman, form lego, transaction lego
- `docs/ENVIRONMENT.md` — env var documentation by purpose and observable failure mode
- `docs/VERIFICATION.md` — commands by change type, with expectations for what to run and how to report residual risk

**Local navigation docs (`AGENT.md` files):**

- `src/AGENT.md` — ownership rules for `app`, `features`, `lib`; alias guidance; placement rules for new files
- `src/app/AGENT.md` — route/layout/hooks/components distinctions; shell vs feature concerns
- `src/lib/dao-hooks/AGENT.md` — shared DAO data primitives; route-agnostic contract; barrel import preference
- `src/lib/tx-builder/AGENT.md` — shared transaction execution guidance
- `src/lib/legos/AGENT.md` — reusable proposal/form/contract lego definitions
- `src/lib/form-builder/AGENT.md` — form rendering behavior
- `src/features/summon/AGENT.md` — summon route flow; form keys, validation, tx assembly
- `src/features/proposal/AGENT.md` — proposal detail/list/actions/action-data ownership
- `src/features/member/AGENT.md` — member list and detail guidance
- `src/features/safe/AGENT.md` — safe balances and safe proposal guidance

**Planned but not yet built (Phase 2 of the improvement plan):**

- `src/features/settings/AGENT.md`
- `src/features/home/AGENT.md`
- `src/features/dao/AGENT.md`
- `src/lib/ui/AGENT.md`
- `src/lib/keychain-utils/AGENT.md`

**LLM engineer prompt template** (`docs/006_prompt_for_llm_maintainer.md`):
A reusable system/developer prompt block that tells an LLM agent where to start reading, how to map URLs to routes, which layers own which logic, and how to trace and report a bug fix. Ready to drop into any session prompt.

---

## How It Was Structured

The documentation follows a layered graph rather than a single large doc:

| Layer | Doc | Purpose |
|---|---|---|
| Index | `README.md` | Front door; links to everything |
| Mental model | `docs/ARCHITECTURE.md` | System-level map |
| Local navigation | `src/**/AGENT.md` | Scoped, colocated guidance |
| Bug entrypoint | `docs/DEBUGGING.md` | Symptom → file path |
| Domain context | `docs/DOMAIN_GLOSSARY.md` | Vocabulary for agents and new engineers |
| Environment context | `docs/ENVIRONMENT.md` | Env var failures and expected behavior |
| Verification | `docs/VERIFICATION.md` | What to run, by change type |

The key design principle: each doc stays short and local. `AGENT.md` files do not duplicate architecture content; they link back to `docs/ARCHITECTURE.md` instead. This keeps maintenance burden low and docs from going stale.

---

## Design Decisions Worth Noting

- **Rollout was phased.** Started with the highest-value, most stable folders (`src/`, `src/app/`, `src/lib/dao-hooks/`, `src/features/summon/`). Tiny leaf folders and obviously-named folders were deliberately skipped.
- **Debugging doc is symptom-driven.** Instead of describing architecture again, `DEBUGGING.md` starts from real bug reports and traces to likely files — this is how a developer or agent actually encounters problems.
- **LLM prompt template is a first-class deliverable.** It encodes reading order, layer ownership, and fix-reporting discipline as a copyable block, not just informal guidance.
- **Gap analysis was done as a second pass.** After initial delivery, a fresh-eyes review identified stale doc indexes, non-portable Markdown links, and missing guides. This became a structured 5-phase improvement plan rather than ad hoc additions.

---

## What This Means for RG

**The pattern is repeatable.** Any web3 project with a meaningful folder structure (`app/`, `features/`, `lib/` or equivalent) can receive the same treatment: one root doc, one architecture doc, local `AGENT.md` files at folder boundaries, a debugging guide, and a prompt template. The total investment is modest; the payoff is that every future agent session has immediate orientation instead of rediscovering the structure from scratch.

**Local docs next to the code outperform a wiki.** Colocated `AGENT.md` files stay visible during file edits and are naturally discovered by agents reading nearby code. A remote wiki requires a deliberate lookup and goes stale faster.

**The LLM prompt template is a billable artifact.** A reusable system prompt that encodes the repo's layer contracts and fix-reporting discipline is something a client can hand to any agent or contractor. It reduces onboarding friction and reduces the variance in how agents behave in the codebase. RG can offer this as a standard deliverable in future maintenance setup engagements.

**Symptom-based debugging docs are underrated.** Architecture docs explain how things work. Debugging docs explain what to do when things break. The latter is more valuable during an active maintenance engagement and more likely to be used. Future similar engagements should include a `DEBUGGING.md` as a core deliverable, not an afterthought.

**Start with a gap analysis pass.** The two-pass approach — build first, then do a fresh-eyes review — caught non-portable links, stale indexes, and missing coverage that would have quietly degraded agent usefulness. Build the first pass fast; budget the second pass explicitly.

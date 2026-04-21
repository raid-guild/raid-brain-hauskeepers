# Documentation And `AGENT.md` Plan

The 1st section of this doc is the initial plan, the 2nd is an additonal pass to fill holes and fix any issues.

**Goal:** Add lightweight local documentation that helps developers and LLM agents navigate the codebase quickly without introducing large, stale docs.

**Date:** April 14, 2026

---

## Why Add `AGENT.md` Files

The repo now has a clearer structure:

```text
src/
  app/
  features/
  lib/
```

This makes it a good fit for local documentation files because each folder now has a more stable responsibility.

Short `AGENT.md` files can help answer:

- What belongs in this folder?
- What are the important entrypoints?
- What should not be imported directly?
- If I need related logic, where should I look next?

For LLM agents, this is especially useful because it reduces search noise and gives task-local context near the code being edited.

---

## Documentation Principles

Each `AGENT.md` should be:

- short
- operational
- local to the folder
- easy to scan
- focused on structure and workflow, not long-form architecture essays

Each file should avoid:

- duplicating large amounts of README content
- describing every file in detail
- embedding change logs
- documenting unstable implementation details unless they affect navigation

---

## Recommended Rollout Order

### Phase A - Root guidance

Create:

- `src/AGENT.md`

Purpose:

- explain the meaning of `app`, `features`, and `lib`
- define import and ownership rules at a high level
- explain where new files should go

### Phase B - App shell guidance

Create:

- `src/app/AGENT.md`

Purpose:

- describe `components`, `hooks`, `layouts`, and `routes`
- explain route/layout relationships
- clarify that `app` is for shell concerns, not feature business logic

### Phase C - Shared library guidance

Create:

- `src/lib/AGENT.md`
- `src/lib/dao-hooks/AGENT.md`

Purpose:

- explain shared infrastructure expectations
- define public surfaces versus internals
- state whether consumers should import from package barrels or internal files

### Phase D - Feature guidance

Start with the most important or most complex features:

- `src/features/proposal/AGENT.md`
- `src/features/summon/AGENT.md`
- `src/features/member/AGENT.md`

Then expand if helpful:

- `src/features/home/AGENT.md`
- `src/features/safe/AGENT.md`
- `src/features/settings/AGENT.md`
- `src/features/dao/AGENT.md`

---

## Suggested Template

Recommended structure for each `AGENT.md`:

```md
# <Area Name>

## Purpose

- What this folder owns
- What it does not own

## Key Entry Points

- Important files or barrels
- Main route/layout/component/hook entrypoints

## Common Tasks

- If editing X, start here
- If adding Y, place it here

## Related Areas

- Closest neighboring folders and why they matter

## Guardrails

- Public import boundaries
- Avoid direct imports from internal files if applicable
```

---

## Proposed Content By Area

### `src/AGENT.md`

Should include:

- architecture overview for `app`, `features`, `lib`
- where to place new components, hooks, and utils
- alias guidance
- note that feature-local code should prefer colocated `components`, `hooks`, and `utils`

### `src/app/AGENT.md`

Should include:

- `routes` are route entrypoints
- `layouts` are app-shell containers
- `hooks` are app-level concerns like route-derived context or wallet/profile helpers
- `components` are app-wide shared UI composition, not feature-specific screens

### `src/lib/dao-hooks/AGENT.md`

Should include:

- this folder owns shared DAO data/query primitives
- these hooks should remain reusable and route-agnostic
- app-specific wrappers belong in `src/features/dao/hooks` or `src/app/hooks`
- prefer imports from `@/lib/dao-hooks` instead of deep internal paths where possible

### `src/features/proposal/AGENT.md`

Should include:

- proposal detail/list/actions/action-data ownership
- where proposal status display logic lives
- where transaction actions live versus read-only displays
- related areas:
  `src/lib/dao-hooks`, `src/lib/legos`, `src/features/member`

### `src/features/summon/AGENT.md`

Should include:

- summon route flow
- component entrypoints
- where form keys, validation, and tx assembly live
- related areas:
  `src/lib/legos`, `src/lib/tx-builder`, `src/lib/keychain-utils`

---

## What To Avoid

Do not add `AGENT.md` files to every folder immediately.

That would create more maintenance burden than value.

Prefer adding them only where:

- the folder has a stable responsibility
- a developer or agent would genuinely save time from local context
- there are enough files or relationships to justify guidance

Good candidates:

- `src/`
- `src/app/`
- `src/lib/dao-hooks/`
- `src/features/proposal/`
- `src/features/summon/`

Lower-value candidates right now:

- tiny leaf folders with one or two files
- folders whose purpose is already obvious from names alone

---

## Success Criteria

This documentation strategy is working if:

- a new developer can find the right area to edit with minimal repo scanning
- an LLM agent can infer ownership from folder structure plus one nearby `AGENT.md`
- fewer imports cross layers accidentally
- feature work starts from feature folders instead of shared library internals

---

## Recommended First Documentation PR

Start small:

1. Add `src/AGENT.md`
2. Add `src/app/AGENT.md`
3. Add `src/lib/dao-hooks/AGENT.md`
4. Add `src/features/summon/AGENT.md` as the first feature example

This gives the repo a strong pattern without overcommitting to a large documentation surface.

---

## Implementation Status

The first documentation iteration has now been completed and expanded beyond the original minimum scope.

### Completed

Added higher-level documentation:

- `README.md`
- `docs/ARCHITECTURE.md`

Added local navigation docs:

- `src/AGENT.md`
- `src/app/AGENT.md`
- `src/lib/dao-hooks/AGENT.md`
- `src/features/summon/AGENT.md`
- `src/features/proposal/AGENT.md`
- `src/features/member/AGENT.md`
- `src/lib/tx-builder/AGENT.md`
- `src/lib/legos/AGENT.md`
- `src/lib/form-builder/AGENT.md`
- `src/features/safe/AGENT.md`

### What Was Covered

The current docs now provide:

- top-level local setup and environment guidance in `README.md`
- a high-level system map in `docs/ARCHITECTURE.md`
- source-level ownership guidance in `src/AGENT.md`
- app shell and routing guidance in `src/app/AGENT.md`
- shared DAO query/data access guidance in `src/lib/dao-hooks/AGENT.md`
- feature-local guidance for the summon, proposal, and member areas
- shared transaction guidance in `src/lib/tx-builder/AGENT.md`
- reusable form/field/tx definition guidance in `src/lib/legos/AGENT.md`
- form rendering guidance in `src/lib/form-builder/AGENT.md`
- feature-local guidance for the safe area

This means the repo now has both:

- high-level documentation for humans and agents to understand the application as a system
- local `AGENT.md` files for task-specific navigation near the code being edited

### Notes

This work intentionally stayed lightweight:

- docs are short and operational rather than exhaustive
- the rollout focused on stable, high-value folders first
- tiny leaf folders were still avoided

# Documentation Improvement Plan

## Purpose

Improve the repo documentation so a new engineer or LLM coding agent can quickly find the right docs, understand the architecture, navigate to relevant code, and safely fix bugs or add features.

This plan is based on a fresh-eyes review of the current README, architecture doc, and nested `AGENT.md` files.

## Goals

- Make documentation easy to discover from the repo root.
- Make Markdown links portable and clickable across local editors and hosted viewers.
- Expand coverage for currently undocumented feature and library areas.
- Add debugging-oriented docs that help an engineer move from symptom to code.
- Add reusable prompt guidance for assigning this repo to an LLM engineer.

## Current Strengths

- `README.md` gives a useful first entrypoint with setup, project shape, and key docs.
- `docs/ARCHITECTURE.md` gives a helpful high-level map of boot flow, routing, data flow, and transaction flow.
- Nested `AGENT.md` files provide good local guidance for several important areas.
- Existing docs consistently reinforce the intended boundaries between `src/app`, `src/features`, and `src/lib`.

## Key Gaps

- Some doc indexes are stale and do not list newer guides such as `safe`, `form-builder`, `legos`, and `tx-builder`.
- Many Markdown links are not portable because they use machine-local absolute paths or paths that resolve incorrectly from the current document location.
- There is no symptom-driven debugging guide for common bug reports.
- There is no domain glossary for DAOhaus/Moloch V3 concepts.
- Several source areas do not yet have local `AGENT.md` guidance.
- Verification expectations are implicit rather than documented by change type.
- Environment variable behavior is listed, but failure modes are not explained.

## Phase 1: Fix Discoverability And Links

### Tasks

- Update `README.md` docs index to include all current local guides:
  - `docs/ARCHITECTURE.md`
  - `src/AGENT.md`
  - `src/app/AGENT.md`
  - `src/lib/dao-hooks/AGENT.md`
  - `src/lib/tx-builder/AGENT.md`
  - `src/lib/form-builder/AGENT.md`
  - `src/lib/legos/AGENT.md`
  - `src/features/summon/AGENT.md`
  - `src/features/proposal/AGENT.md`
  - `src/features/member/AGENT.md`
  - `src/features/safe/AGENT.md`
- Update `docs/ARCHITECTURE.md` related-docs section to include the same current docs.
- Fix links inside nested docs so they resolve relative to each document location.
- Add a short "Docs Map" section to `README.md` that tells agents which docs to read first.

### Acceptance Criteria

- A new reader can start at `README.md` and find every existing `AGENT.md`.
- Links in `docs/ARCHITECTURE.md` correctly point out of `docs/` where needed.
- Links in `src/AGENT.md` correctly point relative to `src/`.

## Phase 2: Add Missing Local Guides

### Tasks

- Add `src/features/settings/AGENT.md`.
- Add `src/features/home/AGENT.md`.
- Add `src/features/dao/AGENT.md`.
- Add `src/lib/ui/AGENT.md`.
- Add `src/lib/keychain-utils/AGENT.md`.

Each guide should include:

- Purpose
- Folder map
- Key entry points
- Common tasks
- Guardrails
- Related areas

### Acceptance Criteria

- Every major folder under `src/features` has a local guide.
- Major reusable infrastructure under `src/lib` has local guidance when it is likely to be touched by bug fixes.
- New guides follow the same concise format as the existing `AGENT.md` files.

## Phase 3: Add Debugging-Oriented Docs

### Tasks

- Create `docs/DEBUGGING.md`.
- Include symptom-to-starting-point recipes, such as:
  - DAO route does not load.
  - Proposal list or detail data is wrong.
  - Proposal action data or decoding is wrong.
  - Proposal action button state is wrong.
  - Summon transaction fails.
  - Safe balances or Safe proposals are wrong.
  - Member list or member detail is stale or incorrect.
  - Settings update form submits the wrong transaction.
  - Wallet or network state behaves unexpectedly.
- For each recipe, include:
  - Primary route or component entrypoint.
  - Data hook or utility likely involved.
  - Transaction/form layer if relevant.
  - Suggested verification command or manual check.

### Acceptance Criteria

- A new engineer with a bug report can choose an initial file path in under one minute.
- The guide points to existing architecture and local `AGENT.md` docs rather than duplicating everything.
- Recipes are short enough to scan quickly.

## Phase 4: Add Domain And Environment Context

### Tasks

- Create `docs/DOMAIN_GLOSSARY.md`.
- Define project-specific terms:
  - DAO
  - DAOhaus
  - Moloch V3
  - Baal
  - proposal
  - summon
  - ragequit
  - Safe
  - shaman
  - shares
  - loot
  - vault
  - graph/query data
  - transaction lego
  - form lego
- Create `docs/ENVIRONMENT.md`.
- Explain each env var from `.env.example` and `src/lib/env.ts`.
- Document what usually breaks when a required key is missing.
- Link this from `README.md`.

### Acceptance Criteria

- A new agent can understand domain language used in bug reports without leaving the repo.
- Environment setup explains both required values and observable failure modes.
- `README.md` remains concise and links to detailed docs instead of growing too large.

## Phase 5: Add Verification Guidance

### Tasks

- Create `docs/VERIFICATION.md`.
- Document standard commands:
  - `npm run lint`
  - `npm run build`
  - `npm run dev`
  - `npm run preview`
- Add change-type guidance:
  - Docs-only change
  - UI component change
  - Data hook change
  - Transaction flow change
  - Environment/config change
  - Routing change
- Note any missing test coverage or manual verification expectations.

### Acceptance Criteria

- Engineers know what to run before handing back a fix.
- LLM agents have explicit guidance for reporting verification and residual risk.

## Risks And Notes

- Keep docs concise. The current guides work because they are short and local.
- Avoid duplicating architecture details across every `AGENT.md`; link back to `docs/ARCHITECTURE.md`.
- Treat doc links as part of the product. Broken links directly reduce agent usefulness.
- Update `README.md` whenever a new major guide is added.

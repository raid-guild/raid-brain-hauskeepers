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

_First captured: April 2026_

Most documentation is written for humans to read once. AI agents re-read docs on every session. Practices that improved agent output: consistent heading structure, explicit statement of assumptions and constraints, documenting "why" decisions were made (not just what), keeping docs colocated with the code they describe.

LLMs reason over text. Well-structured, explicit documentation measurably improves the quality of AI agent output. This is a service RG can deliver — LLM-optimized documentation is a distinct deliverable, not just a side effect of writing good docs.

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

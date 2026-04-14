# Best Practices — AI-Assisted Maintenance (Living Document)

**Purpose:** A running capture of practices, patterns, and recommendations that emerge from this raid. This is the raw material for RG's future service offering and for the guild presentation. Add entries as they emerge — don't wait until the end.

**How to add an entry:** Drop a new section under the relevant category. Include the context (where it came from), the practice itself, and why it works.

---

## Codebase Structure for AI Maintainability

### Structure codebases for intent, not history

**Context:** DAOhaus had a decade of accumulated structure that made sense historically but was hard for both humans and AI agents to navigate.

**Practice:** Organize code by what it does (`app/`, `features/`, `lib/`) not by what type of thing it is (`components/`, `hooks/`, `utils/`). Reduce alias surface to 2–3 stable roots.

**Why it works:** AI agents navigate by pattern-matching. A flat, semantically clear structure reduces the cognitive overhead (and token cost) of every agent operation. Humans benefit too.

---

### Keep directories shallow and feature-colocated

**Context:** The original DAOhaus repo had shared folders with dozens of files. Finding anything required knowing the history.

**Practice:** Colocate feature-specific utilities, hooks, and components within the feature folder. Only truly shared utilities belong in `lib/`.

**Why it works:** An agent asked to work on the proposal feature can read `features/proposal/` and have everything it needs. No cross-repo hunting.

---

### Write documentation for LLMs, not just humans

**Context:** Most documentation is written for humans to read once. AI agents re-read docs on every session.

**Practice:**
- Use consistent heading structure across all docs
- State assumptions and constraints explicitly (don't rely on context)
- Document "why" decisions were made, not just what was done
- Keep docs close to the code they describe (colocated, not in a separate docs repo)

**Why it works:** LLMs reason over text. Well-structured, explicit documentation dramatically improves the quality of AI agent output.

---

## Dependency Modernization

### Bundle major upgrades into a single structured sprint

**Context:** Clients often have many outdated dependencies and resist upgrading them because each change feels risky.

**Practice:** Audit all major dependencies, group them by upgrade difficulty, then run them as a single sprint with a defined order. Don't try to ship incremental upgrades in production — do the full modernization pass in one push.

**Why it works:** The overhead of upgrading is mostly in understanding the system, not in the changes themselves. Bundling pays that cost once. Incremental upgrades pay it repeatedly.

---

### Inline packages as local source when possible

**Context:** The DAOhaus monorepo had many `@daohaus/*` internal packages that added indirection without providing real value.

**Practice:** For internal packages that are only consumed by one app, inline them as local source (`src/lib/`). Remove the package abstraction.

**Why it works:** Eliminates an entire layer of build complexity. Makes the dependency graph obvious. Makes AI agents' lives much simpler — no jumping between package repos.

---

## AI-Assisted Maintenance Systems

<!-- Entries to be added as the AI system workstream progresses -->

### [Placeholder — add entries from AI system workstream]

---

## Human-in-the-Loop Design

<!-- Entries to be added as workflows are designed and tested -->

### [Placeholder — add entries as workflow patterns emerge]

---

## Documentation and SOPs

<!-- Entries to be added from the docs and SOP workstreams -->

### [Placeholder — add entries as docs and SOPs land]

---

## What to Do Early (Order of Operations)

**Practice:** When starting a maintenance modernization project, do codebase simplification before setting up AI tooling — not after.

**Why it works:** AI agents are more effective on clean, well-structured codebases. Setting up agentic tooling on a messy codebase just means the agent inherits all the confusion. Clean first, then automate.

---

## Anti-Patterns to Avoid

<!-- Practices that seemed reasonable but caused problems. Add as they emerge. -->

| Anti-pattern | What went wrong | Better approach |
|-------------|----------------|-----------------|
| | | |

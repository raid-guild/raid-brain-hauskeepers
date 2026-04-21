# Documentation Strategy

We created a layered documentation strategy aimed at helping both humans and LLM coding agents land in the right part of the repo quickly, understand the architecture, and make safer changes.

At a high level, the pattern is:

## 1. Root-Level Orientation

README.md is the front door. It now gives setup basics, the project shape, and a complete docs map. The goal is that a new contributor can start at the root and find the right next doc without guessing.

## 2. System-Level Architecture

docs/ARCHITECTURE.md explains the app at the system level: boot flow, routing, data flow, transaction flow, dependency boundaries, and common starting points. This gives enough context to understand how the major pieces fit together before diving into files.

## 3. Local Navigation Guides

Each important feature or library area gets an AGENT.md. These are short, local guides that answer:

- What does this folder own?
- What are the key entry points?
- Where do common changes start?
- What should not go here?
- What related docs or folders should I inspect?

This is probably the strongest reusable pattern for other repos: put small, scoped docs next to the code they explain.

## 4. Symptom-Based Debugging

docs/DEBUGGING.md maps bug symptoms to likely files and flows. Instead of only documenting architecture, it helps someone start from a real report like “proposal action state is wrong” or “Safe balances are missing” and quickly find the relevant route, feature component, hook, transaction layer, or metadata utility.

## 5. Domain Context

docs/DOMAIN_GLOSSARY.md explains project vocabulary like DAO, Baal, Safe, summon, ragequit, shares, loot, shaman, form lego, and transaction lego. This keeps domain knowledge inside the repo instead of relying on tribal knowledge.

## 6. Environment Context

docs/ENVIRONMENT.md documents env vars by purpose and failure mode. This is useful because many app failures are not code bugs; they are missing keys or network configuration problems.

## 7. Verification Guidance

docs/VERIFICATION.md tells contributors what to run based on the type of change. It also sets expectations for reporting what was verified and what risk remains.

The main takeaway pattern is: don’t make one giant doc. Build a docs graph.

Use:

- README.md as the index.
- ARCHITECTURE.md as the mental model.
- Local AGENT.md files as navigation guides.
- DEBUGGING.md as the bug-report entrypoint.
- Glossary/env/verification docs as supporting context.

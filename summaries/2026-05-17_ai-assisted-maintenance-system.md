# AI-Assisted Maintenance System Workstream Summary

**Date:** 2026-05-17  
**Workstream:** AI-Assisted Maintenance System  
**Scope:** Agentic development environment, GitHub issue management, human-in-the-loop processes

---

## What Was Built

The AI-assisted maintenance system for DAOhaus runs on the Superprism Refactory platform (https://refactory.superprism.io/), a Prism Railway stack deployed specifically for this engagement. It connects Discord and Refactory intake, Codex-based agent execution, Prism Memory and Knowledge for context and history, GitHub for code review and merge state, and Railway for deployment verification.

The system is not an autonomous agent that runs DAOhaus. It is a structured handoff protocol between human judgment and agent execution, where the human stays on every decision that affects production.

### Platform Architecture

The deployed maintenance stack consists of seven Railway services:

| Service | Role |
| --- | --- |
| `site` | Control plane — owns requests, tasks, skills, workflows, artifacts, and agent session state |
| `codex-runtime` | Agent execution — thin HTTP wrapper around the Codex CLI, manages workspaces and model output |
| `prism-memory` | Memory and knowledge — indexes artifacts, digests, knowledge docs, and operational history |
| `discord-adapter` | External bridge — receives Discord messages/events and forwards them into the app flow |
| `memory-cron` | Hourly — processes inbox items, digests, and memory seed outputs |
| `knowledge-cron` | Daily — promotes and indexes knowledge docs |
| `discord-sync-cron` | Every 15–60 min — pulls Discord message history through the discord-adapter |

The site/API owns durable orchestration state. Codex Runtime is a narrow execution boundary. Prism Memory/Knowledge is a split between time-based operational record (what happened) and curated retrievable docs (how things work). The pattern preserves context across agent sessions and operator reviews without trusting chat messages as the source of truth.

### Issue Lifecycle

Issues flow through a defined status path:

```
Inbox
  -> Triaging
  -> Ready for Agent
  -> Working
  -> Awaiting Review
  -> Approved
```

With a revision loop:

```
Awaiting Review -> Changes Requested -> Working -> Awaiting Review
```

Every gate where the status advances to a new stage requires explicit human confirmation. The agent does not self-advance issues through intake, into implementation, or into review.

### Human-in-the-Loop Gates

Human review is required before:

- Moving an inbox item into agent triage
- Moving a triaged issue into implementation
- Accepting an agent-created branch
- Creating, approving, or merging a pull request
- Treating an automation report as an incident
- Changing production configuration or deployment settings

The agent is scoped to bounded implementation tasks — triage summaries, code investigation, branch preparation, small bug fixes, documentation changes, and maintenance reporting. Contract changes, DNS/registrar changes, Graph funding or multisig access, production secrets, and access-control changes are explicitly outside the AI-assisted flow.

### Memory and Knowledge Split

A key design decision that emerged from this workstream: Prism distinguishes between Memory (what happened — transcripts, digests, runtime outputs, activity history) and Knowledge (how things work — SOPs, runbooks, architecture notes, stable summaries). This split matters for future agent sessions because it prevents operational noise from polluting the curated reference layer, and it creates a promotion path:

```
raw event / execution -> artifact -> memory index -> curated knowledge doc
```

---

## What This Means for RG

**The platform pattern is deployable.** The Prism Railway Template turns a repeatable service offering into a one-command deploy with instance-specific secrets, volumes, and cron configuration. A future RG engagement can start from the same template rather than building the stack from scratch.

**Human-in-the-loop is a feature, not a limitation.** The system's value proposition to a client is not "the agent handles everything" — it is "the agent handles triage, investigation, and branch preparation so your one maintainer spends their review time on decisions, not groundwork." That framing is more durable and more honest in a sales context.

**The memory/knowledge split should be a standard deliverable.** Every AI-assisted engagement produces operational context that rots unless it is indexed. The distinction between what-happened (memory) and how-things-work (knowledge) gives future agents and operators a clean entry point. RG should treat this split as a standard setup step, not an optional feature.

**Codex auth is the main friction point.** Device auth is a one-time manual step that must happen on the mounted volume in the deployed Railway service. This cannot be scripted away. Future engagements should budget setup time for this step and document it clearly in the handoff.

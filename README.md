# Hauskeeper Raid — Knowledge Base

Knowledge base for the **DAOhaus Infrastructure Modernization & AI-Assisted Maintenance** raid, executed by Raid Guild.

---

## Structure

```
docs/         Project documents — proposals, planning specs, resources. Drop files here freely.
summaries/    Generated summaries of completed work and milestones.
learnings.md  Accumulating learnings for Raid Guild and future clients.
CLAUDE.md     Instructions and workflow definitions for AI agents working in this KB.
```

---

## Workflows

See [AGENT.md](AGENT.md) for full instructions. Two workflows are defined:

**Generate Summary** — tell the agent which files to draw from and what framing to use. Output lands in `summaries/`.

**Output Learnings** — tell the agent to extract learnings from a set of files or summaries. Output accumulates in `learnings.md`.

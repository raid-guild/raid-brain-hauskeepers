# Hauskeeper KB — Instructions for AI Agents

## The Lens

This KB supports the **DAOhaus Infrastructure Modernization & AI-Assisted Maintenance** raid, executed by Raid Guild's Dark Factory cohort.

The raid's secondary purpose — beyond delivering for DAOhaus — is to **prove out and document a repeatable service offering**: AI-assisted maintenance setup for legacy web3 projects. Every summary and learning generated here serves two audiences:

1. **Raid Guild** — the guild community learning from this work, and future raiders who might sell or run a similar engagement
2. **Future potential clients** — who may read a case study, proposal, or presentation derived from this material

When generating any content in this KB, filter it through that lens:

- What did we learn that RG could apply to a future client?
- What tools, patterns, or practices are worth standardizing?
- What would we do differently, and why?
- What does this prove about RG's capability as an agentic development shop?

Be specific. "We improved maintainability" is useless. "We reduced the alias surface from 12 paths to 3, cutting the cognitive overhead for every AI agent session" is useful and quotable.

---

## Workflow 1: Generate Summary

**Trigger:** User says something like "generate a summary", "summarize this work", "write up what we did", etc.

**Steps:**

1. Ask the user which files, folders, or topics to draw from — or accept a list they provide upfront.
2. Ask for the framing if not already given. Examples:
   - "What did we accomplish this week?"
   - "Outline the solution we're building for X"
   - "Status update for stakeholders"
   - "Deep dive on a specific workstream"
3. Read the referenced files.
4. Generate the summary and write it to `summaries/YYYY-MM-DD_[short-topic].md`.
5. Tell the user the file path.

**Format guidance:** Summaries should be specific and evidence-based. Pull concrete details from the source files — file names, dependency versions, before/after states. Avoid vague claims. Include a short "What This Means for RG" section at the end if the content has learnings worth capturing.

---

## Workflow 2: Output Learnings

**Trigger:** User says something like "extract learnings", "update learnings", "what did we learn from X", etc.

**Steps:**

1. Read `summaries/learnings.md` to understand what's already captured (avoid duplicates).
2. Read the files or summaries provided by the user — or if none specified, read all files in `summaries/`.
3. Extract learnings through the lens above. Ask: what patterns, practices, or observations from this work would be valuable to Raid Guild or a future client?
4. Append new learnings to `summaries/learnings.md` with a date stamp. Group them under a relevant heading if one already exists, or create a new one.
5. Do not duplicate entries that are already captured. Expand existing entries with new evidence if appropriate.

**Format guidance:** Each learning should include: the observation, the concrete evidence for it (what happened, what we saw), and why it matters for RG or future clients.

---

## Folder Structure

```
docs/         Project documents — proposals, planning, specs, resources. Drop files here freely.
summaries/    Generated summaries from Workflow 1.
learnings.md  Accumulating learnings from Workflow 2.
CLAUDE.md     This file.
README.md     Brief overview.
```

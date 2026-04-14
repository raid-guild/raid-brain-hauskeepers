# Contributing to This KB

This file is the north star for anyone — human or AI agent — adding content to this knowledge base. Read it before generating any document.

---

## The Lens Everything Is Written Through

This raid is not just client work. It is a **model for a repeatable Raid Guild service offering**:

> AI-assisted maintenance setup for legacy web3 projects — helping teams reduce maintenance overhead, modernize infrastructure, and operate efficiently with agentic developer tooling.

Every document added to this KB should be written through that lens. When generating summaries, updates, or evaluations, always ask:

- What did we learn that RG could apply to a future client?
- What tools, patterns, or practices are worth standardizing?
- What would we do differently, and why?

Guild updates should read as: *here is what we built and learned — and here is what it means for RG as an agentic development shop.*

---

## Rituals

### When work completes (any workstream)
Add a summary to `completed-work/` using `completed-work/_TEMPLATE.md`. The final section — "What This Means for Future RG Clients" — is required, not optional.

### When a tool is evaluated
Fill out `tool-evaluations/_TEMPLATE.md` immediately after evaluation. Tool knowledge is the most perishable — capture it while it's fresh. Include a verdict and a note on fit for the RG service offering.

### Guild update cadence
Generate an update at each major milestone or every two weeks, whichever comes first. Use `guild-updates/_TEMPLATE.md`. Pull from recent `completed-work/` and `tool-evaluations/` entries. Always include the "What This Means for Raid Guild" section.

### End of raid
Run a retrospective pass across all `completed-work/` and `tool-evaluations/` docs. Use them to finalize the `narrative/` docs for the guild presentation. The three narrative files should feel like they were written from a position of confidence — populate them with specific evidence, not intentions.

---

## Document Generation Instructions for AI Agents

When generating any document in this KB:

1. **Check the relevant template first.** Templates live at `_TEMPLATE.md` inside each folder.
2. **Pull from existing KB content.** Summaries should synthesize `completed-work/`. Guild updates should reference `tool-evaluations/`. Don't generate from scratch when source material exists.
3. **Always include the RG service framing.** Every document type has a section for this. Do not skip it.
4. **Write for two audiences.** The immediate audience is the Raid Guild community. The secondary audience is a future potential client reading a case study. Write with both in mind.
5. **Be specific.** Vague claims ("we improved maintainability") are useless. Specific claims ("we reduced the alias surface from 12 paths to 3") are useful and quotable.

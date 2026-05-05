# Reduced Community & Repo Surface Area Summary

**Date:** May 5, 2026
**Source docs:** `docs/000_scope.md`, `docs/007_repo_docs_overview.md`,
`docs/010_dns_catalog.md`, `docs/011_community_surface_plan.md`,
`docs/014_discord_cleanup.md`

---

## What We Did

This workstream reduced the number of public surfaces a DAOhaus user,
maintainer, or AI agent needs to understand before finding the right system. The
work focused on three connected areas: GitHub/repository clarity, Discord
channel consolidation, and public documentation cleanup.

### GitHub And Active System Clarity

The DAOhaus repository surface was mapped and labeled so active systems are
distinguishable from preserved legacy work. The community surface plan records
completed work to create or update the canonical `HausDAO` repository map, label
active repositories, mark unused repositories as deprecated, preserve legacy
repositories for historical access, clarify actively maintained repositories,
deprecate old monorepo workflows, and document the final GitHub structure in the
maintenance packet.

This turns GitHub from a broad archive into a maintainable operating surface:
active maintainers and AI agents can focus on the canonical admin app, subgraph,
contracts, docs, guide, and website repos without treating every historical repo
as an equal candidate for maintenance.

### Discord Channel Consolidation

The Discord cleanup inventoried the existing server surface and identified
several overlapping areas:

- General discussion was spread across `#tavern`, `#bright-ideas`,
  `#protocol-chat`, `#product-chat`, and `#publichaus-chat`.
- Support and bug reporting were split across `#support` and `#bug-reports`
  (now moving toward `#change-requests`).
- Activity/reporting was split across `#news-flash`, `#rage-beats`,
  `#rage-ships`, `#product-activity`, and `Public HAUS Updates`.
- Voice channels existed across Public Square, PublicHaus, Protocol, and
  Products.

The cleanup simplified the operating structure around a smaller active set:
`#welcome`, `#announcements`, `#support`, `public-forum`, `#protocol-info`,
`#protocol-chat`, `#change-requests`, `#rage-ships`, `protocol-voice`, and the
mod-only `#gatehaus`. The server guide, welcome flow, and Protocol info were
rewritten; mod-only channels and community onboarding were cleaned up; and
`#rage-ships` webhooks were updated to trigger from canonical repos.

New active roles are now explicit: `basic visitor`, `warcamp` for admins, and
`hauskeeper` for controlled intake and maintenance work.

### Public Documentation And Website Cleanup

The public documentation pass reviewed the main DAOhaus surfaces:
`daohaus.club`, `guide.daohaus.club`, `docs.daohaus.club`, and
`moloch.daohaus.fun`. Outdated SDK docs were removed or clearly archived, user
and developer docs were simplified, links to deprecated apps and workflows were
removed unless explicitly historical, and docs were updated to point users toward
active tools and systems.

The docs strategy also produced a reusable pattern for maintainable public and
repo-local documentation: `README.md` as the front door, architecture docs for
system context, local `AGENT.md` files for folder-level navigation,
symptom-based debugging docs, domain glossary, environment docs, and
verification guidance. This gives both human contributors and LLM agents a
short path from "where am I?" to "what should I change?"

The DNS and hosting catalog supports the same cleanup. Core public surfaces now
point to Railway-hosted repos for the website, docs, guide, and admin app:
`daohaus.club`, `www.daohaus.club`, `admin.daohaus.club`,
`docs.daohaus.club`, and `guide.daohaus.club`. Many old records were marked
deprecated on April 29, 2026, and root/www Netlify records were deprecated on
May 2, 2026 after the Railway move.

---

## Current Status

The workstream has substantially reduced DAOhaus' public operating surface. The
active repo set is clearer, public docs now direct people toward maintained
systems, and Discord has a simpler channel model for onboarding, support,
protocol discussion, change requests, and release/activity reporting.

Remaining work is focused rather than exploratory:

- Implement the support flow as part of the AI maintenance workstream.
- Create and publish an announcement post when the raid is shipped.
- Finish any remaining DNS/account ownership questions, especially `.club`
  transfer ownership, Google Workspace/email usage, Amazon SES purpose, and
  whether Cloudflare can be closed after cleanup.
- Rewrite `docs.daohaus.club/contributing` if it remains part of the maintained
  public docs surface.

---

## What This Means For RG

This workstream is a strong example of "maintenance readiness" as more than code
cleanup. Legacy web3 projects often accumulate confusion across GitHub,
Discord, websites, docs, DNS, and hosting. Reducing that surface area makes the
project easier for users to trust, easier for maintainers to operate, and easier
for AI agents to navigate safely.

The repeatable RG pattern is:

- Inventory every public and maintainer-facing surface.
- Mark active, deprecated, and historical systems explicitly.
- Collapse support and reporting into a small number of canonical channels.
- Update docs and DNS only after the active destination is clear.
- Preserve history without forcing maintainers to treat it as active work.

For future clients, this is a concrete service offering: turn a sprawling legacy
project into a smaller, labeled, agent-ready maintenance environment before
automation is layered on top.

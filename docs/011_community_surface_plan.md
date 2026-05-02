# DAOhaus Community Surface Area Reduction Plan

## Purpose

Working document for Workstream 4: Community Surface Area Reduction.

This doc is the place to plan, track, and summarize the cleanup of DAOhaus public/community surfaces so future maintainers and users can tell what is active, what is historical, and where support or governance activity should happen.

## Workstream Goals

- Reduce public confusion around active vs. legacy DAOhaus systems.
- Consolidate Discord activity into a small number of clear channels and categories.
- Clearly label active, maintained repositories.
- Preserve legacy code and historical artifacts while marking them as deprecated.
- Remove or update outdated SDK and developer documentation.
- Ensure public docs and websites only point users toward active tools and systems.
- Capture decisions and rationale for handoff into the maintenance SOP packet.

## Todo

### Discord Cleanup

- [ ] Inventory current Discord categories and channels.
- [ ] Identify unnecessary or inactive channels to archive.
- [ ] Propose simplified Discord category structure:
  - Legacy user support
  - Governance discussions
  - Announcements
  - AI Flow reporting
- [ ] Get feedback on the proposed Discord structure before making changes.
- [ ] Archive approved unnecessary channels.
- [ ] Consolidate active discussion into the approved categories.
- [ ] Update channel descriptions and pinned messages for retained channels.
- [ ] Confirm announcement channels and governance channels are easy to find.
- [ ] Configure AI Flow reporting channel(s) for:
  - Issue triage
  - API monitoring
  - Activity reports
- [ ] Clean up Rage Ships webhooks so they only watch canonical/active repositories.
- [ ] Document final Discord structure and any bot/webhook dependencies.

### GitHub Organization and Repositories

- [x] Create or update a canonical repository map for `https://github.com/HausDAO`.
- [x] Label active repositories clearly.
- [x] Mark unused repositories as deprecated.
- [x] Preserve legacy repositories for historical access.
- [x] Clarify which repositories are actively maintained.
- [x] Deprecate or remove monorepo workflows where no longer relevant.
- [x] Document final GitHub repo structure in the maintenance packet.

Suggested inactive repo notice:

> This project has been packed away in the attic - not actively maintained, but preserved for reference.

### Public Documentation and Websites

- [ ] Review public documentation surfaces:
  - [daohaus.club](https://daohaus.club/)
  - [guide.daohaus.club](https://guide.daohaus.club/)
  - [docs.daohaus.club](https://docs.daohaus.club/)
  - [moloch.daohaus.fun](https://moloch.daohaus.fun/)
- [ ] Identify outdated SDK documentation.
- [ ] Remove or clearly archive outdated SDK docs.
- [ ] Review and simplify user documentation.
- [ ] Review and simplify developer documentation.
- [ ] Ensure docs point to active tools and systems only.
- [ ] Remove links to deprecated apps, repos, workflows, or deployment targets unless explicitly marked historical.
- [ ] Confirm docs describe the canonical admin app, subgraph, and Baal contract repos.
- [ ] Catalog website/docs links that need redirects or DNS follow-up.
- [ ] Publish updated website/docs links before decommissioning related DNS records.
- [ ] Document what public documentation changed.

### Domains, DNS, and Hosting Surface

- [ ] Cross-reference this work with `docs/010_dns_catalog.md`.
- [ ] Confirm which old v2-era Netlify-hosted sites should remain online with no maintenance.
- [ ] Confirm final handling for:
  - `yeet.daohaus.club`
  - `summon.daohaus.club`
  - other legacy app subdomains listed in the DNS catalog
- [ ] Confirm `.club` domain registrar ownership and renewal details.
- [ ] Create or identify account for transferring the `.club` domain.
- [ ] Confirm whether anyone is using `daohaus.club` email addresses.
- [ ] Confirm why Amazon SES was set up and whether it is still needed.
- [ ] Close Cloudflare account if no longer needed after DNS/app cleanup.
- [ ] Decommission DNS records only after website/docs references are updated.
- [ ] Document remaining active DNS records and rationale.

### Architecture and Dependency Documentation

- [ ] Create or link architecture diagram: frontend -> contracts -> indexer -> data flow.
- [ ] Document active code dependencies.
- [ ] Document active third-party service dependencies.
- [ ] Document deployment, infrastructure, and dependency surface.
- [ ] Document active servers/hosting services.
- [ ] Complete environment variable inventory.
- [ ] Identify any public-facing docs that should link to the architecture/dependency overview.
- [ ] Feed finalized architecture/dependency notes into the maintenance SOP packet.

## Open Questions

- Is anyone actively using `daohaus.club` email addresses?
- Is there a current Google Workspace owner/admin for `daohaus.club` email?
- Why was Amazon SES configured for `daohaus.club`?
- Can Amazon SES records be removed, or do they support an active notification flow?
- What account should receive the `.club` domain transfer?
- Which v2-era Netlify sites should intentionally remain public?
  - v2 admin app is the only one
- Which Discord channels must remain visible for governance/history reasons?
- Which webhook/reporting flows should post to AI Flow reporting channels?

## Work Completed

Use this section as the running summary while completing the workstream.

### Discord

- TBD

### GitHub

- TBD

### Public Docs and Websites

- TBD

### Domains and DNS

- TBD

### Architecture and Infrastructure Docs

- TBD

## Final Summary Draft

TBD

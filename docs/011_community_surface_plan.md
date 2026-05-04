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

- [x] Inventory current Discord categories and channels.
- [x] Identify unnecessary or inactive channels to archive.
- [ ] Propose simplified Discord category structure:
- [ ] Archive approved unnecessary channels.
- [ ] Update channel descriptions and pinned messages for retained channels.
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

- [x] Review public documentation surfaces:
  - [daohaus.club](https://daohaus.club/)
  - [guide.daohaus.club](https://guide.daohaus.club/)
  - [docs.daohaus.club](https://docs.daohaus.club/)
  - [moloch.daohaus.fun](https://moloch.daohaus.fun/)
- [x] Remove or clearly archive outdated SDK docs.
- [x] Review and simplify user documentation.
- [x] Review and simplify developer documentation.
- [ ] rewrite https://docs.daohaus.club/contributing
- [x] Ensure docs point to active tools and systems only.
- [x] Remove links to deprecated apps, repos, workflows, or deployment targets unless explicitly marked historical.
- [x] Confirm docs describe the canonical admin app, subgraph, and Baal contract repos.
- [x] Publish updated website/docs links before decommissioning related DNS records.
- [x] Update website - simplify to basic needed info and remove old links
- [x] move website, docs and guide deployments to railway

### Domains, DNS, and Hosting Surface

- [x] Cross-reference this work with `docs/010_dns_catalog.md`.
- [x] Confirm which old v2-era Netlify-hosted sites should remain online with no maintenance.
- [x] Confirm `.club` domain registrar ownership and renewal details.
- [ ] Create or identify account for transferring the `.club` domain.
- [ ] Confirm whether anyone is using `daohaus.club` email addresses.
- [ ] Confirm why Amazon SES was set up and whether it is still needed.
- [ ] Close Cloudflare account if no longer needed after DNS/app cleanup.
- [x] Decommission DNS records only after website/docs references are updated.
- [x] Document remaining active DNS records and rationale.

### Architecture and Dependency Documentation

- [x] Create or link architecture diagram: frontend -> contracts -> indexer -> data flow.
- [x] Document active third-party service dependencies.
- [ ] Document active servers/hosting services.
- [x] Complete environment variable inventory.
- [x] Identify any public-facing docs that should link to the architecture/dependency overview.

## Final Summary Draft

TBD

# System Overview & Architecture Inputs

Working notes for Section 1 of the DAOhaus Maintenance SOP Packet: System Overview & Architecture.

This doc collects the raw inputs needed to author the high-level system narrative, architecture diagram, and repository map described in [009_sop_workstream_ideation.md](./009_sop_workstream_ideation.md).

## Starter System Narrative

DAOhaus is a DAO administration stack built around Baal smart contracts, a subgraph/indexing layer, and a web-based admin application.

At a high level:

- DAO members and operators use the admin app to view DAOs, members, proposals, treasuries, and settings.
- The admin app reads indexed protocol data from the DAOhaus subgraph.
- The subgraph indexes events and state from Baal contracts across supported networks.
- Transaction flows in the admin app prepare and submit contract interactions through connected wallets and supporting transaction tooling.
- The live maintenance surface is primarily the admin app, with contract and subgraph maintenance needed when protocol behavior, supported networks, deployments, or indexed data requirements change.

## Active Stack Repositories

These are the three active repositories that make up the stack that needs to be maintained.

| Repository                                                              | Status             | Role                           | Maintenance Notes                                                                        |
| ----------------------------------------------------------------------- | ------------------ | ------------------------------ | ---------------------------------------------------------------------------------------- |
| [HausDAO/daohaus-admin](https://github.com/HausDAO/daohaus-admin)       | Active / canonical | Main DAOhaus admin application | Primary repository for maintenance automation. This is the main user-facing app surface. |
| [HausDAO/daohaus-subgraph](https://github.com/HausDAO/daohaus-subgraph) | Active / canonical | Subgraph and indexing layer    | Maintains indexed data used by the admin app and related consumers.                      |
| [HausDAO/Baal](https://github.com/HausDAO/Baal)                         | Active / canonical | Smart contracts                | Core Baal contract system that the app and subgraph depend on.                           |

## Supporting And Reference Repositories

These repositories should be cataloged in the repository map, but they are not currently the primary live maintenance target.

| Repository                                                  | Status                    | Role                      | Maintenance Notes                                                                                                                       |
| ----------------------------------------------------------- | ------------------------- | ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [HausDAO/monorepo](https://github.com/HausDAO/monorepo)     | Deprecated / preserved    | Legacy monorepo reference | Keep available for historical context. Do not treat as canonical for current maintenance unless a specific legacy question requires it. |
| [HausDAO/dev-docs](https://github.com/HausDAO/dev-docs)     | Supporting docs           | Developer documentation   | Review for accuracy against the active app, subgraph, and Baal repos. Remove or label outdated SDK/workflow references.                 |
| [HausDAO/user-guide](https://github.com/HausDAO/user-guide) | Supporting docs           | User-facing documentation | Review for current user flows and links to active apps only.                                                                            |
| [HausDAO/website](https://github.com/HausDAO/website)       | Supporting public surface | Website / landing page    | Catalog as part of public surface maintenance and deployment documentation.                                                             |

All other HausDAO organization repositories can be considered deprecated or preserved for historical reference unless specifically identified as active during the final organization inventory pass.

## Architecture Inputs

The SOP architecture section should stay high-level and point maintainers toward the active repos for deeper implementation details.

### Stack Overview

DAOhaus has three primary runtime layers:

1. **Contracts:** [HausDAO/Baal](https://github.com/HausDAO/Baal)
2. **Indexer:** [HausDAO/daohaus-subgraph](https://github.com/HausDAO/daohaus-subgraph)
3. **Admin app:** [HausDAO/daohaus-admin](https://github.com/HausDAO/daohaus-admin)

The contracts are the source of truth for DAO state and actions. Baal contracts define the onchain DAO behavior that members interact with through proposals, membership changes, treasury operations, and related DAO administration flows.

The subgraph indexes contract events and chain state into a queryable data layer. This lets the admin app read DAO, member, proposal, token, treasury, and record data without manually reconstructing everything from raw RPC calls.

The admin app is the main user-facing maintenance surface. It gives DAO members and operators a web interface for reading indexed DAO data and preparing wallet-based transactions back to the Baal contracts.

Suggested SOP diagram:

```text
Baal contracts
  -> emit events / expose onchain state
  -> daohaus-subgraph indexes supported networks
  -> daohaus-admin queries indexed data
  -> users review DAO state and submit transactions
  -> transactions write back to Baal contracts
```

### Admin App Architecture Overview

The admin app is a Vite + React application. It uses React Router for route screens, TanStack Query for remote data caching, Wagmi and RainbowKit for wallet and chain state, and DAOhaus shared hooks/utilities for DAO-specific reads and transaction flows.

At startup, the app mounts shared providers for wallet state, query caching, wallet UI, DAO hook configuration, theming, and routing. This means route screens can generally assume wallet, query, theme, and DAO data context already exist.

The route model is organized around:

- A home/dashboard area.
- A DAO summon flow.
- DAO-specific routes under the `molochv3/:daochain/:daoid` path.
- DAO child screens for overview, proposals, proposal detail, members, member detail, safes, settings, new proposals, and ragequit.

The code is organized into three broad areas:

- `src/app`: route entrypoints, layouts, navigation shells, and app-wide helpers.
- `src/features`: user-facing feature areas such as DAO views, summon, proposals, members, safes, and settings.
- `src/lib`: shared infrastructure such as DAO data hooks, transaction builder, form builder, legos, keychain/network utilities, and UI primitives.

Read-oriented flows generally start from route params and wallet state, call DAO data hooks, cache remote results through TanStack Query, and render those results into feature screens.

Write-oriented flows generally collect user input in a route or feature component, translate it into transaction arguments or reusable transaction configuration, pass it through the shared transaction builder, and then rely on wallet interaction for signing/submission.

For deeper implementation detail, the SOP team should review the architecture and local agent docs inside [HausDAO/daohaus-admin](https://github.com/HausDAO/daohaus-admin), especially the admin app architecture doc and related docs for debugging, environment variables, verification, DAO hooks, transaction builder, form builder, legos, features, and UI.

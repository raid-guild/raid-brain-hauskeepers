# Infrastructure Inventory & Dependencies Inputs

Working notes for Section 2 of the DAOhaus Maintenance SOP Packet: Infrastructure Inventory & Dependencies.

This doc collects the raw inputs needed to author the infrastructure dependency table, network/chain coverage map, and single points of failure callouts described in [009_sop_workstream_ideation.md](./009_sop_workstream_ideation.md).

## Current Hosting Provider(s) And Configs

Use this section to inventory every active hosting surface.

| Surface                | Provider | Environment | URL / Domain       | Repo Source             | Deployment Trigger                         | Owner / Access | Notes                    |
| ---------------------- | -------- | ----------- | ------------------ | ----------------------- | ------------------------------------------ | -------------- | ------------------------ |
| Admin app              | Railway  | Production  | admin.daohaus.club | `HausDAO/daohaus-admin` | Railway CI/CD on PR merge to `main` branch | TBD            | user-facing app surface. |
| Developer docs         | TBD      | Production  | docs.daohaus.club  | `HausDAO/dev-docs`      | Railway CI/CD on PR mergeh                 | TBD            |                          |
| User guide             | TBD      | Production  | guide.daohaus.club | `HausDAO/user-guide`    | Railway CI/CD on PR merge                  | TBD            |                          |
| Website / landing page | TBD      | Production  | daohaus.club       | `HausDAO/website`       | Railway CI/CD on PR merge                  | TBD            |                          |

**Enviroments**
haus-admin environment variable documentation
https://github.com/HausDAO/daohaus-admin/blob/master/docs/ENVIRONMENT.md

**Railway Billing owner**

- Odyssy is currently pating for this
- Cost is usage based. Reimbursment request can be made to DH infra safe

## Domain Registrar(s) And DNS Setup

Use this section to connect domain ownership, DNS hosting, and active records.

| Domain / Zone  | Registrar | DNS Provider | Renewal Date | Renewal Owner | Active Use             | Notes                                   |
| -------------- | --------- | ------------ | ------------ | ------------- | ---------------------- | --------------------------------------- |
| `daohaus.club` | GoDaddy   | Netlify      | August 2027  | Ven Gist      | Primary DAOhaus domain | Need to migrate off Ven owned registrar |

review 010_dns_catalog.md for full subdomain and dns record list. Can include high-level, relevant info in the SOP from that.

- [DNS Catalog](./010_dns_catalog.md)

## The Graph Deployment Details

Links to all subgraphs on supported networks here
https://docs.daohaus.club/subgraphs

Maintenance guides here
https://docs.daohaus.club/contributing/subgraphs

## RPC Providers In Use

Using Alchemy RPCs for all networks.

Odyssy (Sam) owned alchemy account

- Free tier

## Third-Party APIs And Services

Use this section to catalog external services required by the app, docs, or maintenance workflows.

| Service                                                         | Notes                                                                                                                                                                                                                                                                                                                        | Owner / Access                                                                         |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| [Alchemy](https://www.alchemy.com/)                             | RPC provider. Current deployed key is scoped to `*.daohaus.club`. This can be replaced with a free key at any time; DAOhaus is not using a paid account here.                                                                                                                                                                | Current deployed key owned by Odyssy / Sam. Future key can be owned by any maintainer. |
| [WalletConnect](https://walletconnect.com/) ID                  | Required for RainbowKit wallet integration. This can be replaced with a free key at any time; DAOhaus is not using a paid account here.                                                                                                                                                                                      | Free key obtained by Odyssy / Sam. Future key can be owned by any maintainer.          |
| [Sequence Token Indexer](https://sequence.xyz/products/indexer) | Token indexer service. New maintainers can obtain an account and update the key variable if needed.                                                                                                                                                                                                                          | Free key obtained by Odyssy / Sam.                                                     |
| Graph API                                                       | Uses `VITE_GRAPH_API_KEY`. Keys can be obtained in Subgraph Studio. DAOhaus-provided keys were created by the account outlined in the [subgraph maintenance docs](https://docs.daohaus.club/contributing/subgraphs). Current keys are scoped to `*.daohaus.club` and funded by the maintenance process outlined in the docs. | DAOhaus subgraph maintainer account.                                                   |

## DAOhaus Maintenance SOP Packet — Outline Draft

### Section 1: System Overview & Architecture

**Purpose:** Orient any maintainer (human or AI) to what DAOhaus is and how it hangs together.

**Inputs needed:**

- Current repo inventory (active vs. deprecated)
- Existing architecture docs
- Working input notes: [System Overview & Architecture Inputs](./012_system_overview_architecture_inputs.md)

**To be authored:**

- High-level system narrative — what DAOhaus does, who uses it, what "live" means for this protocol
- Architecture diagram: frontend → contracts → indexer → data flow
- Repository map: active repos clearly labeled, deprecated repos clearly marked, purpose of each

### Section 2: Infrastructure Inventory & Dependencies

**Purpose:** Complete picture of every infrastructure-related system DAOhaus depends on, including who can access it, how it is deployed, how domains are managed, and how indexing is maintained.

**Inputs needed:**

- Access holders for GitHub org, hosting platforms, DNS, API keys, The Graph, and related services
  - github: free, many owners who were previous contributors: https://github.com/orgs/HausDAO/people
  - railway: odyssy paid instance (dh infra reimburse)
  - refactory access - need to define how this is granted
  - dns is in odyssy control
- Current hosting provider(s), deployment configs, and CI/CD triggers
  - there is some of the [gitflow for ci here](https://github.com/raid-guild/raid-brain-hauskeepers/blob/master/docs/008_issue_and_git_flow.md)
  - admin app, website, docs, guide all in railway now
- Environment variable inventory
  - doc in the admin app
- Domain registrar(s), DNS providers, current record inventory, and renewal details
- The Graph deployment details, active subgraphs, billing/query balance process, and supported networks
- RPC providers and any third-party APIs or services (wallet connectors, token sequencers)
- Working input notes: [Infrastructure Inventory & Dependencies Inputs](./013_infrastructure_inventory_dependencies_inputs.md)

**To be authored:**

- Infrastructure dependency table: service → purpose → owner/contact → renewal/cost info → access requirements
- Access matrix: system → current holders → access level → how to gain/revoke access
- Deployment runbook for the admin app, website, guide, and docs sites
- Domain inventory with registrar, expiry, DNS provider, renewal owner, and active-use notes
- DNS record map and renewal SOP
- Network/chain coverage map: supported chains, active subgraphs, deployment IDs, and query balance status
- Subgraph operations runbook: deploy/update, monitor indexing health, and add to query balance
- Single points of failure callouts

**Subsections:**

#### Access & Credential Management

- Current access holders for each infrastructure system
- How to get new credentials or request access
  - see 013_infrastructure_inventory_dependencies_inputs.md
  - most dependencies are free tier and any contributor can get an account and get key
  - see doc for the graph details as it has the most restricted dependencies
- Onboarding checklist for a new maintainer
- Offboarding and access revocation checklist

#### Deployment & Hosting Operations

- Hosting platform details
- Deployment pipeline and CI/CD triggers
- Environment variable reference
- Deployment and rollback procedures

#### Domain & DNS Management

- Domain inventory
- Registrar ownership and renewal calendar
- DNS provider and active record map
- Renewal SOP and alert setup recommendation

#### The Graph Indexer Management

- Active subgraph deployments
- How to deploy/update a subgraph
- How to monitor indexing health
- How to monitor billing and add to query balance
- Most of the content can be found here: https://docs.daohaus.club/contributing/subgraphs

### Section 3: AI-Assisted Maintenance Workflows

**Purpose:** How the human maintainer works with the agentic systems set up in Workstream 3.

**Inputs needed:**

- Refactory environment overview and configuration
- GitHub issue management flow design
- Defined human-in-the-loop decision points
- Known recurring tasks: dependency updates, subgraph checks, deployment checks, issue triage, API monitoring, and activity reporting
- [See this doc for a start](https://github.com/raid-guild/raid-brain-hauskeepers/blob/master/docs/008_issue_and_git_flow.md)

**To be authored:**

- Overview of the AI maintenance system and what it handles autonomously vs. what escalates to a human
- Routine maintenance procedures performed by the AI maintenance system
- Recurring task schedule and expected outputs
- How recurring automation feeds into issue triage workflows
- Issue triage workflow: how issues enter, how they get labeled/routed, what the AI does, when human reviews
- Code analysis and PR assistance workflow
- Monitoring and escalation flow (what triggers an alert, how it surfaces, what human action looks like)
- How a maintainer monitors AI maintenance activity and knows what to expect

**Dependencies**

- Sam: This should mostly come out of the automation workstream

### Section 4: Stewardship Transition Guide

**Purpose:** How to hand off maintainership if/when that becomes necessary.

**Inputs needed:**

- All of the above sections (this is a synthesis/index section)

**To be authored:**

- Transition checklist: what a new maintainer needs access to, needs to read, needs to verify
- "State of the system" template — a snapshot document format to be filled out at time of transition
- Known risks and open items to communicate at handoff

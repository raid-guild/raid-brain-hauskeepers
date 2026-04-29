## DAOhaus Maintenance SOP Packet — Planning Outline

### Section 1: System Overview & Architecture

**Purpose:** Orient any maintainer (human or AI) to what DAOhaus is and how it hangs together.

**Inputs needed:**

- Current repo inventory (active vs. deprecated)
- Existing architecture docs

**To be authored:**

- High-level system narrative — what DAOhaus does, who uses it, what "live" means for this protocol
- Architecture diagram: frontend → contracts → indexer → data flow
- Repository map: active repos clearly labeled, deprecated repos clearly marked, purpose of each

**Dependencies**

- Sam: Architecture diagram and Repository map drafts will be produced on the Architecture & documentation workstream
- Sam: Add main website and docus website here

### Section 2: Infrastructure Inventory & Dependencies

**Purpose:** Complete picture of every external system DAOhaus depends on.

**Inputs needed:**

- Current hosting provider(s) and configs
- Domain registrar(s) and DNS setup
- The Graph deployment details
- RPC providers in use
- Any third-party APIs or services (wallet connectors, token sequencers)

**To be authored:**

- Infrastructure dependency table: service → purpose → owner/contact → renewal/cost info
- Network/chain coverage map (which chains, which subgraphs)
- Single points of failure callouts

**Dependencies**

- Sam: I'll take a pass at collecting these inputs from docs and earlier workstream output

### Section 3: Access & Credential Management

**Purpose:** Who has the keys to what, and how does access get transferred or revoked.

**Inputs needed:**

- Current access holders for: GitHub org, hosting platforms, DNS, any API keys
- How to get new credentials or request access

**To be authored:**

- Access matrix: system → current holders → access level → how to gain/revoke access
- Key rotation procedures
- Onboarding checklist for a new maintainer (what access do they need and how do they get it)
- Offboarding checklist

**Dependencies**

- Sam: I'll take a pass at collecting these inputs

### Section 4: Deployment & Hosting Operations

**Purpose:** Step-by-step procedures for deploying and updating live systems.

**Inputs needed:**

- Current deployment pipeline (CI/CD setup, what triggers what)
  - there is some of the [gitflow for ci here](https://github.com/raid-guild/raid-brain-hauskeepers/blob/master/docs/008_issue_and_git_flow.md)
- Hosting platform details (Railway)
- Environment variable inventory

**To be authored:**

- Deployment runbook for the admin app, website and docs sites
- Documentation site deployment procedure
- Environment variable reference

**Dependencies**

- Sam: The public docs and website updates workstream is a blocker here.

### Section 5: The Graph Indexer Management

**Purpose:** Keeping subgraph indexing healthy across supported networks.

**Inputs needed:**

- All active subgraph deployments (IDs, networks, hosted vs. decentralized)
- Document processes to monitor billing and top off query fee balances
- Most of the content can be found here: https://docs.daohaus.club/contributing/subgraphs

**To be authored:**

- Subgraph inventory table
- How to deploy/update a subgraph
- How to monitor indexing health
- How to add to query balance

### Section 6: Domain & DNS Management

**Purpose:** Keep domains registered and pointed correctly.

**Inputs needed:**

- All domains in use
- Registrar accounts
- DNS provider and current record inventory
- Renewal calendar

**To be authored:**

- Domain inventory with registrar, expiry, and renewal owner
- DNS record map
- Renewal SOP and alert setup recommendation

**Dependencies**

- Sam: I'll take a pass at collecting these inputs

### Section 7: Routine Maintenance Procedures

**Purpose:** The recurring tasks that keep things healthy

**Inputs needed:**

- We need to define this more in relation to the automation workstream
- Known recurring tasks (dependency updates, subgraph checks, etc.); **NEED TO DEFINE**

**To be authored:**

- Document what processes the automations perform and how they load into the traige workflows
- How a maintainer can monitor/what to expect

**Dependencies**

- Sam: This should mostly come out of the automation workstream

### Section 8: AI-Assisted Maintenance Workflows

**Purpose:** How the human maintainer works with the agentic systems set up in Workstream 3.

**Inputs needed:**

- Refactory environment overview and configuration
- GitHub issue management flow design
- Defined human-in-the-loop decision points
- [See this doc for a start](https://github.com/raid-guild/raid-brain-hauskeepers/blob/master/docs/008_issue_and_git_flow.md)

**To be authored:**

- Overview of the AI maintenance system and what it handles autonomously vs. what escalates to a human
- Issue triage workflow: how issues enter, how they get labeled/routed, what the AI does, when human reviews
- Code analysis and PR assistance workflow
- Monitoring and escalation flow (what triggers an alert, how it surfaces, what human action looks like)

**Dependencies**

- Sam: This should mostly come out of the automation workstream

### Section 9: Stewardship Transition Guide

**Purpose:** How to hand off maintainership if/when that becomes necessary.

**Inputs needed:**

- All of the above sections (this is a synthesis/index section)

**To be authored:**

- Transition checklist: what a new maintainer needs access to, needs to read, needs to verify
- "State of the system" template — a snapshot document format to be filled out at time of transition
- Known risks and open items to communicate at handoff

# DAOhaus Infrastructure Modernization & AI-assisted Maintenance Workflow Initiative

## Executive Summary

DAOhaus infrastructure has accumulated technical debt across its codebase, documentation, and operational processes over several years of active use.

This proposal funds a **one-time modernization and maintenance sprint executed by Raid Guild** to simplify the codebase, update dependencies, clean documentation, and document infrastructure operations. It also introduces **AI-assisted maintenance workflows** to support long-term sustainability with a combination of human oversight and agentic developer systems.

### What

The goal is to reduce complexity, clarify what is actively maintained, and make DAOhaus significantly easier to support over time.

The work includes:

- Consolidating and simplifying the active codebase
- Updating dependencies and resolving known issues
- Cleaning and restructuring documentation
- Creating maintenance SOPs and operational playbooks
- Reducing unnecessary repository and community surface area
- Introducing AI-assisted maintenance infrastructure

### Why

DAOhaus has supported thousands of organizations and remains live, functional infrastructure. However, the surrounding systems have become fragmented and harder to maintain.

This creates risks including:

- Growing technical debt and maintenance overhead
- Outdated dependencies and potential system fragility
- Unclear repository and documentation structure
- Difficulty onboarding new maintainers
- Undocumented operational knowledge

This initiative addresses these issues by making DAOhaus **simpler, more maintainable, and easier to operate**, while enabling future contributors—supported by AI-assisted workflows—to efficiently sustain the system.

---

## Scope

This initiative will be executed by **Raid Guild**, a collective of engineers and builders with deep experience supporting decentralized infrastructure and Ethereum ecosystem projects.

Raid Guild will perform a structured infrastructure audit, modernization effort, and documentation sprint to reduce maintenance complexity and prepare DAOhaus for long-term sustainability.

The work is organized into several workstreams.

### Workstreams

#### 1. Codebase Consolidation & Modernization

- Consolidate active packages into a simplified repository structure
- Preserve legacy repositories while clearly marking them as deprecated
- Update dependencies across active codebases
- Resolve known technical issues (e.g. wallet connection compatibility issues)
- Remove legacy SDK dependencies from the active application layer

The objective is to reduce technical surface area, simplify maintenance, and clearly identify active systems.

#### 2. Internal Architecture & Maintenance Documentation

Create structured internal documentation covering:

- Repository structure and system architecture
- Key design decisions
- Deployment processes
- Infrastructure dependencies
- Known constraints and edge cases
- System dependency maps

Documentation will be structured to support both **human maintainers and AI-assisted development tools**.

#### 3. AI-Assisted Maintenance Infrastructure

As part of the modernization effort, Raid Guild will introduce **agentic AI development tooling** designed to support long-term maintenance of DAOhaus.

This includes:

- Setup of an **agentic development environment**)
  - Raid Guild Dark Factory
  - Github issue management flows
- Configuration of AI agents for:
  - Issue triage
  - Code analysis
  - Implementation assistance
  - Infra monitoring and escalation
- Integration of these systems with the DAOhaus repository

These tools allow a single human maintainer to operate with significantly increased efficiency by delegating routine development tasks to structured AI workflows.

#### 4. Community Surface Area Reduction

- Discord cleanup
  - Archive unnecessary channels
  - Consolidate discussion to a small set of clear categories:
    - Legacy user support
    - Governance discussions
    - Announcements
    - AI Flow reporting (issue triage, api monitoring, activity reports)
- Mark unused repositories as deprecated
- Update READMEs to clearly identify active repositories
- Preserve legacy code for historical access
- Clarify which repositories are actively maintained
- Remove outdated SDK documentation
- Review and simplify User and Developer documentation
- Ensure public documentation reflects only active tools and systems

#### 5. Maintenance & Transition Readiness Packet

Raid Guild will produce a structured **DAOhaus Maintenance & Transition Readiness Packet** designed to support ongoing operations and future maintainers.

This packet will include:

- Codebase architecture overview
- Infrastructure diagrams
- Repository map with clear identification of active systems
- Maintenance SOPs and operational playbooks covering:
  - The Graph indexer management
  - Deployment and hosting processes
  - Domain management
  - Documentation hosting
  - Main website hosting
  - Access management procedures
- Documentation of **AI-assisted maintenance workflows**, including how maintainers utilize agentic systems for:
  - Issue triage
  - Code analysis and implementation
  - Testing and validation

This packet ensures DAOhaus infrastructure is **fully documented, reproducible, and maintainable**, while enabling efficient long-term support through both human and AI-assisted workflows.

It also prepares DAOhaus for potential future stewardship or maintenance transitions, without initiating any transfer of control.

---

# Timeline

6 weeks

The initiative will be structured as a **fixed-scope infrastructure modernization sprint** executed by Raid Guild.

---

# Budget

Budget will cover:

- Engineering work performed by Raid Guild contributors
- Documentation and infrastructure mapping
- AI-assisted maintenance environment setup
- Community Surface Area Reduction setup
- Operational playbook creation
- 3 Raid Guild Dvelopers/PM roles (Dekan, Sam, Other RG Developer)

**XX ETH**

Operational cost addition:

- **AI Tooling subscriptions for AI-assisted maintenance:**
  - Paid for with existing infra budget.

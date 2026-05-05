# **DAOhaus <> Dark Factory Opportunity**

## Summary

DAOhaus is exploring an initiative to modernize its infrastructure and long-term maintenance systems, and is considering engaging **Raid Guild’s Dark Factory** to execute the work.

Raid Guild will perform a structured infrastructure audit, modernization effort, and documentation sprint to reduce maintenance complexity and prepare DAOhaus for long-term sustainability.

The work is organized into several workstreams.

- Codebase Consolidation & Modernization
- Internal Architecture & Maintenance Documentation
- AI-Assisted Maintenance Infrastructure
- DAOhaus Community Surface Area Reduction
- Maintenance & Transition Readiness Packet / SOPs

## Deliverables

- **Simplified DAOhaus codebase**
  - Refactor monorepo
    - Preserve admin application
    - Update and simplify dependencies and tooling
    - Deprecate SDK structure
    - Resolve key bugs
  - Deprecate legacy repositories
  - Redefine deployment pipeline

- **Clear architecture & documentation**
  - System architecture and repository map
  - Deployment, infrastructure, and dependency documentation
  - LLM optimized guides and docs
  - Issue templates

- **AI-assisted maintenance system**
  - Agentic development environment setup (triage, coding, monitoring)
  - Integrated GitHub workflows for AI-assisted issue management
  - Human-in-the-loop maintenance processes

- **Reduced community & repo surface area**
  - Simplified GitHub structure with clear active systems
  - Cleaned and consolidated Discord channels
  - Cleaned and updated public documentation

- **Maintenance SOPs & playbooks**
  - Infrastructure management (hosting, domains, indexing, access)
  - Step-by-step operational procedures for maintainers
  - AI-assisted maintenance workflows and usage guidelines
  - Architecture overview and infrastructure diagrams
  - Repository map and system inventory
  - Complete SOPs and maintenance workflows

---

## Roles

| Workstream                     | Primary | Support/QA | Notes                                                                                  |
| ------------------------------ | ------- | ---------- | -------------------------------------------------------------------------------------- |
| Monk                           | EC      |            |                                                                                        |
| Simplified DAOhaus codebase    | Sam     | Dekan      | Support to help test ui and review code and iteration with maintenance machine testing |
| Architecture & documentation   | Sam     | Dekan      | Support to review docs and iterate with maintenance machine testing                    |
| AI-assisted maintenance system | Dekan   | EC/Sam     | Support to help with planning, testing. Any dev support                                |
| DH Comms Updates               | Sam     | Dekan      | Support setup and integration with maintenance machine                                 |
| Maintenance SOPs & playbooks   | EC      | Dekan/Sam  | Support to provide content and input for final SOP packet                              |

EC monk help with: timeline + high level epics

## Resources

[DAOhaus/PublicHaus Proposal Draft](https://hackmd.io/@CdDE9nbxQL-ViLycM4ARBA/HkowRjVKWx)

## Solution Considerations

**Agentic development environment**

- Requirements
  - Cron or webhook triggered workflows
  - Hosted environment to run ai development flows
  - Does this need any community knowledge or memory? Can it just use github issues for state?
- Explore tooling similar to Dark Factory (good knowledge gathering for RG)
  - Omniclaw
  - Nanoclaw
  - Paperclip (https://rg-paperclip-production.up.railway.app/HAU/issues/HAU-1)
  - NemoClaw (nvidia)
  - Google Agent Development Kit + Vertex Agent Builder
  - CrewAI
  - Warp Oz
  - Taskade

* How much UI should we consider vs. github/discord only?

**Hosting**

- Dedicated railway?

**LLM Docs**

- sero suggestions: https://www.youtube.com/watch?v=VgR66ybAtdg
- agent.md file tree
  - types
- coding rules for smaller files/less file sin each directory - rules fie
- tests (don't really want to)
- ensure we output changelogs

**Other outputs**

- How can we tell this story in RG?
  - Cohort to client work
  - Agentic software leaders
- How can we capture learning for future raids/sales
  - Tool evaluations + Best practices

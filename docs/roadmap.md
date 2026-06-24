# Roadmap

This roadmap communicates sequence, not dates. A milestone is complete only
when its documented outcomes work together; individual items may be explored
earlier when they reduce risk for later work.

## 1. Platform Foundation

**Planned:** Establish the shared control-plane foundation needed by every
module.

- Define platform administration and the always-multi-tenant hierarchy.
- Support IT and MSP tenants, including customer organizations and sites for
  MSPs.
- Design authentication, authorization, tenant isolation, and audit needs.
- Validate the dashboard authentication technology, including Better Auth.
- Define module lifecycle and first-party module boundaries.
- Design the agent enrollment, identity, communication, and task model.
- Prefer Go standard library packages only for implementation to reduce supply-chain risk; build shared code in-repo or as internally authored packages.
- Establish a minimal Docker Compose development and self-hosting path.

## 2. Cross-Platform Agent Baseline

**Planned:** Deliver a useful baseline on both Linux and Windows.

- Implement enrollment and stable device identity.
- Report heartbeat, operating-system details, and basic hardware and software
  inventory.
- Execute authorized commands or tasks and report their results.
- Define safe failure, reconnect, and task-status behavior.
- Exercise update and recovery design before relying on unattended agent
  upgrades.

Linux leads early implementation and day-to-day testing. Windows development
proceeds in parallel, and this milestone is not complete until the baseline is
available on both operating systems.

## 3. RMM Core

**Planned:** Turn the platform and agent into the first meaningful RootPlane
product milestone.

- Add hierarchical policies, default root policies, and conditional alerts.
- Target devices through organizations, departments, locations, groups, and
  tags.
- Schedule Bash and PowerShell scripts with history and optional expiration.
- Add reusable automation and custom fields.
- Introduce opt-in monitoring for selected security, account, session, and
  software-change events.
- Deliver initial email, Microsoft Teams, webhook, and Telegram notifications.
- Establish technician workflows and the foundation for an end-user portal.

## 4. Security, Lifecycle, and Asset Integrations

**Planned:** Build closely related operational modules on the RMM foundation.

- Add operating-system and third-party software patching.
- Assess cache-server feasibility for efficient site-level patch delivery.
- Add recurring vulnerability and misconfiguration assessment.
- Use CISA Known Exploited Vulnerabilities data as a prioritization signal.
- Expand automated inventory into asset-management records.
- Add warranty records, supported vendor lookups where feasible, and expiration
  notifications.
- Connect findings, patches, assets, warranties, alerts, and reports without
  making optional modules mandatory.

## 5. ITSM and Advanced Modules

**Planned/Candidate:** Expand RootPlane after the agent and RMM foundations are
proven.

- Add ticketing and an end-user support experience.
- Add manual and automatically populated documentation, including candidate
  network topology views.
- Investigate secure remote-control architecture and platform feasibility.
- Define billing boundaries and accounting-system integration needs.
- Investigate iOS and Android MDM feasibility and external requirements.
- Expand cross-module reporting from validated operator use cases.
- Define a security model and compatibility contract for third-party modules
  and integrations.

## Roadmap Review

Before promoting a candidate or open question into a committed milestone,
record the decision and its consequences in the [decision backlog](decisions.md).
Roadmap changes should preserve tenant isolation, cross-platform agent intent,
modularity, and a manageable self-hosting experience.

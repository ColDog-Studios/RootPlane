# Roadmap

This roadmap communicates sequence, not dates. A milestone is complete only
when its documented outcomes work together; individual items may be explored
earlier when they reduce risk for later work.

## 1. Platform Foundation

**Planned:** Establish the shared control-plane foundation needed by every
module.

- Document the AGPLv3-only licensing direction and the no-feature-gating
  commercial model.
- Define the dedicated-instance-first tenancy model for IT organizations and
  MSPs, including customer organizations and sites.
- Design authentication, authorization, tenant isolation, and audit needs.
- Design modern authentication support, including local accounts, MFA,
  passkeys, OIDC/OAuth2, and SAML.
- Establish PostgreSQL as the primary database and define stateless server
  behavior for future Kubernetes-style scaling.
- Establish the React and TypeScript dashboard stack.
- Define module lifecycle and first-party module boundaries.
- Design the agent enrollment, identity, communication, and task model.
- Establish the separate agent repository and cross-repo development workflow.
- Prefer Go standard library packages where practical to reduce supply-chain
  risk; allow mature third-party packages where they are safer than custom
  implementations, especially for authentication, cryptography, database
  access, and protocols.
- Establish a minimal Docker Compose development and self-hosting path.

## 2. Cross-Platform Agent Baseline

**Planned:** Deliver a useful baseline on both Linux and Windows.

- Implement enrollment and stable device identity.
- Report heartbeat, operating-system details, and basic hardware and software
  inventory.
- Classify device type in agent inventory, including Windows server, desktop,
  and laptop where detectable, and Linux desktop or laptop where detectable.
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
- Add Wake-on-LAN tasks with same-organization relay selection, same-site
  preference, cross-site policy controls, and audit history.
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
modularity, free software functionality, and a manageable self-hosting
experience.

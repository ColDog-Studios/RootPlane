# Decision Backlog

This backlog keeps unresolved choices visible without presenting them as
finished architecture. When a decision is made, its outcome and rationale
should be recorded before the corresponding documentation is relabeled.

| Topic | Status | Question to resolve |
| --- | --- | --- |
| License and commercial model | Committed | RootPlane will be AGPLv3-only free software. Paid offerings may provide hosting, signing, branding assistance, support, and convenience, but not restricted product functionality. |
| Deployment and tenancy model | Committed | RootPlane is dedicated-instance-first and tenant-aware internally. Shared multi-tenant hosting is a future candidate, not the default architecture target. |
| Repository topology | Committed | The agent will be developed in a separate repository from the server and dashboard. First-party content may remain in the server repo until it justifies a separate repository. |
| Primary database | Planned | PostgreSQL is the primary database. Schema, migrations, backup, HA, and operational guidance still need design. |
| Server implementation direction | Candidate | Is Go the best fit for the server while meeting authentication, scaling, deployment, and dependency-restraint goals? |
| Dashboard stack | Planned | React and TypeScript with Vite-style tooling is the preferred dashboard direction. The exact router, component approach, and build integration still need validation. |
| Agent implementation language | Candidate | Is Go the best fit for a small, cross-platform, privileged agent and its update model? |
| Dependency policy | Open Question | How will dependencies be selected, reviewed, pinned, inventoried, and updated without creating avoidable supply-chain risk? |
| Authentication architecture | Planned | How will local auth, server-side sessions, MFA, recovery codes, passkeys, OIDC/OAuth2, and SAML work without taking unnecessary dependencies or hand-rolling risky protocols? |
| Authorization model | Open Question | Which instance, organization, MSP-customer, technician, and end-user roles and scoped permissions are required? |
| Agent protocol | Open Question | How will enrollment, identity, task delivery, result reporting, reconnects, and protocol compatibility work securely? |
| Agent updates | Open Question | How will updates be signed, delivered, staged, rolled back, and recovered on Linux and Windows? |
| First-party content distribution | Open Question | How will built-in scripts, checks, policies, inventory definitions, signing, versioning, and agent compatibility work without forcing agent binary updates for content changes? |
| Wake-on-LAN relay policy | Open Question | How will RMM select eligible same-org relay agents, prefer same-site relays, use device type, allow cross-site fallback, rate-limit packets, and audit wake attempts? |
| Third-party modules | Candidate | What extension interfaces, permissions, isolation, versioning, and compatibility guarantees can be supported safely? |
| Mobile device management | Open Question | Which iOS and Android capabilities are feasible given enrollment, certificate, signing, vendor-service, and distribution requirements? |
| Patch cache servers | Candidate | How should caches be discovered, authorized, validated, invalidated, and operated at customer sites? |
| Remote control | Candidate | Which protocol and relay design can meet consent, unattended-access, audit, and cross-platform requirements? |
| Warranty providers | Open Question | Which vendor APIs and terms allow reliable automated coverage lookup? |
| Billing boundary | Open Question | Should RootPlane implement billing records and invoices, or provide usage data to accounting platforms? |
| Production deployment | Open Question | What topology, backup, scaling, high-availability, secret-management, and upgrade guidance is required beyond Docker Compose and managed dedicated instances? |
| Reporting architecture | Open Question | Which initial reports and export mechanisms are justified by real workflows across the first modules? |

## Decision Criteria

Architecture decisions should be evaluated against the following committed
direction:

- customer and organization data must remain correctly isolated;
- free software functionality must not depend on paid feature gates;
- both Linux and Windows must be supported by the universal-agent baseline;
- optional modules must not become accidental deployment requirements;
- privileged operations must be reviewable and designed for safe failure;
- common self-hosting should remain understandable and reproducible; and
- unnecessary dependencies and trusted components should be minimized.

Decision records should identify the problem, alternatives considered, chosen
direction, consequences, and any follow-up work. No unresolved table entry above
represents a finalized technology choice.

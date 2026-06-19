# Decision Backlog

This backlog keeps unresolved choices visible without presenting them as
finished architecture. When a decision is made, its outcome and rationale
should be recorded before the corresponding documentation is relabeled.

| Topic | Status | Question to resolve |
| --- | --- | --- |
| Agent implementation language | Candidate | Is Go the best fit for a small, cross-platform, privileged agent and its update model? |
| Dependency policy | Open Question | How will dependencies be selected, reviewed, pinned, inventoried, and updated without creating avoidable supply-chain risk? |
| Dashboard authentication | Candidate | Does Better Auth satisfy the chosen server stack, platform-admin boundary, tenant context, session, and deployment requirements? |
| Authorization model | Open Question | Which platform, tenant, MSP-customer, technician, and end-user roles and scoped permissions are required? |
| Agent protocol | Open Question | How will enrollment, identity, task delivery, result reporting, reconnects, and protocol compatibility work securely? |
| Agent updates | Open Question | How will updates be signed, delivered, staged, rolled back, and recovered on Linux and Windows? |
| Third-party modules | Candidate | What extension interfaces, permissions, isolation, versioning, and compatibility guarantees can be supported safely? |
| Mobile device management | Open Question | Which iOS and Android capabilities are feasible given enrollment, certificate, signing, vendor-service, and distribution requirements? |
| Patch cache servers | Candidate | How should caches be discovered, authorized, validated, invalidated, and operated at customer sites? |
| Remote control | Candidate | Which protocol and relay design can meet consent, unattended-access, audit, and cross-platform requirements? |
| Warranty providers | Open Question | Which vendor APIs and terms allow reliable automated coverage lookup? |
| Billing boundary | Open Question | Should RootPlane implement billing records and invoices, or provide usage data to accounting platforms? |
| Production deployment | Open Question | What topology, backup, scaling, high-availability, secret-management, and upgrade guidance is required beyond Docker Compose? |
| Reporting architecture | Open Question | Which initial reports and export mechanisms are justified by real workflows across the first modules? |

## Decision Criteria

Architecture decisions should be evaluated against the following committed
direction:

- tenant and customer data must remain correctly isolated;
- both Linux and Windows must be supported by the universal-agent baseline;
- optional modules must not become accidental deployment requirements;
- privileged operations must be reviewable and designed for safe failure;
- common self-hosting should remain understandable and reproducible; and
- unnecessary dependencies and trusted components should be minimized.

Decision records should identify the problem, alternatives considered, chosen
direction, consequences, and any follow-up work. No table entry above represents
a finalized technology choice.

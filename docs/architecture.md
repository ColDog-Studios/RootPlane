# Architecture Direction

This document records product-level architecture direction. It intentionally
does not define wire protocols, database schemas, or security guarantees that
have not yet been designed.

## Control Plane and Tenancy

**Committed:** RootPlane will always operate as a multi-tenant control plane.
A separate platform-administration backend will manage tenants and
platform-wide operations.

RootPlane will support two tenant types:

- **IT tenant:** Represents an organization managing its own environment.
- **MSP tenant:** Represents a service provider managing customer
  organizations and their sites.

The intended organizational hierarchy is:

```text
RootPlane platform
├── Platform administration
└── Tenant
    ├── IT organization
    │   └── Sites / locations, departments, groups, users, and devices
    └── MSP
        └── Customer organizations
            └── Sites / locations, departments, groups, users, and devices
```

**Planned:** Authorization and data access will respect tenant and customer
organization boundaries. The exact role and permission model is still an open
design decision.

Hosting does not introduce another tenant type. Self-hosted, MSP-operated, and
hosted-service deployments use the same tenancy concepts.

## Modular Platform

**Committed:** RootPlane capabilities will be divided into first-party modules
that deployments can enable according to need. Modules will build on shared
platform services such as authentication, authorization, tenancy, device
identity, notifications, and reporting.

**Planned:** Integrations between enabled modules will exchange useful domain
information without requiring every related module. Examples include:

- vulnerability findings informing patch prioritization;
- agent inventory populating asset and documentation records;
- warranty expiration creating alerts or notifications; and
- ticketing linking support work to users, devices, and organizations.

**Candidate:** Third-party modules and integrations will be supported after
extension boundaries and their security model are defined.

## Universal Agent

**Committed:** One cross-platform agent will provide common management
capabilities for Linux and Windows devices. The baseline is expected to include
enrollment, stable device identity, heartbeat, inventory collection, and secure
command or task execution.

Linux will lead early development and testing. Windows work will proceed in
parallel, and both platforms are required for completion of the baseline agent
milestone. Operating-system-specific features may use platform-specific
implementations behind shared control-plane concepts.

**Candidate:** Go is being considered for the agent. No implementation language
has been finalized.

**Open Question:** The agent protocol, privilege boundaries, update mechanism,
offline behavior, and dependency policy require dedicated design decisions.

## Server Deployment

**Planned:** RootPlane will support containerized server deployment through
Docker and a straightforward Docker Compose configuration. The default setup
should minimize required configuration while still making security-sensitive
settings explicit.

**Open Question:** Production topology, scaling, backup, high availability,
secret management, and upgrade behavior remain to be designed.

## Authentication and Administration

**Candidate:** Better Auth is the preferred authentication candidate for the
dashboard. Its fit with the selected server stack, platform-administration
boundary, tenant context, and authorization model must be validated before it
is treated as final.

**Planned:** Platform administrators, tenant administrators, technicians, and
end users will have distinct experiences appropriate to their responsibilities.
The end-user portal may expose ticketing and other user-facing modules without
granting access to technician workflows.

## Cross-Cutting Services

The following shared services are expected to emerge as modules are designed:

- **Planned:** Notification delivery for email, Microsoft Teams, webhooks, and
  Telegram.
- **Planned:** Reporting across enabled modules.
- **Planned:** Scoped objects and targeting for tenants, customer organizations,
  departments, sites or locations, groups, users, and devices.
- **Open Question:** Audit logging, event transport, retention, observability,
  and extension APIs.

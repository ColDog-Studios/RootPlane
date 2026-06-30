# Architecture Direction

This document records product-level architecture direction. It intentionally
does not define wire protocols, database schemas, or security guarantees that
have not yet been designed.

## Control Plane and Tenancy

**Committed:** RootPlane will be tenant-aware internally, but the primary
deployment model is dedicated instances. A deployment may serve one internal IT
organization, one MSP managing many customer organizations, or a future hosted
operator managing multiple independent tenants.

RootPlane will support two primary operating shapes:

- **IT organization:** Represents an organization managing its own environment.
- **MSP:** Represents a service provider managing customer organizations and
  their sites.

The intended dedicated-instance hierarchy is:

```text
RootPlane instance
|-- Instance administration
`-- Organization or MSP
    |-- IT organization
    |   `-- Sites / locations, departments, groups, users, and devices
    `-- MSP
        `-- Customer organizations
            `-- Sites / locations, departments, groups, users, and devices
```

**Planned:** Authorization and data access will respect instance, organization,
MSP customer, site, group, user, and device boundaries. The exact role and
permission model is still an open design decision.

Shared multi-tenant hosting is a future candidate, not the default planning
assumption. The architecture should avoid decisions that make it impossible,
but early product and hosting work should optimize for self-hosted and managed
dedicated instances.

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
enrollment, stable device identity, heartbeat, inventory collection, device
type classification, and secure command or task execution.

Linux will lead early development and testing. Windows work will proceed in
parallel, and both platforms are required for completion of the baseline agent
milestone. Operating-system-specific features may use platform-specific
implementations behind shared control-plane concepts.

**Planned:** The agent will classify its device type as part of inventory.
Windows agents should distinguish at least server, desktop, and laptop where
platform data allows. Linux agents should distinguish at least desktop and
laptop where platform data allows, with server or unknown classifications used
when reliable detection is not available.

**Committed:** The agent will be developed in a separate repository from the
server and dashboard. The server repository will own the API contract,
dashboard, deployment path, and fake-agent tests. The agent repository will own
agent runtime code, platform-specific implementations, packaging, update logic,
and fake-server tests.

**Candidate:** Go is the preferred implementation direction for the agent. The
final implementation language remains a decision record until the first
prototype validates packaging, service integration, updates, and platform APIs.

**Open Question:** The agent protocol, privilege boundaries, update mechanism,
offline behavior, and dependency policy require dedicated design decisions.

## RMM Network Actions

**Planned:** Wake-on-LAN will be a built-in RMM capability rather than a
separate module. Wake requests will stay inside organization boundaries and use
eligible online agents as relays.

Relay selection should prefer agents in the target device's site. If no
same-site relay is online, policy may allow approved cross-site relays within
the same organization, which is useful for environments where some sites share
subnets or selected IT devices can reach other subnets.

**Planned:** Device type should influence relay eligibility. Servers and
desktops are stronger default relay candidates than laptops or remote devices.
Operators should be able to override relay eligibility through policy because
network layout, VPN use, Wi-Fi, and device trust vary by environment.

**Open Question:** The exact relay selection algorithm, rate limits, packet
strategy, broadcast address handling, audit fields, and success detection need
design before implementation.

## Server Deployment

**Planned:** RootPlane will support containerized server deployment through
Docker and a straightforward Docker Compose configuration. The default setup
should minimize required configuration while still making security-sensitive
settings explicit.

**Committed:** PostgreSQL is the planned primary database. Server application
replicas should be stateless where practical so a deployment can scale behind a
load balancer in Kubernetes or similar infrastructure. Sessions, tasks, audit
events, agent state, and operational data should live in PostgreSQL or another
explicit shared service rather than in local process memory.

**Planned:** Production topology, scaling, backup, high availability, secret
management, and upgrade behavior remain to be designed beyond the dedicated
instance baseline.

## Authentication and Administration

**Committed:** RootPlane needs modern enterprise authentication options,
including MFA, passkeys, OIDC, OAuth2 provider integrations, and SAML. Social
login providers such as Microsoft, Google, and GitHub are useful later, but
generic OIDC/SAML support is more important than consumer login coverage.

**Planned:** The server should be Go-first, with mature third-party packages
allowed for authentication, cryptography, database access, and protocol work
where hand-rolled code would be riskier. Browser sessions should use
server-side session state rather than self-contained dashboard JWTs by default.

**Planned:** Instance administrators, organization administrators, MSP
technicians, customer-scoped technicians, and end users will have distinct
experiences appropriate to their responsibilities. The end-user portal may
expose ticketing and other user-facing modules without granting access to
technician workflows.

## Dashboard

**Planned:** The dashboard will be a React and TypeScript application served by
the RootPlane control plane. Vite, TanStack Query, TanStack Table, Tailwind CSS,
and locally owned component code are the preferred frontend direction unless a
prototype proves a better fit.

## Licensing and Commercial Model

**Committed:** RootPlane will be AGPLv3-only free software. Paid or supporter
offerings should not restrict product functionality. Acceptable paid offerings
include managed dedicated hosting, official code-signed agent builds, branded
build assistance, support, deployment assistance, release provenance, and
similar services.

## Cross-Cutting Services

The following shared services are expected to emerge as modules are designed:

- **Planned:** Notification delivery for email, Microsoft Teams, webhooks, and
  Telegram.
- **Planned:** Reporting across enabled modules.
- **Planned:** Scoped objects and targeting for organizations, MSP customers,
  departments, sites or locations, groups, users, and devices.
- **Open Question:** Audit logging, event transport, retention, observability,
  and extension APIs.

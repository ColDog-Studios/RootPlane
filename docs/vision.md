# Product Vision

## Purpose

**Committed:** RootPlane will be an open, modular control plane for managing,
supporting, and securing IT environments through one universal endpoint agent.
It should give internal IT teams and MSPs a coherent alternative to assembling
many disconnected management products.

RootPlane is not intended to make every capability mandatory. A deployment
should be able to use a focused RMM configuration or enable adjacent modules as
its needs grow.

**Committed:** RootPlane will be AGPLv3-only free software. All product
functionality should remain available from source without paid feature gates.
Commercial offerings should be services, trust, packaging, hosting, support, or
branding assistance rather than restricted product capabilities.

## Who RootPlane Serves

- **Committed - Internal IT teams:** Manage the users, devices, departments,
  locations, and services belonging to their organization.
- **Committed - MSPs:** Manage multiple customer organizations and sites while
  maintaining clear customer boundaries.
- **Planned - Technicians:** Monitor devices, respond to alerts and tickets,
  run approved automation, and access the modules permitted by their role.
- **Planned - End users:** Use a separate portal for support and other
  user-facing module experiences.
- **Planned - Self-hosters and service operators:** Run RootPlane for their own
  organization, their customers, or as managed dedicated instances.

Hosting is a deployment model, not a special tenant type. The primary hosted
commercial path is managed dedicated instances. Shared multi-tenant hosting is
a future candidate only after the product and operational model justify it.

## Product Principles

### One agent, shared capabilities

**Committed:** Managed Linux and Windows devices will run one RootPlane agent.
Modules should reuse its enrollment, identity, inventory, communication, and
execution foundations instead of installing a separate agent for every feature.

**Committed:** The agent will be developed in a separate repository from the
server and dashboard so its release cadence, packaging, signing, update logic,
and dependency review can be managed independently.

Linux will lead early implementation and testing, while Windows support will
be developed in parallel to reach the initial cross-platform baseline. Platform
depth may differ temporarily where operating-system capabilities differ.

### Modular by design

**Committed:** First-party capabilities will be divided into modules that can
be enabled according to a deployment's needs.

**Candidate:** Third-party modules and integrations may extend RootPlane. Their
trust model, compatibility guarantees, and extension boundaries remain open
design work.

### Useful connections between modules

**Planned:** Enabled modules should cooperate without becoming inseparable. For
example, vulnerability findings can inform patch priority, device inventory can
populate asset records and documentation, and warranty state can produce RMM
alerts.

### Straightforward self-hosting

**Planned:** A standard server deployment will be available through Docker and
Docker Compose. The common path should use a small, understandable
configuration rather than requiring many incidental settings before the service
can start.

**Planned:** RootPlane should also support managed dedicated instances and
larger deployments that run stateless application replicas with shared state in
PostgreSQL.

### Security and supply-chain restraint

**Committed:** Security is a design constraint because the control plane and
agent will hold privileged access to managed environments.

**Committed:** RootPlane should minimize unnecessary third-party dependencies,
especially in the agent, to reduce supply-chain exposure and maintenance risk.
Exceptions are expected where well-reviewed packages are the safer choice,
including authentication, cryptography, database drivers, and protocol
implementations that should not be hand-rolled.

Security-sensitive behavior-including enrollment, authorization, command
execution, secret handling, updates, tenant isolation, SSO, MFA, and
passkeys-must be designed and reviewed before implementation claims are made.

### No feature-gated open core

**Committed:** RootPlane's free software distribution should include the same
product functionality as any paid offering. Paid offerings may provide
code-signed builds, managed hosting, branded build assistance, support,
deployment help, release provenance, and similar services that do not hide or
disable product features.

### Reporting across the platform

**Planned:** Reporting will span enabled modules so operators can understand
device health, operational activity, vulnerabilities, patch state, assets,
warranties, support work, and other relevant data from a consistent interface.

## Initial Product Focus

**Planned:** RootPlane's first meaningful release will combine a Linux and
Windows universal-agent baseline with core RMM workflows. Later milestones will
build deeper patching, vulnerability, asset, warranty, ITSM, and advanced
management capabilities on that foundation.

See the [roadmap](roadmap.md) for sequencing and the [module catalog](modules.md)
for the intended capability set.

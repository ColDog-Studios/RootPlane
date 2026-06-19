# Product Vision

## Purpose

**Committed:** RootPlane will be an open, modular control plane for managing,
supporting, and securing IT environments through one universal endpoint agent.
It should give internal IT teams and MSPs a coherent alternative to assembling
many disconnected management products.

RootPlane is not intended to make every capability mandatory. A deployment
should be able to use a focused RMM configuration or enable adjacent modules as
its needs grow.

## Who RootPlane Serves

- **Committed — Internal IT teams:** Manage the users, devices, departments,
  locations, and services belonging to their organization.
- **Committed — MSPs:** Manage multiple customer organizations and sites while
  maintaining clear tenant boundaries.
- **Planned — Technicians:** Monitor devices, respond to alerts and tickets,
  run approved automation, and access the modules permitted by their role.
- **Planned — End users:** Use a separate portal for support and other
  user-facing module experiences.
- **Planned — Self-hosters and service operators:** Run RootPlane for their own
  organization, their customers, or as a hosted service.

Hosting is a deployment model, not a special tenant type. The same platform
model should work whether RootPlane is operated privately or offered as a
service.

## Product Principles

### One agent, shared capabilities

**Committed:** Managed Linux and Windows devices will run one RootPlane agent.
Modules should reuse its enrollment, identity, inventory, communication, and
execution foundations instead of installing a separate agent for every
feature.

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
Docker Compose. The common path should use a small, understandable configuration
rather than requiring many incidental settings before the service can start.

### Security and supply-chain restraint

**Committed:** Security is a design constraint because the control plane and
agent will hold privileged access to managed environments.

**Candidate:** RootPlane should minimize unnecessary third-party dependencies,
especially in the agent, to reduce supply-chain exposure and maintenance risk.
The exact dependency policy and review process are not yet defined.

Security-sensitive behavior—including enrollment, authorization, command
execution, secret handling, updates, and tenant isolation—must be designed and
reviewed before implementation claims are made.

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

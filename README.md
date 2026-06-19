# RootPlane

RootPlane is an open, modular control plane for managing, supporting, and
securing IT environments through one universal agent.

The project is intended for both internal IT teams and managed service
providers (MSPs). It combines remote monitoring and management with optional
capabilities such as patching, vulnerability management, asset management,
ticketing, documentation, remote control, warranty tracking, billing, mobile
device management, and reporting.

> [!NOTE]
> RootPlane is currently in the planning and design stage. The documentation
> describes product direction, not a released or production-ready system.

## Direction

- **Committed:** RootPlane will use an always-multi-tenant control plane with
  distinct IT and MSP tenant types.
- **Committed:** A cross-platform universal agent will provide shared device
  management capabilities on Linux and Windows.
- **Committed:** Features will be modular so deployments can enable only the
  capabilities they need.
- **Planned:** The first meaningful milestone will pair the universal agent
  with core RMM functionality.
- **Planned:** Self-hosting will be supported through a straightforward Docker
  Compose deployment.

Linux will lead early agent development because it offers a convenient testing
environment, but the initial agent baseline requires both Linux and Windows.

## Documentation

- [Product vision](docs/vision.md)
- [Architecture direction](docs/architecture.md)
- [Module catalog](docs/modules.md)
- [Roadmap](docs/roadmap.md)
- [Decision backlog](docs/decisions.md)

The labels **Committed**, **Planned**, **Candidate**, and **Open Question** are
used throughout these documents to separate settled direction from ideas that
still need investigation.

## Contributing

RootPlane is documentation-first while its initial architecture and product
boundaries are established. Discussion and contributions should use the
decision backlog and roadmap to avoid treating exploratory ideas as finalized
designs.

## License

RootPlane is licensed under the [GNU Affero General Public License v3.0](LICENSE).

# Module Catalog

This catalog describes intended first-party capabilities. A maturity label is
not a release promise:

- **Committed:** Foundational product direction.
- **Planned:** Intended capability with sequencing on the roadmap.
- **Candidate:** A useful idea that still needs validation or design.
- **Open Question:** Feasibility or product boundaries are unresolved.

## Summary

| Module | Maturity | Purpose |
| --- | --- | --- |
| RMM | Planned - initial focus | Monitor and manage endpoint fleets through policies and automation. |
| Patching | Planned | Manage operating-system and third-party software updates. |
| Vulnerability management | Planned | Find and prioritize software, OS, and configuration risks. |
| Asset management | Planned | Maintain device and asset inventory from automated and manual sources. |
| Warranty tracking | Planned | Track vendor coverage and upcoming expirations. |
| Ticketing | Planned | Coordinate support requests and technician work. |
| Documentation | Planned | Combine manual knowledge with automatically discovered environment data. |
| Remote control | Candidate | Provide technician-to-device remote assistance. |
| Reporting | Planned | Report across enabled RootPlane modules. |
| Billing | Candidate | Support billing workflows associated with managed services. |
| MDM | Open Question | Manage supported iOS and Android devices where platform requirements permit. |

## RMM

**Planned - initial focus:** Remote monitoring and management will be the first
major module built on the universal agent.

Intended capabilities include:

- policies with parent-child inheritance and default root policies;
- conditional alerts;
- scheduled automation and scheduled tasks;
- targeting by device, organization or MSP customer, department, site or
  location, and group;
- built-in Wake-on-LAN tasks that use approved online agents as same-org
  relays;
- Bash and PowerShell script libraries;
- task schedules with optional expiration;
- custom fields for devices, organizations, departments, and locations;
- system tags;
- technicians and role-appropriate access;
- notification channels including email, Microsoft Teams, webhooks, and
  Telegram; and
- opt-in monitoring for events such as BitLocker or TPM state changes, user
  account changes, login activity, and software installation, removal, or
  updates.

Wake-on-LAN relay behavior should respect organization isolation. Same-site
agents are preferred, and at least one same-site relay should be selected when
same-site relays are online. If none are online, policy may allow approved
cross-site relays within the same organization. Device type should inform
default relay eligibility: servers and desktops are stronger candidates than
laptops, remote devices, Wi-Fi clients, or other devices that operators mark as
unsuitable relays.

**Planned integrations:** OS and third-party patching, warranty-expiration
alerts, asset inventory, vulnerability findings, and cross-module reporting.

## Patching

**Planned:** Patching will cover operating-system and third-party software
updates. When vulnerability management is enabled, known risk and exploitation
data should help operators prioritize remediation.

**Candidate:** Local cache servers could reduce repeated update downloads across
managed sites. Cache discovery, trust, and content-validation behavior are not
yet designed.

## Vulnerability Management

**Planned:** The module will use recurring privileged assessment to detect
known software and operating-system vulnerabilities and relevant
misconfigurations. "Continuous" describes repeated assessment rather than a
promise of instantaneous detection.

**Planned:** CISA's Known Exploited Vulnerabilities catalog will contribute to
prioritization when a finding matches a known exploited issue.

**Open Question:** Scan methods, data sources, privilege boundaries, frequency,
and the division of work between agent and server require design.

## Asset Management

**Planned:** Asset management will combine automatically collected endpoint
inventory with operator-maintained records. Assets should be linkable to their
organization, department, location, assigned user, documentation, support work,
and warranty where those modules are enabled.

## Warranty Tracking

**Planned:** Warranty tracking will record coverage and notify operators before
expiration. Initial vendor candidates are Dell, Lenovo, Toshiba, HP, and
Microsoft.

**Open Question:** Vendor API availability and terms will determine which
lookups can be automated. Warranty tracking may remain a distinct module while
integrating closely with RMM and asset management.

## Ticketing

**Planned:** Ticketing will support requests from end users and work managed by
technicians. Tickets should be linkable to organizations, MSP customers, users,
devices, assets, and relevant documentation.

**Open Question:** Queues, service agreements, approval workflows, and billing
connections are not yet specified.

## Documentation

**Planned:** Documentation will support manual knowledge while incorporating
automatically discovered data where practical. Candidate generated views
include asset details and network maps or topology assembled from agent and
inventory data.

**Open Question:** Document format, version history, secrets handling, access
control, and the boundary between documentation and asset management require
design.

## Remote Control

**Candidate:** A streamer/player capability could provide interactive remote
assistance through the universal-agent ecosystem.

**Open Question:** Protocol choice, relay infrastructure, consent, unattended
access, recording, clipboard and file transfer, and platform support require a
security and feasibility study.

## Reporting

**Planned:** Reporting will provide shared views across enabled modules,
including device health, automation, patching, vulnerabilities, assets,
warranties, and support activity. Initial reports should grow from actual
module use cases rather than from a generic report-builder requirement.

## Billing

**Candidate:** Billing may support MSP workflows based on customers, services,
assets, users, or support activity.

**Open Question:** RootPlane may generate invoices itself or integrate with
specialized accounting and payment systems; that boundary is not decided.

## Mobile Device Management

**Open Question:** iOS and Android MDM remain feasibility investigations rather
than committed deliverables. Enrollment programs, certificates, signing,
platform policy, vendor services, and distribution requirements may limit what
an open self-hosted implementation can provide.

If feasible, mobile management should integrate with the shared inventory,
policy, user, and reporting concepts without weakening platform security.

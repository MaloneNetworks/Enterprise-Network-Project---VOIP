# Enterprise Network & VoIP Lab

A work-in-progress enterprise networking lab built with **GNS3** and **VMware Workstation**. The goal is to design, implement, secure, troubleshoot, and repeatedly rebuild a multi-layer network with switching, routing, firewalls, a DMZ, branch connectivity, and VoIP.

> **Project status:** In development. Planned features are not considered complete until they are configured and verified. This repository is being built alongside the lab.

## Start here

1. Read the [project overview](00-start-here/project-overview.md).
2. Review the [design documents](01-design/):
   - [Topology and diagrams](01-design/topology/README.md)
   - [Device inventory](01-design/device-inventory.md)
   - [IP addressing and VLAN plan](01-design/ip-addressing.md)
   - [Port and cable register](01-design/port-mapping.md)
3. Follow the [build instructions](02-build/BUILD-INSTRUCTIONS.md). The other build documents are supporting references until their overlap is consolidated.
4. Store sanitized device configurations in [03-configurations](03-configurations/).
5. Follow the [VoIP documentation](04-voip/README.md) when the network path is ready.
6. Use the [test plan](05-testing/test-plan.md) to verify each stage.
7. Explore the [troubleshooting lab](06-troubleshooting/network-chaos-lab/README.md) after the base network is stable.

## Repository map

| Section | Purpose |
|---|---|
| [00 - Start Here](00-start-here/) | Project overview and orientation |
| [01 - Design](01-design/) | Topology, device inventory, ports, IPs, and VLANs |
| [02 - Build](02-build/) | Ordered implementation instructions and planning |
| [03 - Configurations](03-configurations/) | Device configuration files, organized by device role |
| [04 - VoIP](04-voip/) | CME, softphone, extensions, and voice implementation |
| [05 - Testing](05-testing/) | Test cases and verification evidence |
| [06 - Troubleshooting](06-troubleshooting/) | Controlled faults and recovery exercises |
| [07 - Logs & Evidence](07-logs-evidence/) | Build logs, screenshots, and milestone evidence |
| [08 - References](08-references/) | Supporting media and external references |

## Lab scope

The intended environment includes:

- Redundant core switching and distribution/access layers
- Departmental VLANs and inter-VLAN routing
- WAN/ISP connectivity and branch-office routing
- Cisco ASA and FortiGate firewalling
- DMZ and internal server networks
- A dedicated voice VLAN with Cisco CME evaluation and Windows softphone
- Repeatable troubleshooting exercises, eventually supported by Python automation

## Documentation rules

- **Design is not implementation.** A proposed address, link, or feature must not be presented as configured.
- **Use explicit status labels:** Planned, Connected, Configured, Tested, or Verified.
- **Keep one authoritative record for each subject.** The IP/VLAN plan owns addressing; the port register owns cable endpoints; the device inventory owns device details.
- **Verify before documenting as complete.** Capture command output, screenshots, or test results.
- **Protect the lab and credentials.** Keep the lab isolated and remove passwords, keys, tokens, and other secrets from files before committing.

## Current topology

The current design snapshot is [topology version 2.0](01-design/topology/v2.0.png). It is a design reference, not proof that every pictured component is configured or operational. The editable draw.io source and detailed multi-page cut sheet will be added when they are created and verified.

## Tools

- GNS3
- VMware Workstation
- Cisco IOS / IOU images
- Cisco ASA and FortiGate images
- Windows 11 virtual machine

This repository will evolve as the lab is built. Folder placeholders are intentional where implementation work has not reached that stage.

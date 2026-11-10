# Enterprise Network & VoIP Project

A hands-on enterprise networking lab built with **GNS3** and **VMware Workstation**. This repository documents the design, implementation, validation, and troubleshooting of a segmented enterprise network with switching, routing, perimeter security, a DMZ, branch connectivity, and a VoIP environment.

> **Project status:** Planning and environment preparation. Features remain planned until configured and verified.

## Project goals
- Design and document an enterprise network topology.
- Implement VLAN segmentation and Layer 2 switching.
- Build Layer 3 routing and gateway redundancy.
- Configure firewall boundaries and a DMZ.
- Establish branch connectivity.
- Evaluate and deploy a compatible Cisco CME/VoIP solution.
- Validate the environment with repeatable tests.
- Publish sanitized configurations, diagrams, and implementation evidence.

## Current lab environment

| Component | Platform / candidate | Status |
|---|---|---|
| Network simulation | GNS3 | In use |
| Virtualization | VMware Workstation | In use |
| Endpoint VM | Windows 11 | Installed |
| CME router | Cisco 3745 / IOS 12.4(25d) candidate | Compatibility and storage validation pending |
| VoIP endpoint | Cisco IP Communicator or compatible softphone | Not installed |
| Other network appliances | Existing GNS3 devices | Inventory pending |

## Current design notes

| Item | Proposed value | State |
|---|---|---|
| Voice VLAN | VLAN 30 | Proposed; verify against topology |
| Voice subnet | `10.10.30.0/24` | Proposed |
| Voice gateway | `10.10.30.1` | Proposed |
| CME candidate address | `10.10.30.10` | Proposed |
| VMware segment | `VOIP-LAB` | Created |
| Windows phone VM | `VOIP-PHONE-01` | Windows installed |

These are planning notes, not confirmed active settings. Final addressing and gateway/DHCP ownership will be validated before configuration.

## Repository map

- [diagrams/](diagrams/) — enterprise, logical, and VoIP topology diagrams
- [documentation/](documentation/) — design, inventory, addressing, port mapping, and roadmap
- [configurations/](configurations/) — sanitized device configurations
- [voip/](voip/) — CME, DHCP/TFTP, endpoints, and registration notes
- [testing/](testing/) — test plans, results, and troubleshooting
- [screenshots/](screenshots/) — milestone evidence
- [media/](media/) — demonstration and walkthrough links

## Implementation workflow

1. Inventory appliances, interfaces, and existing links.
2. Finalize addressing, VLANs, and port assignments.
3. Implement and validate switching.
4. Implement and validate routing and redundancy.
5. Implement firewall and DMZ controls.
6. Implement branch connectivity.
7. Validate voice network and CME compatibility.
8. Deploy endpoints and test calls.
9. Capture evidence and publish documentation.

## Evidence and security

For each milestone, save sanitized configurations, verification output, topology screenshots, actual test results, and troubleshooting notes.

**Never commit** passwords, private keys, tokens, personal data, proprietary IOS images, or licensed firmware. Review screenshots and configuration files before publishing.

## Project status

- [Implementation roadmap](documentation/implementation-roadmap.md)
- [Project overview](documentation/project-overview.md)
- [Device inventory](documentation/device-inventory.md)
- [IP addressing plan](documentation/ip-addressing.md)
- [Port mapping](documentation/port-mapping.md)
- [VoIP implementation notes](voip/README.md)
- [Test plan](testing/test-plan.md)

Independent educational lab. Product names and trademarks belong to their respective owners; no affiliation or endorsement is implied.

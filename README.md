# Enterprise Network & VoIP Lab

Welcome to my Enterprise Network & VoIP lab. I'm building an enterprise-style network using **GNS3**, **Cisco CML Personal**, and **VMware Workstation** to get hands-on experience with networking, security, virtualization, and voice services.

The lab is a work in progress. I'll document the design, configuration steps, troubleshooting, and test results as I build it.

## Current network design

**Starting baseline: Enterprise Network v1.4**

Baseline v1.4 is the current reference for the lab. The design includes:

- Dual ISP connections and an HQ edge router
- Cisco ASA perimeter firewall and FortiGate internal firewall
- Redundant Layer 3 core switches, plus distribution and access layers
- Separate VLANs for administration, engineering, voice, servers, management, and the branch
- A DMZ for public-facing services
- A branch office connected over GRE/IPsec
- Cisco CME for VoIP
- A connection between the GNS3 and Cisco CML environments

The diagrams below show the planned layout and how the lab environments fit together. They are design references, not a claim that every device and feature is already configured. I'll update them as the build changes.

### Enterprise topology

![Enterprise Network Baseline v1.4](01-design/topology/Enterprise_Network_BASELINE_v1.4.png)

### Network cut sheet

The cut sheet puts the key details in one place: VLANs, subnets, gateways, WAN addressing, firewall interfaces, server addresses, and device inventory.

![Enterprise Network Cut Sheet](01-design/topology/Enterprise%20Network%20Cut%20Sheet.png)

### Cisco CML and GNS3 integration

This close-up shows the CME-side connection from **R-CME-01** through **R1** toward the external Cisco CML network.

![CME-to-Cisco CML connection detail](01-design/topology/CME%20from%20CML.png)

The wider diagram shows the overall GNS3-to-Cisco CML connection, including the external connector, transit router, switch, and server connections.

![Cisco CML–GNS3 Integration Diagram](01-design/topology/Cisco-CML-GNS3-Integration.png)

The transit build has its own repository: [Cisco CML–GNS3 Transit Network](https://github.com/MaloneNetworks/Cisco-CML_GNS3-Transit-Network). It documents the VMware LAN Segment, Cisco CML bridge, GNS3 Cloud connection, and successful ping tests in both directions across the `10.255.255.0/30` link.

### Design documents

- [Topology documentation](01-design/topology/README.md)
- [IP addressing and VLAN plan](01-design/ip-addressing.md)
- [Port mapping](01-design/port-mapping.md)
- [Device inventory](01-design/device-inventory.md)
- [Previous topology versions](01-design/topology/)

## What the lab covers

The goal is to build and work with several parts of an enterprise network:

- **Switching and VLANs** — segment departments and devices.
- **Routing and redundancy** — connect networks and practice failover with HSRP.
- **Firewalls** — configure Cisco ASA and FortiGate policies, NAT, and traffic controls.
- **DMZ and servers** — separate internal systems from services that need outside access.
- **Branch connectivity** — connect a remote office using a site-to-site VPN.
- **VoIP** — use Cisco Call Manager Express (CME) with a Windows softphone.
- **Virtual machines** — connect a Windows 11 VM to the lab as an endpoint.

## Tools and environment

| Tool / platform | How it's used |
|---|---|
| GNS3 | Build and run the network topology |
| Cisco CML Personal | Run Cisco virtual network devices |
| VMware Workstation | Run the GNS3 environment and endpoint VMs |
| Cisco IOS IOU L2/L3 | Practice switching, VLANs, and routing |
| Cisco ASA | Perimeter firewall and DMZ |
| FortiGate | Internal network segmentation |
| Cisco 3745 | Planned CME/VoIP router |
| Windows 11 | Planned endpoint and softphone |
| Python | Planned troubleshooting automation |

## VoIP and Windows endpoint

The voice network is planned for **VLAN 30**.

| Item | Planned value |
|---|---|
| Voice subnet | `10.10.30.0/24` |
| Voice gateway | `10.10.30.1` |
| CME router | `10.10.30.10` |
| Windows VM | `VOIP-PHONE-01` |
| VMware LAN Segment | `VOIP-LAB` |

The Windows VM is intended to connect to the voice network through a VMware LAN Segment, the GNS3 VM, a GNS3 Cloud node, and the voice switch. A separate NAT adapter will provide normal internet access. These values are planned until configured and tested.

## Build plan

I'll work through the network in stages:

1. Confirm device connections and interface assignments.
2. Finalize VLANs and IP addressing.
3. Configure access ports and switch uplinks.
4. Configure core switching, routing, and HSRP.
5. Configure the ASA, FortiGate, and DMZ.
6. Bring up the branch VPN.
7. Configure CME and connect the softphone.
8. Test connectivity, firewall rules, redundancy, and VoIP.
9. Add repeatable troubleshooting exercises.

## Troubleshooting exercises

Once the main network is working, I plan to use Python or similar tools to introduce controlled faults in the lab. Examples include a wrong access VLAN, a missing trunk VLAN, a routing issue, an HSRP problem, or a firewall rule blocking traffic.

I'll investigate each issue, fix it, and verify the result. The exercises will use known, reversible changes and stay inside the isolated lab.

## Repository guide

The repository is organized by project stage:

- [Project overview](00-start-here/project-overview.md) — goals and current status.
- [Design](01-design/) — topology, addressing, port mapping, and device inventory.
- [Build instructions](02-build/BUILD-INSTRUCTIONS.md) — configuration steps and verification commands.
- [Lab guide](02-build/LAB-GUIDE.md) — how the lab is set up.
- [Implementation roadmap](02-build/implementation-roadmap.md) — planned build stages.
- [Configurations](03-configurations/) — saved device configurations.
- [VoIP](04-voip/README.md) — CME and softphone notes.
- [Testing](05-testing/test-plan.md) — test cases and results.
- [Troubleshooting](06-troubleshooting/network-chaos-lab/README.md) — controlled fault exercises.
- [Logs and evidence](07-logs-evidence/) — progress notes and screenshots.

For a quick overview of the folders, see the [repository guide](00-start-here/README.md).

## Project status

The network design is in place, and configuration is underway. Planned settings will be marked as such until they are verified. I'll keep adding configurations, screenshots, and test results as the lab develops.

## Other projects and feedback

You can find my other work on my [GitHub profile](https://github.com/MaloneNetworks) or connect with me on [LinkedIn](https://www.linkedin.com/in/darrellmalone9107/).

If you have feedback or suggestions, feel free to open an issue or start a discussion.

Thanks for checking out the project!

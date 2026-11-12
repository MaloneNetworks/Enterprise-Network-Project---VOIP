# Enterprise Network & VoIP Lab

I'm building an enterprise-style network in **GNS3** and **VMware Workstation**. The lab brings together routing, switching, firewalls, servers, branch connectivity, and VoIP.

This is a hands-on learning project. I'll document the design, configurations, problems, fixes, and test results as I build it.

## Current starting design

**Baseline: Enterprise Network v1.4**

This is the design I'm using to start the configuration work. It includes:

- Two ISP connections and an HQ edge router
- Cisco ASA perimeter firewall
- FortiGate internal firewall
- Redundant Layer 3 core switches
- Distribution and access switches
- Separate user, voice, server, and DMZ networks
- Branch office connected with GRE over IPsec
- Cisco CME for VoIP
- A connection between the GNS3 and Cisco CML labs

The diagrams show the planned design. Not every device or feature is configured and tested yet. I'll update the documentation as each part is built and verified.

### Enterprise topology

![Enterprise Network Baseline v1.4](01-design/topology/Enterprise_Network_BASELINE_v1.4.png)

### Network cut sheet

The cut sheet is the quick reference for VLANs, subnets, gateways, WAN links, firewall interfaces, servers, and device inventory.

![Enterprise Network Cut Sheet](01-design/topology/Enterprise%20Network%20Cut%20Sheet.png)

### Cisco CML and GNS3 integration

The following detail shows the CME-side connection from **R-CME-01** through **R1** toward the external Cisco CML network.

![CME-to-Cisco CML connection detail](01-design/topology/CME%20from%20CML.png)

This diagram shows the wider GNS3-to-Cisco CML connection, including the external connector, transit router, switch, and server connections.

![Cisco CML–GNS3 Integration Diagram](01-design/topology/Cisco-CML-GNS3-Integration.png)

The transit setup is documented in a separate repository: [Cisco CML–GNS3 Transit Network](https://github.com/MaloneNetworks/Cisco-CML_GNS3-Transit-Network). That project covers the VMware LAN Segment, Cisco CML bridge, GNS3 Cloud connection, and successful ping tests in both directions over `10.255.255.0/30`.

### Design files

- [Topology documentation](01-design/topology/README.md)
- [IP addressing and VLAN plan](01-design/ip-addressing.md)
- [Port mapping](01-design/port-mapping.md)
- [Device inventory](01-design/device-inventory.md)
- [Previous topology versions](01-design/topology/)

## What I'm building

The lab is designed to give me practice with:

- **Switching:** VLANs, access ports, trunks, and Layer 3 switching.
- **Routing:** Inter-VLAN routing, WAN links, and branch connectivity.
- **Redundancy:** HSRP and redundant core connections.
- **Firewalls:** Cisco ASA and FortiGate policies, NAT, and traffic control.
- **DMZ and servers:** Separating services from the internal user networks.
- **VoIP:** Cisco Call Manager Express (CME) and a Windows softphone.
- **Virtual machines:** Connecting a Windows 11 VM to the lab as an endpoint.

## Lab environment

| Tool or device | Purpose |
|---|---|
| GNS3 | Build and run the network |
| Cisco CML Personal | Run Cisco virtual network devices |
| VMware Workstation | Run the GNS3 environment and endpoint VMs |
| Cisco IOS IOU L2/L3 | Switching, VLANs, and routing practice |
| Cisco ASA | Perimeter firewall and DMZ |
| FortiGate | Internal network segmentation |
| Cisco 3745 | Planned CME/VoIP router |
| Windows 11 | Planned endpoint and softphone |
| Python | Planned network troubleshooting exercises |

## VoIP and Windows VM plan

The voice network is planned for **VLAN 30**:

| Item | Planned value |
|---|---|
| Voice subnet | `10.10.30.0/24` |
| Voice gateway | `10.10.30.1` |
| CME router | `10.10.30.10` |
| Windows VM | `VOIP-PHONE-01` |
| VMware LAN Segment | `VOIP-LAB` |

The Windows VM is intended to connect to the voice network through a VMware LAN Segment, the GNS3 VM, a GNS3 Cloud node, and the voice switch. Its separate NAT adapter will provide normal internet access.

These are planned settings. I'll mark them as complete only after they are configured and tested.

## Build order

I'll build and test the network in stages:

1. Confirm device connections and interface assignments.
2. Finalize VLANs and IP addressing.
3. Configure access ports and switch uplinks.
4. Configure core switching, routing, and HSRP.
5. Configure the ASA, FortiGate, and DMZ.
6. Set up the branch VPN.
7. Configure CME and connect the softphone.
8. Test connectivity, security rules, redundancy, and calls.
9. Add repeatable troubleshooting exercises.

## Troubleshooting practice

After the main network is working, I plan to create Python-based exercises that introduce one controlled fault at a time. Examples include a wrong access VLAN, a missing trunk VLAN, a routing issue, an HSRP problem, or a firewall rule blocking traffic.

I'll use the lab to find the issue, fix it, and verify the result. The exercises will stay inside the isolated lab and use known, reversible changes.

## Repository guide

The project files are grouped by purpose:

- [Project overview](00-start-here/project-overview.md) — goals and current status.
- [Design](01-design/) — topology, addressing, port mapping, and device inventory.
- [Build instructions](02-build/BUILD-INSTRUCTIONS.md) — configuration steps and verification commands.
- [Lab guide](02-build/LAB-GUIDE.md) — how the lab is organized.
- [Implementation roadmap](02-build/implementation-roadmap.md) — planned build stages.
- [Configurations](03-configurations/) — saved device configurations.
- [VoIP](04-voip/README.md) — CME and softphone notes.
- [Testing](05-testing/test-plan.md) — planned tests and results.
- [Troubleshooting](06-troubleshooting/network-chaos-lab/README.md) — controlled fault exercises.
- [Logs and evidence](07-logs-evidence/) — progress notes and screenshots.

For a quick guide to the folders, see the [repository guide](00-start-here/README.md).

## Project status

The current topology and cut sheet are the starting design. Configuration and testing are ongoing. I'll keep planned settings separate from completed work and update the project as the lab develops.

## Other projects and feedback

You can find my other work on my [GitHub profile](https://github.com/MaloneNetworks). You can also connect with me on [LinkedIn](https://www.linkedin.com/in/darrellmalone9107/).

If you have suggestions or spot something I can improve, feel free to open an issue or start a discussion.

Thanks for checking out the project!

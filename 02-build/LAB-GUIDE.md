# Enterprise Network & VoIP Lab — Lab Guide

## 1. Introduction

This is a hands-on enterprise networking lab built with GNS3 and VMware Workstation. The goal is to design, configure, secure, troubleshoot, and document a multi-site business network using virtual routers, switches, firewalls, servers, and endpoints.

The lab is being built in stages. Some devices and links are already present, but the full network is not yet configured or verified. This guide describes the intended design and learning goals; it does not claim that planned features are already operational.

## 2. Learning goals

By completing this lab, I aim to practice:

- Layer 2 switching, VLANs, access ports, and 802.1Q trunks.
- Layer 3 switching, SVIs, inter-VLAN routing, and routing tables.
- Redundancy using technologies such as EtherChannel/LACP, Spanning Tree, and HSRP where supported and appropriate.
- Firewall zones, access policies, NAT, and DMZ design.
- Branch connectivity and site-to-site VPN concepts.
- Network management and secure device access.
- Cisco Call Manager Express (CME), voice VLANs, DHCP/TFTP phone provisioning, and softphone testing.
- Network verification, troubleshooting, documentation, and controlled fault exercises.

## 3. Lab platform and tools

| Tool | Purpose |
|---|---|
| GNS3 | Build and run the virtual network topology |
| VMware Workstation | Host the GNS3 VM and Windows endpoint VM |
| Cisco IOU L2/L3 | Practice access, distribution, core switching, and Layer 3 functions |
| Cisco ASA | Practice firewall policies, NAT, and network segmentation |
| FortiGate | Practice Fortinet firewall administration and policy design |
| Cisco 3745 | Candidate router for the CME/VoIP portion |
| Windows 11 VM | Endpoint for network testing and planned softphone use |
| draw.io / diagrams.net | Create and maintain editable topology diagrams |
| Python (planned) | Create repeatable, controlled troubleshooting exercises |

## 4. Intended network layout

The design includes these functional areas:

1. **Internet/WAN edge:** ISP connections and the HQ edge router.
2. **Security perimeter:** Firewall layers controlling access between outside, internal, and DMZ networks.
3. **Core:** Two Layer 3 switches intended to provide resilient switching and routing.
4. **Distribution:** A Layer 2 distribution switch connecting the core to access switches.
5. **Access:** Separate access switches for administration, engineering, voice, and servers.
6. **DMZ:** A separated network for services that may need controlled outside access.
7. **Branch office:** A remote network connected to HQ over a routed WAN/VPN design.
8. **Voice network:** VLAN 30, a Cisco 3745 CME candidate, and a Windows softphone endpoint connected through a VMware LAN Segment.

Use the current topology image in `../diagrams/v2.0.png` as the design snapshot. The editable draw.io source should be stored in `../diagrams/source/` when added. The diagram, cut sheet, and live GNS3 project must be kept in sync.

## 5. VLAN plan

| VLAN | Name | Subnet | Intended use |
|---:|---|---|---|
| 10 | ADMIN | `10.10.10.0/24` | Administration endpoints |
| 20 | ENGINEERING | `10.10.20.0/24` | Engineering endpoints |
| 30 | VOICE | `10.10.30.0/24` | Voice endpoints and CME |
| 40 | SERVERS | `10.10.40.0/24` | Internal servers |
| 60 | MANAGEMENT | `10.10.60.0/24` | Management interfaces |
| 70 | BRANCH | `10.10.70.0/24` | Branch network |
| 100 | DMZ | `172.16.80.0/24` | DMZ servers |
| 999 | NATIVE-BLACKHOLE | No IP | Unused/native VLAN where appropriate |

These are proposed networks. Gateway ownership, DHCP, DNS, and firewall boundaries still need to be finalized before configuration.

## 6. Voice and CME design

The voice network is planned around VLAN 30 and the following items:

| Item | Current plan |
|---|---|
| Voice VLAN | VLAN 30 |
| Voice subnet | `10.10.30.0/24` |
| Proposed gateway | `10.10.30.1` |
| CME candidate | Cisco 3745, `R-CME-01` |
| CME interface address | `10.10.30.10` on Fa0/0 was previously configured |
| Windows endpoint | `VOIP-PHONE-01` |
| VMware LAN Segment | `VOIP-LAB` |
| GNS3 VM adapter | `eth1` intended for the lab-side connection |

The proposed Windows-to-CME path is:

```text
Windows 11 VM
  |
VMware LAN Segment: VOIP-LAB
  |
GNS3 VM network adapter (eth1)
  |
GNS3 Cloud node
  |
SW-Voice
  |
Voice VLAN 30
  |
R-CME-01 (Cisco 3745)
```

This path is planned and must be tested end to end. The Windows VM is intended to keep a separate NAT adapter for ordinary internet access.

Before configuring CME, validate the 3745 IOS feature support, available flash/storage, memory, CME version compatibility, phone firmware requirements, and softphone compatibility. The router booting and having an IP address do not prove that CME or phone provisioning will work.

## 7. How the documentation works

The documents have separate jobs:

- **Network cut sheet:** The source of truth for device names, ports, links, VLANs, and IP assignments.
- **Lab guide:** Explains the design, purpose, technologies, and learning goals.
- **Build instructions:** Gives the ordered configuration steps, commands, and verification checks.
- **Device inventory:** Tracks images, versions, and device capabilities.
- **Test plan:** Records expected results and actual test evidence.
- **draw.io topology:** Shows the network visually, including interface labels and logical groupings.

If the diagram, cut sheet, and GNS3 project disagree, stop and reconcile them before making configuration changes.

## 8. Safety and good lab practice

- Keep experiments inside the isolated GNS3 environment.
- Do not attach fault-injection scripts to physical network adapters, the home router, or external networks.
- Save a known-good copy before making major changes.
- Change one thing at a time and verify it.
- Use unique, documented device names and interface labels.
- Do not upload passwords, private keys, tokens, or sensitive configuration data to GitHub.
- Clearly label planned, configured, tested, and verified features.

## 9. Completion standard

A feature is complete only when:

1. The configuration has been applied and saved.
2. The relevant verification commands show the expected state.
3. Connectivity or behavior has been tested.
4. Results and any limitations have been documented.
5. The cut sheet and topology diagram match the actual lab.

## 10. Project status

This is an independent learning project and an evolving lab. The repository will be updated as the topology is built, configurations are validated, and test evidence is collected. Planned features will remain labeled as planned until they are working.

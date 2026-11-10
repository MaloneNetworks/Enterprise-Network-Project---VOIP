# Enterprise Network & VoIP Lab

Hey, thanks for stopping by!

I'm building this project to get hands-on experience designing, setting up, and troubleshooting an enterprise-style network. I'm using **GNS3** and **VMware Workstation** to create a virtual environment where I can practice the same kinds of networking and security tasks you'd find in a real business.

This is a work in progress, and I'm documenting the process as I go — including the design decisions, configurations, things that break, and how I fix them.

## New to GNS3 or virtualization?

No worries — here's the quick version.

**GNS3** is a program that lets you build a computer network on your PC without needing a room full of physical routers, switches, and firewalls. You add virtual versions of network devices to a workspace, connect them with virtual cables, and then configure them much like you would real equipment. You can practice things like VLANs, routing, firewalls, and troubleshooting in that virtual environment.

**Virtualization** is the technology that lets one physical computer run multiple separate computers, called *virtual machines (VMs)*. Each VM behaves like its own computer, with its own operating system and virtual network connections.

For this project, I'm using:

- **GNS3** to create the network topology and connect the virtual network devices.
- **VMware Workstation** to run virtual machines, including the GNS3 virtual machine and a Windows 11 endpoint.
- **Virtual network adapters and links** to connect the VMs to the lab, so they can communicate with the routers, switches, and firewalls.

Think of it like building a small IT environment inside one physical PC. The routers, switches, firewalls, servers, and computers are virtual, but the configuration and troubleshooting skills are very similar to working with physical equipment.

You don't need to know GNS3 or virtualization to follow along. I'll document the setup, explain the purpose of each part, and include diagrams, configurations, screenshots, and test results as the project develops.

## What I'm building

The goal is to create a network that brings several technologies together:

- **Switching and VLANs** — separate departments and devices into their own networks.
- **Routing and redundancy** — connect the networks and practice keeping things online when a link or device fails.
- **Firewalls and network security** — work with Cisco ASA and FortiGate, build security rules, and control traffic between network zones.
- **DMZ and servers** — create a separate network for services that need to be reachable from outside.
- **Branch connectivity** — connect a remote office to the main site and practice VPN technologies.
- **VoIP** — build a voice network using Cisco Call Manager Express (CME) and a Windows softphone.

I also want to add a troubleshooting mode that intentionally introduces network problems. The idea is to randomly break one part of the lab, then work through the symptoms and figure out what went wrong.

## Tools and environment

| Tool / platform | How I'm using it |
|---|---|
| GNS3 | Build and run the network topology |
| VMware Workstation | Run the GNS3 environment and Windows endpoint VM |
| Cisco IOS IOU L2/L3 | Practice switching, VLANs, routing, and redundancy |
| Cisco ASA | Practice firewall rules, NAT, and DMZ security |
| FortiGate | Get hands-on experience with Fortinet firewall administration |
| Cisco 3745 | Evaluate as the router for the CME/VoIP portion |
| Windows 11 | Host the planned softphone endpoint |

Some devices are already placed and connected in GNS3. The network has not been configured yet, so the addressing and feature details below are still a working design.

## Current design

The voice portion is planned around:

| Item | Current plan |
|---|---|
| Voice VLAN | VLAN 30 |
| Voice subnet | `10.10.30.0/24` |
| Proposed voice gateway | `10.10.30.1` |
| Proposed CME address | `10.10.30.10` |
| Windows VM | `VOIP-PHONE-01` |
| VMware network segment | `VOIP-LAB` |

These values are not configured or verified yet. I'll update the documentation as the design is tested and finalized.

## How I'm approaching the project

I'm building this in stages so I can test each part before moving on:

1. Document the devices, interfaces, and existing connections.
2. Finalize the IP addressing and VLAN plan.
3. Configure the core, distribution, and access switching.
4. Set up routing and gateway redundancy.
5. Configure the ASA, FortiGate, and DMZ.
6. Bring up the branch connection.
7. Validate the CME router and connect the Windows softphone.
8. Test connectivity, security policies, failover, and VoIP calls.
9. Add repeatable troubleshooting exercises and document the results.

## The troubleshooting challenge

One feature I'm planning is a small **Network Chaos Lab**. It will randomly introduce one controlled issue — for example, a VLAN mistake, a broken trunk, a routing problem, an HSRP issue, or a firewall rule blocking traffic.

The challenge will be to identify the cause, repair it, and verify that the network is working again. This part is still in the design stage; it will be developed after the main network is working and backed up.

## Follow along

I'm keeping the project organized so the build can be followed and repeated. The repository includes:

- [Implementation roadmap](documentation/implementation-roadmap.md)
- [Lab build instructions](documentation/lab-instructions.md)
- [Device inventory](documentation/device-inventory.md)
- [IP addressing plan](documentation/ip-addressing.md)
- [Port mapping](documentation/port-mapping.md)
- [CME configuration plan](voip/cme-configuration.md)
- [Windows softphone setup](voip/softphone-setup.md)
- [Network Chaos Lab](network-chaos-lab/README.md)
- [Test plan](testing/test-plan.md)

As I complete each stage, I'll add diagrams, sanitized configurations, screenshots, test results, and notes about what I learned.

## A note on project status

This is an independent learning project. The topology is being prepared, and the configuration and testing work is still ahead. I'll distinguish planned features from features that are actually implemented and verified.


## Check out my other labs & share feedback

This is one of my hands-on projects, and I'll be adding more labs and experiments as I continue learning. Feel free to check out my other repositories and projects on my [GitHub profile](https://github.com/MaloneNetworks).

If you spot something I could improve, have a different way of approaching a configuration, or just have feedback, I'd love to hear it. Open an issue or start a discussion in the repository. I'm always looking to learn, improve the lab, and hear how other people would tackle the same challenges.

Thanks for checking out my work!

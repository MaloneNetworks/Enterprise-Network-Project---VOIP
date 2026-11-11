# Network Diagrams

This folder holds the network design snapshots and their editable source files. Keep diagrams aligned with the GNS3 project and the port/cable register.

## Current working baseline

**Enterprise Network Baseline v1.2** is the current working design baseline as of November 10, 2026.

- [Enterprise Network Baseline v1.2](Enterprise_Network_BASELINE_v1.2.png) — current working design.
- [Enterprise Network Baseline v1.1](Enterprise_Network_BASELINE_v1.1.png) — previous revision.

The latest baseline image was supplied in the project conversation. It should be committed here as:

`enterprise-network-baseline-v1.1.png`

The v1.2 baseline includes:

- Dual ISP connections into the HQ edge router
- GRE over IPsec site-to-site tunnel to the branch
- Cisco ASA perimeter firewall protecting the DMZ and HQ network from the WAN
- FortiGate internal segmentation firewall
- Redundant Layer 3 core switches using HSRP and an LACP core interconnect
- Distribution and access switching for Admin, Engineering, Voice, and Servers
- Dedicated voice VLAN and Cisco CME router
- DMZ web, mail, and DNS servers
- Branch office router, switch, endpoint, and VLAN 70

**Status:** The design and interface mapping have been reviewed against the GNS3 topology. The diagram represents intended architecture and addressing; it does not prove that every IP address, route, firewall policy, or service has been configured and tested.

## Diagram conventions

- Mark links as planned until they exist in GNS3 and are checked.
- Distinguish configured from tested and verified connections.
- Keep endpoint interface labels on both ends of each link.
- Keep the editable draw.io source alongside exported images whenever available.
- Record changes as a new version rather than silently replacing the baseline.

## Existing design snapshot

- [Topology v2.0](v2.0.png) — earlier design snapshot.

## Planned supporting diagrams

- Full GNS3 layout with exact interface labels
- VLAN and IP addressing map
- Firewall zone and traffic-flow diagram
- VoIP network and softphone integration

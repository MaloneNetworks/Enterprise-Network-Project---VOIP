# Enterprise IP Addressing Plan

> **Status: Draft / proposed design.** The network is not configured yet. These addresses are a working plan for the lab, not verified live settings. Confirm device interfaces, firewall transit networks, existing labels in the GNS3 topology, and gateway ownership before applying configurations.

## VLAN and subnet plan

| VLAN | Name | Subnet | Proposed default gateway | Intended use |
|---:|---|---|---|---|
| 10 | ADMIN | 10.10.10.0/24 | 10.10.10.1 | Administration endpoints |
| 20 | ENGINEERING | 10.10.20.0/24 | 10.10.20.1 | Engineering endpoints |
| 30 | VOICE | 10.10.30.0/24 | 10.10.30.1 | VoIP endpoints and CME reachability |
| 40 | SERVERS | 10.10.40.0/24 | 10.10.40.1 | Internal servers |
| 60 | MANAGEMENT | 10.10.60.0/24 | 10.10.60.1 | Network-device management |
| 70 | BRANCH | 10.10.70.0/24 | 10.10.70.1 | Branch user/data network |
| 100 | DMZ | 172.16.80.0/24 | TBD | Public-facing DMZ services |
| 999 | NATIVE-BLACKHOLE | No IP subnet | None | Unused native VLAN on trunks, subject to image support |

The VLAN IDs and broad purposes follow the current topology design. The /24 networks and gateway addresses are proposed conventions and must be checked against any IP labels already present in the GNS3 project.

## Proposed infrastructure reservations

| Network | Device / purpose | Proposed address | Notes |
|---|---|---|---|
| VLAN 10 | HSRP virtual gateway | 10.10.10.1 | Only if HSRP is selected |
| VLAN 20 | HSRP virtual gateway | 10.10.20.1 | Only if HSRP is selected |
| VLAN 30 | HSRP virtual gateway | 10.10.30.1 | Only if HSRP is selected |
| VLAN 40 | HSRP virtual gateway | 10.10.40.1 | Only if HSRP is selected |
| VLAN 60 | HSRP virtual gateway | 10.10.60.1 | Only if HSRP is selected |
| VLAN 70 | HSRP virtual gateway | 10.10.70.1 | Only if branch routing design uses this gateway |
| VLAN 30 | R-CME-01 | 10.10.30.10 | Candidate CME address; verify interface and CME support |
| VLAN 30 | Softphone VM | DHCP reservation or 10.10.30.100 | Do not assign until L2 bridge and DHCP path are validated |
| VLAN 40 | Internal services | 10.10.40.0/24 | Reserve low addresses for servers; assign after inventory |
| VLAN 60 | Switch management | 10.10.60.0/24 | Reserve static addresses after switch inventory |

## DHCP planning

| VLAN | DHCP scope proposal | Exclusions / reservations |
|---:|---|---|
| 10 | 10.10.10.100–10.10.10.199 | .1 gateway; reserve infrastructure |
| 20 | 10.10.20.100–10.10.20.199 | .1 gateway; reserve infrastructure |
| 30 | 10.10.30.100–10.10.30.199 | .1 gateway; .10 CME candidate; Option 150 only after TFTP/CME validation |
| 40 | Static assignments preferred | Servers and infrastructure |
| 60 | Static assignments preferred | Network management |
| 70 | 10.10.70.100–10.10.70.199 | .1 gateway; branch services excluded |
| 100 | Static assignments preferred | DMZ servers |

DHCP server location, relay/helper configuration, and actual pools are undecided. Do not configure multiple DHCP servers for the same scope. If CME supplies DHCP, define the scope there only after routing and voice VLAN behavior are validated.

## WAN, transit, and tunnel networks

These links require dedicated point-to-point addressing and must not be guessed from the LAN VLAN plan. Assign them only after inventorying the exact router/firewall interfaces and the IP labels in the topology:
- ISP1 to HQ-EDGE
- ISP2 to HQ-EDGE
- HQ-EDGE to ASA-HQ-01
- ASA-HQ-01 to FortiGate
- FortiGate to CORE-01 and CORE-02
- Branch WAN underlay and GRE/IPsec tunnel
- Any DMZ transit segments

A /30 or /31 may be appropriate for point-to-point routed links depending on platform support. Record both endpoint addresses and masks in the port map.

## Address allocation rules
1. Reserve .1 for the virtual gateway only where HSRP is actually deployed.
2. Reserve low addresses for infrastructure and statically addressed services.
3. Exclude static addresses from DHCP scopes.
4. Record DHCP source, relay/helper, DNS, and TFTP details for every scope.
5. Do not assume the core switches own every VLAN gateway; confirm the firewall/router boundary first.
6. Avoid duplicate default gateways, overlapping subnets, and multiple DHCP authorities.
7. Reconcile this draft with the GNS3 diagram before configuration.

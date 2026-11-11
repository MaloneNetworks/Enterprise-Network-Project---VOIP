# Enterprise Network & VoIP Lab — Network Cut Sheet

> **Document status:** Working draft  
> **Purpose:** This is the source of truth for device names, interfaces, VLANs, IP addressing, and physical/logical connections in the GNS3 lab.  
> **Important:** A planned value is not a verified configuration. Only mark a row **Verified** after checking the GNS3 cable and the device configuration.

## 1. Lab overview

| Item | Current design |
|---|---|
| Platform | GNS3 running with VMware Workstation |
| Main site | HQ enterprise network |
| Remote site | Branch office |
| Security | Cisco ASA and FortiGate |
| Switching | Cisco IOU L2 and L3 |
| Voice | Cisco 3745 CME candidate and Windows 11 softphone VM |
| Voice VMware segment | `VOIP-LAB` |
| Topology diagram | [Enterprise Network Baseline v1.2](topology/Enterprise_Network_BASELINE_v1.2.png) |
| Editable diagrams | `diagrams/source/` (add the matching `.drawio` source file when available) |

## 2. VLAN and IP address plan

These are the current proposed networks. Confirm gateway ownership, DHCP source, and firewall boundaries before configuring them.

| VLAN | Name | Network | Proposed gateway | Purpose | Status |
|---:|---|---|---|---|---|
| 10 | ADMIN | `10.10.10.0/24` | `10.10.10.1` | Admin endpoints | Draft |
| 20 | ENGINEERING | `10.10.20.0/24` | `10.10.20.1` | Engineering endpoints | Draft |
| 30 | VOICE | `10.10.30.0/24` | `10.10.30.1` | Voice devices and CME | Draft; switch path partly configured |
| 40 | SERVERS | `10.10.40.0/24` | `10.10.40.1` | Internal servers | Draft |
| 60 | MANAGEMENT | `10.10.60.0/24` | `10.10.60.1` | Network management | Draft |
| 70 | BRANCH | `10.10.70.0/24` | `10.10.70.1` | Branch network | Draft |
| 100 | DMZ | `172.16.80.0/24` | To be decided | Public-facing services | Draft |
| 999 | NATIVE-BLACKHOLE | No IP address | None | Unused/native VLAN where appropriate | Draft |

**Gateway note:** The `.1` addresses are proposed only. If HSRP is used, these may become virtual gateway addresses. Do not configure them until we decide which devices provide Layer 3 routing.

## 3. ASA-to-FortiGate transit

| Link | Network | Device A / interface / IP | Device B / interface / IP | Status |
|---|---|---|---|---|
| ASA-FGT-TRANSIT-01 | `10.255.0.8/30` | ASA-HQ-01 E1 — `10.255.0.9/30` | FortiGate E0 — `10.255.0.10/30` | Addressing agreed; configuration and testing pending |

Network `10.255.0.8/30` has usable addresses `10.255.0.9` and `10.255.0.10`, with broadcast address `10.255.0.11`.

## 4. Device inventory summary

| Device name | Role | Platform / image known so far | Interfaces / notes | Status |
|---|---|---|---|---|
| CORE-01 | Primary core switch | Cisco IOU L3 | Four ports available; exact interface names and cable assignments must be checked | Added; initial configuration pending |
| CORE-02 | Secondary core switch | Cisco IOU L3 | Four ports available; exact interface names and cable assignments must be checked | Added; initial configuration pending |
| SW-DIST-01 | Distribution switch | Cisco IOU L2 | Exact port map to be confirmed | Added; configuration in progress |
| SW-Admin | Admin access switch | Cisco IOU L2 | Exact port map to be confirmed | Added; pending |
| SW-ENG | Engineering access switch | Cisco IOU L2 | Exact port map to be confirmed | Added; pending |
| SW-Voice | Voice access switch | Cisco IOU L2 | E0/0 uplink; E0/1 to CME router, as previously recorded | VLAN 30/trunk work reported as configured |
| SW-SRV | Server access switch | Cisco IOU L2 | Exact port map to be confirmed | Added; pending |
| R-CME-01 | CME/voice router candidate | Cisco 3745; IOS 12.4(25d), Advanced Enterprise image reported | Fa0/0 has `10.10.30.10` configured | CME support and storage require validation |
| HQ-EDGE | HQ WAN/edge router | Exact image/model to confirm | Record all WAN and firewall-facing ports | Pending |
| R-Branch | Branch router | Exact image/model to confirm | Record WAN and LAN ports | Pending |
| ASA-HQ-01 | HQ firewall | Exact ASA image/version to confirm | Record outside, inside, and DMZ-facing ports | Pending |
| FortiGate | Additional firewall | Exact image/version to confirm | Record all connected ports | Pending |
| VOIP-PHONE-01 | Windows softphone endpoint | Windows 11 VM | VMware NAT adapter plus `VOIP-LAB` LAN Segment adapter planned | VM exists; lab-side path not yet verified |
| GNS3 VM | Runs GNS3 nodes | VMware VM | `eth0` reported as `192.168.4.79/22`; `eth1` intended for lab bridge | `eth1` path not yet verified |

## 5. Known cable and interface assignments

Do not move existing cables to match this table. Check the actual GNS3 link endpoints before entering interface configuration.

| Link ID | Device A | Interface A | Device B | Interface B | Purpose | Status |
|---|---|---|---|---|---|---|
| ASA-FGT-TRANSIT-01 | ASA-HQ-01 | `Ethernet1` (E1) | FortiGate | `Ethernet0` (E0) | Routed firewall transit; `10.255.0.8/30` | Interface mapping checked; addressing agreed |
| VOICE-UPLINK-01 | SW-DIST-01 | `Ethernet1/0` | SW-Voice | `Ethernet0/0` | Distribution-to-voice-switch uplink | Previously recorded; verify in GNS3 |
| CME-LINK-01 | SW-Voice | `Ethernet0/1` | R-CME-01 | `FastEthernet0/0` | CME router connection to voice VLAN | Previously recorded; verify in GNS3 |
| CORE-PEER-01 | CORE-01 | To verify | CORE-02 | To verify | First planned core peer link | Cable/ports need confirmation |
| CORE-PEER-02 | CORE-01 | To verify | CORE-02 | To verify | Second planned core peer link; potential LACP member | Cable/ports need confirmation |
| CORE-DIST-01 | CORE-01 | To verify | SW-DIST-01 | To verify | Core-to-distribution path | Cable/ports need confirmation |
| CORE-DIST-02 | CORE-02 | To verify | SW-DIST-01 | To verify | Redundant core-to-distribution path | Cable/ports need confirmation |
| VM-VOICE-01 | Windows 11 VM | VMware adapter on `VOIP-LAB` | GNS3 Cloud1 | Cloud interface to verify | Windows softphone path into GNS3 | Planned; not tested |

Add every remaining cable from the GNS3 workspace before calling the cut sheet complete. This includes ISP links, HQ edge/firewall links, DMZ links, branch links, server links, and endpoint connections.

## 6. Reserved and planned endpoint addresses

| Device / service | VLAN | Planned address | Status / notes |
|---|---:|---|---|
| R-CME-01 Fa0/0 | 30 | `10.10.30.10` | Address reported configured; reachability still needs testing |
| Voice gateway | 30 | `10.10.30.1` | Proposed; gateway device not selected |
| Windows softphone | 30 | DHCP or `10.10.30.100` | Do not assign until VM bridge and DHCP design are verified |
| Internal servers | 40 | To assign | Use static/reserved addresses |
| Switch management | 60 | To assign | Assign after management VLAN design is approved |
| DMZ servers | 100 | To assign | Assign after firewall and DMZ design is approved |

## 7. Interface verification checklist

For each cable, record both ends exactly as shown in GNS3 and verify the interface on the device.

- [ ] Confirm CORE-01 interface names and cable endpoints.
- [ ] Confirm CORE-02 interface names and cable endpoints.
- [ ] Confirm the two core peer links, if both are present.
- [ ] Confirm each core-to-distribution connection.
- [ ] Confirm all distribution-to-access connections.
- [ ] Confirm the voice-switch uplink and CME connection.
- [ ] Confirm firewall, ISP, DMZ, and branch connections.
- [ ] Confirm the Windows `VOIP-LAB` path into GNS3 Cloud1.

Useful Cisco checks (not every command is supported by every image):

```text
show ip interface brief
show interfaces status
show cdp neighbors detail
show lldp neighbors detail
show vlan brief
show interfaces trunk
show etherchannel summary
```

## 8. Change control

When a port, VLAN, address, or cable changes:

1. Update this cut sheet.
2. Update the draw.io source diagram and exported image.
3. Update the relevant configuration instructions.
4. Apply the change in GNS3.
5. Verify the result and record the test evidence.
6. Update the status from **Draft** or **Pending** to **Verified** only when the evidence supports it.

Never publish passwords, private keys, public IPs that should remain private, or other sensitive configuration details.

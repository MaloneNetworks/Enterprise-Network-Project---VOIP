# Project Overview

## Purpose
A practical enterprise networking and VoIP implementation lab demonstrating planning, configuration, validation, troubleshooting, and documentation in a repeatable virtual environment.

## Scope
- Enterprise topology and device inventory
- VLANs, trunks, access ports, and Layer 2 controls
- Layer 3 switching, inter-VLAN routing, and gateway redundancy
- WAN and branch connectivity
- Firewall segmentation, NAT, ACLs, and DMZ policy
- Voice VLAN, DHCP/TFTP, call control, and softphone endpoints
- Verification, failure testing, and technical documentation

## Working principles
1. Preserve the existing GNS3 project while inventorying it.
2. Confirm appliance capabilities before choosing commands.
3. Maintain one authoritative IP and port assignment table.
4. Apply changes in small, testable increments.
5. Capture evidence for every completed milestone.
6. Sanitize configurations before committing them.

## Current known environment
- GNS3 VM running in VMware Workstation.
- Windows 11 endpoint VM named `VOIP-PHONE-01`.
- Windows VM has a NAT adapter and a second adapter on VMware LAN Segment `VOIP-LAB`.
- GNS3 VM second interface `eth1` is intended for `VOIP-LAB`.
- Cisco 3745 candidate reports IOS 12.4(25d), image `C3745-ADVENTERPRISEK9-M`; flash availability needs investigation.

## Open decisions
- Confirm appliance types, software versions, and interfaces.
- Confirm final VLAN and subnet allocations.
- Confirm gateway and DHCP ownership.
- Confirm CME release and endpoint protocol compatibility.
- Confirm the Cloud1 `eth1` bridge path.

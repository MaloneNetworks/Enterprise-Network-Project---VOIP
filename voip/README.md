# VoIP Implementation

## Goal
Integrate virtual softphone endpoints with call control. Intended voice network: VLAN 30, `10.10.30.0/24`, subject to final validation.

## Current state
- Windows 11 VM `VOIP-PHONE-01` installed.
- Adapter 1 uses VMware NAT for internet access.
- Adapter 2 is assigned to VMware LAN Segment `VOIP-LAB`.
- GNS3 VM `eth1` is intended to connect to the same LAN segment.
- Cloud1 is configured to expose GNS3 VM `eth1`.
- Cisco 3745 is the CME candidate; IOS/CME/firmware compatibility and flash storage require verification.

## Important technical distinction
A Cisco 7960/7940 firmware image is not a standalone GNS3 phone appliance; it requires compatible phone hardware. For a hardware-free lab, use a compatible softphone. Cisco IP Communicator is a Cisco-style softphone, but installer availability, licensing, supported OS, and CME interoperability must be verified. A SIP softphone may require a different call-control platform or protocol configuration; SIP and SCCP are not interchangeable.

## Proposed endpoint plan
| Endpoint | Extension | Addressing | Status |
|---|---:|---|---|
| VOIP-PHONE-01 | 1001 | DHCP in voice subnet, planned | Windows installed; softphone pending |
| VOIP-PHONE-02 | 1002 | DHCP in voice subnet, planned | Not created |
| VOIP-PHONE-03 | 1003 | DHCP in voice subnet, planned | Not created |

## Checklist
- [ ] Verify VLAN 30 end-to-end.
- [ ] Verify Cloud1 bridge path.
- [ ] Verify gateway and DHCP design.
- [ ] Verify CME software and flash requirements.
- [ ] Verify endpoint protocol compatibility.
- [ ] Configure DHCP/TFTP as appropriate.
- [ ] Configure extensions.
- [ ] Test registration and two-way audio.
- [ ] Capture sanitized evidence.

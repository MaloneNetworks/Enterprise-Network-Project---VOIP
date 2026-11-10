# Windows Softphone Endpoint Setup

> Status: planned. The Windows 11 VM has a NAT adapter and a second adapter on VMware LAN Segment VOIP-LAB. The GNS3 bridge path is not yet validated.

## Intended path
Windows VM VOIP-LAB adapter -> VMware LAN Segment -> GNS3 VM eth1 -> GNS3 Cloud1 -> SW-Voice -> VLAN 30 -> CME/router path.

This is an intended path, not a verified connection.

## Validation sequence
1. Identify the MAC address of the VM's VOIP-LAB adapter.
2. Confirm GNS3 VM eth1 is attached to the same VMware LAN Segment and is up.
3. Confirm Cloud1 is bound to the intended GNS3 VM interface.
4. Confirm the Cloud1-to-SW-Voice link and switch port.
5. Configure VLAN 30 only after verifying switchport mode and upstream trunk.
6. Confirm the VM receives the intended voice subnet address.
7. Test gateway and CME reachability.
8. Install a softphone compatible with the available CME protocol/version.
9. Register and place test calls.

Do not bridge the NAT adapter into the voice VLAN. VMware LAN Segment connectivity is not automatically connected to GNS3; the Cloud bridge must be validated. Cisco IP Communicator availability, licensing, OS compatibility, and CME compatibility must be checked. A SIP client cannot register to an SCCP-only setup unless compatible SIP support is configured.

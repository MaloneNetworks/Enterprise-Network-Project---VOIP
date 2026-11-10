# Connect the Windows Softphone VM

> **Status: Planned.** The Windows 11 VM has a VMware NAT adapter and a second adapter on the VMware LAN Segment named `VOIP-LAB`. The connection from that segment into GNS3 has not been tested yet.

## Planned connection path

Windows VM's VOIP-LAB adapter -> VMware LAN Segment -> GNS3 VM `eth1` -> GNS3 Cloud1 -> SW-Voice -> VLAN 30 -> CME router.

This is the connection we want. It is not confirmed working yet.

## Check it in this order

1. Find the MAC address of the Windows VM's VOIP-LAB adapter.
2. Make sure GNS3 VM `eth1` is connected to the same VMware LAN Segment and is turned on.
3. Make sure GNS3 Cloud1 uses the correct GNS3 VM interface.
4. Check the cable from Cloud1 to SW-Voice and confirm the switch port.
5. Set up VLAN 30 only after checking the switch port and the link back to the other switches.
6. Check whether Windows receives an address from the voice network.
7. Test whether Windows can reach the voice gateway and CME router.
8. Install a softphone that works with the CME version and phone protocol.
9. Register the phone and place test calls.

Do not connect the Windows NAT adapter to the voice VLAN. The NAT adapter is for internet access. The VMware LAN Segment does not connect to GNS3 by itself; the Cloud connection must be checked.

Cisco IP Communicator still needs checks for availability, license, Windows support, and CME support. SIP and SCCP are different phone protocols, so the softphone and CME settings must match.

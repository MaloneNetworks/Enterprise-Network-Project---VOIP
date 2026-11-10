# Cable and Port List

This page records which device ports are connected to each other. The GNS3 diagram is already cabled, and we want to keep those connections. Some labels still need to be checked in GNS3 before we treat them as confirmed.

## Core and distribution switches

| Link | First device | Port | Second device | Port | Why they are connected | Status |
|---|---|---|---|---|---|---|
| CORE-LINK-01 | CORE-01 | Check in GNS3 | CORE-02 | Check in GNS3 | First link in the planned LACP bundle | Cable drawn; ports to check |
| CORE-LINK-02 | CORE-01 | Check in GNS3 | CORE-02 | Check in GNS3 | Second link in the planned LACP bundle | Cable drawn; ports to check |
| CORE-DIST-01 | CORE-01 | Check in GNS3 | SW-DIST-01 | Check in GNS3 | Main link to the distribution switch | Cable drawn; ports to check |
| CORE-DIST-02 | CORE-02 | Check in GNS3 | SW-DIST-01 | Check in GNS3 | Backup link to the distribution switch | Cable drawn; ports to check |

Each core switch has four ports, as confirmed by the user. Keep the current cables in place. Check the actual port labels before setting up the two-link LACP bundle or the distribution links.

## Links to the access switches

| Link | First device | Port | Second device | Port | Why they are connected | Status |
|---|---|---|---|---|---|---|
| ACCESS-ADMIN | SW-DIST-01 | Check in GNS3 | SW-Admin | Check in GNS3 | Admin network connection | Cable drawn; ports to check |
| ACCESS-ENG | SW-DIST-01 | Check in GNS3 | SW-ENG | Check in GNS3 | Engineering network connection | Cable drawn; ports to check |
| ACCESS-VOICE | SW-DIST-01 | Ethernet1/1 shown in diagram; check in GNS3 | SW-Voice | Ethernet0/0 | Carries the voice network (VLAN 30) | Cable drawn; switch setup in progress |
| ACCESS-SRV | SW-DIST-01 | Check in GNS3 | SW-SRV | Check in GNS3 | Server network connection | Cable drawn; ports to check |

## Phone network connections

| Link | First device | Port | Second device | Port | Why they are connected | Status |
|---|---|---|---|---|---|---|
| CME-VOICE | R-CME-01 | FastEthernet0/0 | SW-Voice | Ethernet0/1 | Connects the CME router to the voice network | Cable shown in v2.0; router address is 10.10.30.10; switch setup in progress |
| VM-BRIDGE | GNS3 Cloud1 | eth1 planned | VMware VOIP-LAB adapter | LAN Segment adapter | Connects the Windows softphone VM to GNS3 | Planned; not tested |

## Other cables to record

Add the ports for ISP1, ISP2, the internet cloud, HQ-EDGE, ASA-HQ-01, FortiGate, the DMZ switch and servers, R-Branch, branch switch, and all PCs.

## Rules for this page

- Do not move or change existing cables unless we find a real problem and agree to change them.
- Write down the port at both ends of every cable.
- Use the exact port names shown by GNS3.
- Check the switch settings after configuring a port.
- Mark a link as confirmed only after checking it in GNS3 and on the devices.

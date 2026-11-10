# Port Mapping

Authoritative record of GNS3 links and interface assignments. The GNS3 workspace is cabled but has not yet been started/configured. The port names below are a transcription of the current diagram where legible; verify both endpoints against GNS3 link labels before configuration.

## Core and distribution links

| Link | Device A | Interface A | Device B | Interface B | Purpose | State |
|---|---|---|---|---|---|---|
| CORE-LINK-01 | CORE-01 | Diagram label to verify | CORE-02 | Diagram label to verify | First member of planned LACP EtherChannel | Drawn; verify |
| CORE-LINK-02 | CORE-01 | Diagram label to verify | CORE-02 | Diagram label to verify | Second member of planned LACP EtherChannel | Drawn; verify |
| CORE-DIST-01 | CORE-01 | Diagram label to verify | SW-DIST-01 | Diagram label to verify | Distribution uplink | Drawn; verify |
| CORE-DIST-02 | CORE-02 | Diagram label to verify | SW-DIST-01 | Diagram label to verify | Redundant distribution uplink | Drawn; verify |

Each IOU L3 core switch has four ports according to the user. Preserve the current cabling. Do not add ports or change links based on an assumed interface map. Verify that the existing two-link inter-core bundle and other links match the actual four-port inventory.

## Access-layer uplinks

| Link | Device A | Interface A | Device B | Interface B | Purpose | State |
|---|---|---|---|---|---|---|
| ACCESS-ADMIN | SW-DIST-01 | Diagram label to verify | SW-Admin | Diagram label to verify | Admin access uplink | Drawn; verify |
| ACCESS-ENG | SW-DIST-01 | Diagram label to verify | SW-ENG | Diagram label to verify | Engineering access uplink | Drawn; verify |
| ACCESS-VOICE | SW-DIST-01 | Ethernet1/1 (diagram label; verify in GNS3) | SW-Voice | Ethernet0/0 | Voice access uplink / VLAN 30 trunk | Cable shown in v2.0 diagram; switch config in progress |
| ACCESS-SRV | SW-DIST-01 | Diagram label to verify | SW-SRV | Diagram label to verify | Server access uplink | Drawn; verify |

## VoIP links

| Link | Device A | Interface A | Device B | Interface B | Purpose | State |
|---|---|---|---|---|---|---|
| CME-VOICE | R-CME-01 | FastEthernet0/0 | SW-Voice | Ethernet0/1 | CME reachability / voice access (VLAN 30) | Cable shown in v2.0 diagram; router Fa0/0 configured as 10.10.30.10; switch config in progress |
| VM-BRIDGE | GNS3 Cloud1 | eth1 candidate | VMware VOIP-LAB adapter | LAN Segment adapter | Windows VM to GNS3 | Intended; not validated |

## Other topology links

Inventory and document ISP1, ISP2, Internet cloud, HQ-EDGE, ASA-HQ-01, FortiGate, DMZ switch and servers, R-Branch, branch switch, and all endpoint links. Add one row per physical GNS3 link.

## Rules
- Preserve the current GNS3 cabling unless a specific issue is identified and agreed.
- Replace "Diagram label to verify" with actual interface names from GNS3.
- Record both ends of every link.
- Verify switch access/trunk mode and VLAN allowance with device commands after configuration.
- Mark a link verified only after comparing the GNS3 link endpoints and live interface state.

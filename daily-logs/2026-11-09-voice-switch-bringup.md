# Lab Notes — November 9, 2026

## What I worked on
Started bringing up the voice network and its switch connections.

## CME router check: R-CME-01
- Device: Cisco 3745.
- IOS: 12.4(25d), Advanced Enterprise image.
- Memory: about 256 MB.
- FastEthernet0/0 address: `10.10.30.10`; it showed up/up.
- The router reports that flash storage is missing or unavailable.
- CME support, required phone files, and a usable storage location still need to be checked.

## Voice network plan
- Voice VLAN: VLAN 30 (`VOIP`).
- Voice subnet: `10.10.30.0/24`.
- CME router address: `10.10.30.10`.
- The voice gateway and DHCP service have not been decided or tested yet.

## Switch connections and progress

| Device | Port | Connected device | Connected port | Purpose | Progress |
|---|---|---|---|---|---|
| SW-Voice | Ethernet0/0 | SW-DIST-01 | Ethernet1/0 | Trunk carrying VLAN 30 | User reports configured and good |
| SW-Voice | Ethernet0/1 | R-CME-01 | FastEthernet0/0 | Router connection in VLAN 30 | User reports configured and good |
| SW-DIST-01 | Ethernet1/0 | SW-Voice | Ethernet0/0 | Trunk carrying VLAN 30 | User reports configured and good |

Both switches use the Cisco IOU L2 image. VLAN 30 and the trunk connection were set up on SW-DIST-01. The user confirmed that SW-DIST-01 is the same switch type as SW-Voice and that the switch setup is good. The exact verification command output was not saved in this log, so capture it during the next session if needed.

## Commands used or planned
The trunk configuration used on the switch-to-switch link was:

```cisco
interface Ethernet1/0
 description TRUNK-TO-SW-VOICE
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 30
 no shutdown
```

If the switch rejects the encapsulation command, use the supported commands for that image and check the trunk state before calling it verified.

## Next steps
1. Start CORE-01 and collect its model, VLAN, interface, and EtherChannel information.
2. Check the actual core-to-core and core-to-distribution port connections in GNS3. Do not move existing cables or guess interface numbers.
3. Configure VLAN 30 on the core/distribution path as needed.
4. Decide which device will be the voice VLAN gateway and which device will provide DHCP.
5. Test reachability between the CME router and the voice gateway.
6. Investigate the 3745 flash-storage issue and confirm CME compatibility.
7. Connect the Windows 11 softphone VM through the planned VMware `VOIP-LAB` segment and GNS3 Cloud1 path.
8. Test phone registration and calls only after the network path and CME requirements are confirmed.

## Lab safety and documentation notes
- The existing GNS3 cables have not been changed.
- Do not mark a feature as working until it has been tested.
- Keep the lab isolated from the home network.
- Remove passwords and other private information before publishing configurations.

## Session status
Paused after setting up the voice access switch and its distribution-switch connection. Next session starts with CORE-01.

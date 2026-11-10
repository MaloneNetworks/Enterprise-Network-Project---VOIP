# Device List

This page tracks the equipment in the lab. Add the real model, software version, ports, and current status as each device is checked. Do not guess based on the icon in GNS3.

## Devices checked so far

| Device name | What it does | GNS3 device/image | Software | Ports | Current status |
|---|---|---|---|---|---|
| CORE-01 | Main network switch; handles routing between networks | Cisco IOU L3 | To check | 4 ports reported; names still need checking | Added; not configured |
| CORE-02 | Backup/main network switch | Cisco IOU L3 | To check | 4 ports reported; names still need checking | Added; not configured |
| SW-DIST-01 | Connects the core switches to the access switches | Cisco IOU L2 | To check | To check | Added; not configured |
| SW-Admin | Connects admin computers | Cisco IOU L2 | To check | To check | Added; not configured |
| SW-ENG | Connects engineering computers | Cisco IOU L2 | To check | To check | Added; not configured |
| SW-Voice | Connects voice devices and the CME router | Cisco IOU L2 | To check | To check | Added; configuration in progress |
| SW-SRV | Connects internal servers | Cisco IOU L2 | To check | To check | Added; not configured |
| HQ-EDGE | Connects the main office to the internet/WAN | GNS3 device; exact model unknown | To check | To check | Added; not configured |
| R-Branch | Router at the branch office | GNS3 device; exact model unknown | To check | To check | Added; not configured |
| R-CME-01 | Handles phone calls (CME candidate) | Cisco 3745 | IOS 12.4(25d), C3745-ADVENTERPRISEK9-M | FastEthernet ports; check exact links | Boots; CME support and storage still need checking |
| ASA-HQ-01 | Cisco firewall | ASA image; exact version unknown | To check | To check | Added; not configured |
| FortiGate | Fortinet firewall | Exact image/version unknown | To check | To check | Added; not configured |
| VOIP-PHONE-01 | Windows computer that will run the softphone | Windows 11 VMware VM | To check | NAT + VMware LAN Segment named VOIP-LAB | Installed; GNS3 connection not tested |
| GNS3 VM | Runs the GNS3 network devices | GNS3 VM in VMware | To check | eth0 and eth1 reported | eth1 is intended for VOIP-LAB; not tested |

## Devices still to check

Add the internet cloud, ISP routers, DMZ switch and servers, branch switch and PC, office PCs, and any other devices in the GNS3 project.

## Commands that help identify a Cisco device

These commands show the model, software, ports, neighbors, VLANs, and storage:

```text
show version
show inventory
show ip interface brief
show interfaces
show cdp neighbors detail
show vlan brief
show interfaces trunk
show etherchannel summary
show file systems
```

Some commands are not available on every device. If a command is rejected, note that and move on.

## Cisco 3745 storage note

The 3745 reported that its flash storage was in a REMOVED state. We need to check the GNS3 device settings and available storage before trying to add CME files. The router starting successfully does not prove that CME will work.

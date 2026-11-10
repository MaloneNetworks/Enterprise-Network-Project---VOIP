# Device Inventory

Record actual appliance names, templates, versions, interfaces, and status. Do not infer models from topology icons.

## Confirmed / reported inventory

| Lab hostname | Intended role | Appliance/template | Software version | Interfaces | Status / notes |
|---|---|---|---|---|---|
| CORE-01 | Layer 3 core | Cisco IOU L3 | To record | 4 ports reported; exact names to verify | Placed; not configured |
| CORE-02 | Layer 3 core | Cisco IOU L3 | To record | 4 ports reported; exact names to verify | Placed; not configured |
| SW-DIST-01 | Distribution | Cisco IOU L2 | To record | To inventory | Placed; not configured |
| SW-Admin | Admin access | Cisco IOU L2 | To record | To inventory | Placed; not configured |
| SW-ENG | Engineering access | Cisco IOU L2 | To record | To inventory | Placed; not configured |
| SW-Voice | Voice access | Cisco IOU L2 | To record | To inventory | Placed; not configured |
| SW-SRV | Server access | Cisco IOU L2 | To record | To inventory | Placed; not configured |
| HQ-EDGE | HQ edge routing | Existing GNS3 appliance; model TBD | To record | To inventory | Placed; not configured |
| R-Branch | Branch routing | Existing GNS3 appliance; model TBD | To record | To inventory | Placed; not configured |
| R-CME-01 | VoIP call-control candidate | Cisco 3745 | IOS 12.4(25d), C3745-ADVENTERPRISEK9-M | FastEthernet interfaces to verify | Candidate; CME compatibility and storage pending |
| ASA-HQ-01 | Perimeter / DMZ firewall | ASA appliance; exact template TBD | To record | To inventory | Placed; not configured |
| FortiGate | Enterprise firewall practice | FortiGate appliance; exact image/version TBD | To record | To inventory | Placed; not configured |
| VOIP-PHONE-01 | Softphone endpoint VM | Windows 11 VMware VM | To record | NAT + VMware LAN Segment VOIP-LAB | Installed; GNS3 bridge path pending |
| GNS3 VM | GNS3 compute/server | GNS3 VM | To record | eth0 and eth1 reported | eth1 intended for VOIP-LAB; bridge not yet validated |

## Topology inventory still required

Record all remaining ISP routers/clouds, DMZ switch and servers, branch access switch and PC, HQ endpoints, and any additional appliances visible in the GNS3 workspace. Confirm each node's exact template and interface count from GNS3.

## Cisco IOS inventory commands

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

Some commands are platform-dependent; unsupported commands can be skipped.

## Storage note

Cisco 3745 previously reported `flash:` in a REMOVED state. Record `show file systems` and inspect GNS3 template storage settings before deciding how to provide flash or CME files. Do not assume CME is available just because the router boots.

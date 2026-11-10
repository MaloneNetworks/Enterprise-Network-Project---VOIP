# Device Inventory

Record actual appliance names, templates, versions, interfaces, and status. Do not infer models from topology icons.

| Lab hostname | Intended role | Appliance/template | Software version | Interfaces | Status / notes |
|---|---|---|---|---|---|
| CORE-01 | Primary core switching | To verify | To verify | To inventory | Existing topology |
| CORE-02 | Secondary core switching | To verify | To verify | To inventory | Existing topology |
| SW-DIST-01 | Distribution | To verify | To verify | To inventory | Existing topology |
| SW-Voice | Voice/access switching | To verify | To verify | To inventory | Existing topology |
| HQ-EDGE | HQ edge routing | To verify | To verify | To inventory | Existing topology |
| R-Branch | Branch routing | To verify | To verify | To inventory | Existing topology |
| R-CME-01 | VoIP call-control candidate | Cisco 3745 | IOS 12.4(25d), C3745-ADVENTERPRISEK9-M | Verify | Flash reports unavailable; CME compatibility pending |
| ASA | Perimeter firewall | To verify | To verify | To inventory | Existing topology |
| VOIP-PHONE-01 | Softphone endpoint VM | Windows 11 VMware VM | To record | NAT + VOIP-LAB | Installed; network integration pending |
| GNS3 VM | GNS3 compute/server | GNS3 VM | To record | eth0, eth1 | eth1 intended for VOIP-LAB |

## Cisco IOS inventory commands
```text
show version
show inventory
show ip interface brief
show interfaces status
show cdp neighbors detail
show vlan brief
show interfaces trunk
show file systems
```

## Storage note
Cisco 3745 previously reported `flash:` in a REMOVED state. Record `show file systems` and inspect GNS3 template storage settings before deciding how to provide flash.

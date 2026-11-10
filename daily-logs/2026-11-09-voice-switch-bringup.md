# Lab Notes — November 9, 2026

## What I worked on
Started checking the router and switch that will connect the lab phones.

## Router check: R-CME-01

Commands used:

```cisco
show version
show ip interface brief
show file systems
show flash:
```

What I found:
- The router is a Cisco 3745.
- It runs IOS 12.4(25d), using the Advanced Enterprise image.
- The router reports about 256 MB of memory.
- Port FastEthernet0/0 has address `10.10.30.10` and showed as up/up.
- The router says its flash storage is missing or unavailable.
- We still need to find out whether this router can run the CME phone software and where the required files could be stored.

## Voice switch check: SW-Voice

- The switch uses the Cisco IOU L2 image.
- The switch ports were listed in the default VLAN 1.
- VLANs 1002–1005 were also listed; these are standard built-in VLANs.
- The switch has not been fully set up for the phone network yet.

## Planned switch connections

| Switch port | Connected device | What the port should do |
|---|---|---|
| Ethernet0/0 | SW-DIST-01 | Carry VLAN 30 between switches |
| Ethernet0/1 | R-CME-01 FastEthernet0/0 | Put the CME router in VLAN 30 |

## Problem found on the switch

When I tried to make Ethernet0/0 a trunk, the switch returned this message:

```text
An interface whose trunk encapsulation is "Auto" can not be configured to "trunk" mode.
```

In plain terms, the switch is set to choose the trunk type automatically, and it will not let me turn trunk mode on until the type is set.

The next command to try is:

```cisco
configure terminal
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 30
 no shutdown
end
```

This has **not** been confirmed to work yet. If the first command is rejected, save the exact error and check what this switch image supports. Do not mark the trunk as working until `show interfaces trunk` confirms it.

The router-facing port should eventually be set up like this, but it has **not** been confirmed as applied:

```cisco
configure terminal
interface Ethernet0/1
 description CONNECTION-TO-R-CME-01
 switchport mode access
 switchport access vlan 30
 no shutdown
end
```

## Progress

- [x] Router starts.
- [x] Router software version checked.
- [x] Router FastEthernet0/0 address checked.
- [x] Cisco IOU L2 voice switch identified.
- [x] Current VLAN list checked.
- [ ] Create and confirm VLAN 30.
- [ ] Fix the trunk setup on SW-Voice Ethernet0/0.
- [ ] Set and check SW-Voice Ethernet0/1 for VLAN 30.
- [ ] Set up VLAN 30 on SW-DIST-01 and the links back to the core.
- [ ] Test that the CME router can be reached.
- [ ] Fix or work around the router's missing flash storage.
- [ ] Connect the Windows phone VM and test a softphone.

## Notes
The existing GNS3 cables have not been moved. Planned settings are labeled as planned until they have been entered and tested.

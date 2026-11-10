# Daily Log — 2026-11-09

## Focus
Bring up the VoIP access switch and validate the CME router connection.

## Topology reference
- Using the user's GNS3 topology v2.0; preserve existing links.
- R-CME-01 FastEthernet0/0 connects to SW-Voice Ethernet0/1.
- SW-Voice Ethernet0/0 connects upstream to SW-DIST-01. The distribution-side label appears to be Ethernet1/1; verify in GNS3 before relying on it.

## R-CME-01 inspection
Commands run: show version, show ip interface brief, show file systems, show flash:

Observed:
- Cisco 3745 / 3700 Software, image C3745-ADVENTERPRISEK9-M.
- IOS 12.4(25d), Advanced Enterprise.
- Approximately 256 MB RAM reported by show version.
- FastEthernet0/0 has 10.10.30.10 and showed up/up in show ip interface brief.
- show file systems lists flash prefixes, but show flash: returns Device 'flash:' is in REMOVED state and No device available.
- CME capability and usable storage for CME/phone files are not confirmed. Do not assume CME is ready based only on the IOS image name.

## SW-Voice inspection
- Image: Cisco IOU L2.
- show vlan brief showed VLAN 1 (default) active with switch ports assigned to it; legacy VLANs 1002–1005 were also present.
- The first attempt, show vlan br, was rejected; the abbreviated command sho vla br succeeded.
- The switch has not yet been fully configured for this lab.

## Intended voice switch port plan
| Interface | Connection | Intended role |
|---|---|---|
| Ethernet0/0 | SW-DIST-01 | 802.1Q trunk carrying VLAN 30 |
| Ethernet0/1 | R-CME-01 FastEthernet0/0 | Access VLAN 30 |

## Trunk encapsulation issue
The trunk command on Ethernet0/0 was rejected with this message:

> An interface whose trunk encapsulation is "Auto" can not be configured to "trunk" mode.

Next troubleshooting step proposed but not yet confirmed successful:

```cisco
configure terminal
interface Ethernet0/0
 switchport trunk encapsulation dot1q
 switchport mode trunk
 switchport trunk allowed vlan 30
 no shutdown
end
```

If the encapsulation command is unavailable or rejected, capture the exact error and inspect show version, show interfaces Ethernet0/0 switchport, and available switchport commands before choosing an image-specific alternative. Do not claim the trunk is configured until show interfaces trunk verifies it.

Intended CME-facing access configuration (not yet confirmed as applied):

```cisco
configure terminal
interface Ethernet0/1
 description CONNECTION-TO-R-CME-01
 switchport mode access
 switchport access vlan 30
 no shutdown
end
```

## Current status
- [x] R-CME-01 boots and IOS version identified.
- [x] R-CME-01 Fa0/0 IP observed as 10.10.30.10 and up/up.
- [x] SW-Voice identified as Cisco IOU L2.
- [x] Default VLAN state inspected.
- [ ] Confirm VLAN 30 creation.
- [ ] Resolve trunk encapsulation issue on SW-Voice Ethernet0/0.
- [ ] Configure/verify SW-Voice Ethernet0/1 as access VLAN 30.
- [ ] Configure SW-DIST-01 and carry VLAN 30 end-to-end.
- [ ] Verify gateway/routing and reachability to 10.10.30.10.
- [ ] Resolve CME storage/flash and release compatibility.
- [ ] Connect Windows VOIP-LAB VM through GNS3 Cloud and test a softphone.

## Notes
No changes were made to existing topology cabling. Treat unverified commands and design values as planned, not completed. Save sanitized configurations and test results as work progresses.

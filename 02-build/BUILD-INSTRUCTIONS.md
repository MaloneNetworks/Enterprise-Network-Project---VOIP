# Enterprise Network & VoIP Lab — Build Instructions

> **Status:** Working build procedure. Not all steps have been performed. Follow the sequence and mark a step complete only after verifying it.

## 1. Before you begin

1. Open the GNS3 project and save a backup copy.
2. Do not move existing cables as part of routine setup.
3. Open the [network cut sheet](CUT-SHEET.md), [device inventory](device-inventory.md), [IP plan](ip-addressing.md), and [port map](port-mapping.md).
4. Confirm the actual device models, images, software versions, and interface names.
5. Make sure the lab is isolated from the home network and physical network interfaces.
6. Record the current state before changing a device.

## 2. Baseline discovery

Perform discovery before applying configurations. On Cisco IOS devices, use the commands that the image supports:

```cisco
enable
show version
show ip interface brief
show interfaces
show cdp neighbors detail
show lldp neighbors detail
show vlan brief
show interfaces trunk
show etherchannel summary
show file systems
show running-config
```

Some commands may not exist on a particular IOU or router image. Record unsupported commands rather than assuming a feature is available.

Update the cut sheet with:
- Exact hostname and device image.
- Software version.
- Exact interface names.
- Cable connections at both ends.
- Current interface state.
- Features supported by the image.

## 3. Finalize the design before configuring

1. Confirm VLAN IDs and names.
2. Confirm each subnet and mask.
3. Decide which device routes each VLAN.
4. Decide whether HSRP is required and supported.
5. Decide which device provides DHCP and DNS.
6. Decide how management access will work.
7. Assign fixed addresses for servers and network devices.
8. Assign IPs to routed links between routers and firewalls.
9. Update the cut sheet and draw.io diagram.

Do not configure a proposed gateway or address just because it appears in an early draft.

## 4. Configure the switching layer

### 4.1 Initial device setup

For each switch:
1. Set the hostname.
2. Set a suitable enable secret and secure management access.
3. Configure only the management settings that have been approved.
4. Save a baseline configuration.
5. Verify the hostname and interface status.

Do not paste a generic configuration until the exact image and interface names have been checked.

### 4.2 VLANs

Create only the VLANs approved in the cut sheet. The current draft VLANs are 10, 20, 30, 40, 60, 70, 100, and 999.

After creating them, verify:

```cisco
show vlan brief
```

### 4.3 Trunks and access ports

1. Use the cut sheet to identify each switch-to-switch link.
2. Configure the correct trunk mode and allowed VLAN list supported by the image.
3. Configure endpoint-facing ports as access ports in the correct VLAN.
4. Configure voice VLAN behavior only on ports intended for IP phones and only where the switch image supports it.
5. Verify trunk state and VLAN membership.

```cisco
show interfaces trunk
show interfaces status
show vlan brief
```

### 4.4 Core peer links and LACP

The two core switches have four ports each. Verify the actual two peer-link cable endpoints before configuring an EtherChannel. If two suitable links exist and both images support LACP:

1. Confirm the two physical links have matching speed/duplex and compatible settings.
2. Configure the same channel-group and compatible trunk settings at both ends.
3. Verify that the port-channel forms and both links are bundled.
4. Do not assume that a configured channel is working until the operational state confirms it.

```cisco
show etherchannel summary
show interfaces port-channel
```

### 4.5 Spanning Tree and redundancy

1. Decide the intended root bridge for each VLAN.
2. Configure root preferences only after the topology and redundant paths are known.
3. Check for unexpected blocked or looping paths.
4. Test failover only after saving a known-good configuration.

## 5. Configure Layer 3 routing

1. Confirm which device owns each VLAN gateway.
2. Configure SVIs or routed interfaces according to the approved design.
3. Configure HSRP only if supported and selected.
4. Configure routes between internal networks and toward the WAN/firewall.
5. Verify interface state, routing table, and gateway reachability.

Useful checks:

```cisco
show ip interface brief
show ip route
show standby brief
show running-config
```

If the image does not support a command or feature, stop and choose a supported design rather than forcing the configuration.

## 6. Configure firewalls and the DMZ

1. Confirm the firewall image/version and physical/logical port mapping.
2. Identify outside, inside, transit, and DMZ interfaces.
3. Assign addresses from the approved routed-link and DMZ plan.
4. Define the intended traffic flows before writing policies.
5. Configure NAT and access policies in a controlled order.
6. Test permitted flows and denied flows separately.
7. Save the configuration and document the results.

Do not copy ASA or FortiGate commands between different software versions without checking syntax and feature support.

## 7. Configure the branch network

1. Confirm branch router and switch models, ports, and links.
2. Configure the branch LAN using the approved IP plan.
3. Configure WAN addressing and routing.
4. Add GRE or IPsec only if the selected images support the required features.
5. Verify tunnel state and intended routes.
6. Test access to approved HQ resources and confirm that unrelated traffic is not allowed.

## 8. Bring up the VMware-to-GNS3 voice path

The intended path is Windows 11 VM → VMware LAN Segment `VOIP-LAB` → GNS3 VM `eth1` → GNS3 Cloud node → SW-Voice → VLAN 30 → R-CME-01.

1. Confirm the Windows VM has a NAT adapter for internet access and a separate adapter attached to `VOIP-LAB`.
2. Confirm the GNS3 VM has the intended second adapter connected to the same VMware LAN Segment.
3. Confirm the GNS3 VM sees the second interface and that it is up.
4. Bind the GNS3 Cloud node to the correct interface.
5. Connect Cloud1 to the correct SW-Voice port.
6. Verify VLAN 30 is carried across the required trunk and the Cloud-facing port is configured appropriately for the design.
7. Check the Windows VM's adapter address and test reachability to the voice gateway when one exists.

Do not bridge the lab into the home LAN. If the Windows VM can reach the internet through NAT, that does not prove the lab-side adapter is connected correctly.

## 9. Validate the CME router before configuring CME

The current CME candidate is Cisco 3745, `R-CME-01`. IOS 12.4(25d) and an Advanced Enterprise image have been reported. The router's Fa0/0 address was set to `10.10.30.10`.

Before attempting CME setup:

1. Check `show version` for the exact IOS image and memory.
2. Check `show file systems` and `dir` for usable storage.
3. Investigate the previously reported flash state of `REMOVED`.
4. Confirm the IOS release supports the CME version and required telephony features.
5. Confirm phone firmware files and TFTP requirements.
6. Confirm the selected softphone can register with the planned CME setup.
7. Confirm VLAN 30 connectivity and the final voice gateway/DHCP design.

Do not proceed to phone provisioning until these checks pass. A router with an IP address is not necessarily a working CME platform.

## 10. Configure CME and the first softphone

Only after Step 9 passes:

1. Select and document a compatible CME/IOS and softphone combination.
2. Configure the voice network and DHCP scope on the chosen DHCP server.
3. Add phone provisioning options such as TFTP information only after the TFTP service and file paths are known.
4. Configure CME telephony service and a first directory number using syntax supported by the installed IOS.
5. Configure the softphone with the required account/extension and server details.
6. Confirm registration.
7. Place a test call and document the result.
8. Add additional extensions and endpoints only after the first call works.

The exact CME commands will be written as a separate device-specific procedure after the IOS, storage, CME support, and phone requirements have been verified.

## 11. Verification and troubleshooting

For each stage:
1. Check interface status.
2. Check VLAN membership and trunk state.
3. Check MAC address learning and ARP where relevant.
4. Check routing tables.
5. Test expected connectivity.
6. Test traffic that should be blocked.
7. Save outputs or screenshots as evidence.
8. Update the cut sheet, topology, and test plan.

## 12. Save and document

After a successful stage:
- Save device configurations.
- Save a GNS3 project checkpoint.
- Update the cut sheet and diagram.
- Record commands and verification results.
- Remove credentials and secrets from any files before committing them to GitHub.

## 13. Controlled troubleshooting exercises

The planned Python fault-injection exercise must be limited to this isolated lab. Use only known, reversible faults, one at a time. Include a dry-run, a known-good backup, a reset path, and verification. Never let the script modify the host OS, VMware NAT, physical NICs, home router, or external networks.

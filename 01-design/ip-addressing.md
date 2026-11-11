# IP Address Plan

> **Status: Draft.** These are planned addresses, not proof that the network is configured. Check the GNS3 diagram and decide which device owns each gateway before using these addresses.

## VLAN and network plan

A **VLAN** is a way to keep groups of devices on separate networks, even when they use the same physical switches. A **gateway** is the address a device uses when it needs to reach another network.

| VLAN | Name | Network | Planned gateway | Used for |
|---:|---|---|---|---|
| 10 | ADMIN | 10.10.10.0/24 | 10.10.10.1 | Admin computers |
| 20 | ENGINEERING | 10.10.20.0/24 | 10.10.20.1 | Engineering computers |
| 30 | VOICE | 10.10.30.0/24 | 10.10.30.1 | Phones and CME |
| 40 | SERVERS | 10.10.40.0/24 | 10.10.40.1 | Internal servers |
| 60 | MANAGEMENT | 10.10.60.0/24 | 10.10.60.1 | Switch and network-device management |
| 70 | BRANCH | 10.10.70.0/24 | 10.10.70.1 | Branch office computers |
| 100 | DMZ | 172.16.80.0/24 | To decide | Servers that may need outside access |
| 999 | NATIVE-BLACKHOLE | No IP network | None | Unused VLAN for trunk links, if supported |

The VLAN numbers follow the current diagram. The network and gateway addresses are still a draft. Check them against the actual project before configuring devices.

## Addresses we may reserve

| Network | Device or use | Planned address | Notes |
|---|---|---|---|
| VLAN 10 | Main/backup gateway address | 10.10.10.1 | Only if we use HSRP |
| VLAN 20 | Main/backup gateway address | 10.10.20.1 | Only if we use HSRP |
| VLAN 30 | Main/backup gateway address | 10.10.30.1 | Only if we use HSRP |
| VLAN 40 | Main/backup gateway address | 10.10.40.1 | Only if we use HSRP |
| VLAN 60 | Main/backup gateway address | 10.10.60.1 | Only if we use HSRP |
| VLAN 70 | Branch gateway address | 10.10.70.1 | Depends on the branch design |
| VLAN 30 | R-CME-01 | 10.10.30.10 | Router address already entered; still needs network testing |
| VLAN 30 | Windows softphone VM | DHCP or 10.10.30.100 | Do not assign until the connection and DHCP plan work |
| VLAN 40 | Internal servers | 10.10.40.0/24 | Pick individual addresses after checking the servers |
| VLAN 60 | Switch management | 10.10.60.0/24 | Pick individual addresses after checking the switches |

HSRP is a feature that lets two routers or switches share one gateway address. The .1 addresses above should only be used as shared gateway addresses if we actually configure HSRP.

## ASA-to-FortiGate transit assignment

| Device | Interface | Address |
|---|---|---|
| ASA-HQ-01 | E1 | `10.255.0.9/30` |
| FortiGate | E0 | `10.255.0.10/30` |

Network: `10.255.0.8/30` · Usable addresses: `10.255.0.9–10.255.0.10` · Broadcast: `10.255.0.11`.

This is the agreed addressing plan. It has not yet been configured or tested.

## DHCP plan

DHCP automatically gives devices their IP settings. These ranges are ideas only; no DHCP service has been chosen yet.

| VLAN | Possible address range | Notes |
|---:|---|---|
| 10 | 10.10.10.100–10.10.10.199 | Keep gateway and network-device addresses out of this range |
| 20 | 10.10.20.100–10.10.20.199 | Keep gateway and network-device addresses out of this range |
| 30 | 10.10.30.100–10.10.30.199 | CME may need to provide phone setup information |
| 40 | Mostly static addresses | Servers should have addresses that do not change |
| 60 | Mostly static addresses | Network devices should have addresses that do not change |
| 70 | 10.10.70.100–10.10.70.199 | Keep gateway and branch-service addresses out of this range |
| 100 | Static addresses | DMZ servers should have fixed addresses |

We still need to choose which device gives out addresses. Only one DHCP service should manage each address range. If phones need a TFTP server address (often sent using DHCP Option 150), we will add it after CME and TFTP are confirmed to work.

## Links between routers and firewalls

These links need their own IP addresses. We should not guess them. First check the exact ports and labels in the GNS3 diagram:

- ISP1 to HQ-EDGE
- ISP2 to HQ-EDGE
- HQ-EDGE to ASA-HQ-01
- ASA-HQ-01 to FortiGate: network `10.255.0.8/30`; ASA E1 `10.255.0.9/30`, FortiGate E0 `10.255.0.10/30`
- FortiGate to CORE-01 and CORE-02
- Branch internet connection and GRE/IPsec tunnel
- DMZ connections

A /30 or /31 network is often used for a direct router-to-router link. We will choose one that the device supports and write down the address at both ends.

## Address rules

1. Do not give two devices the same IP address.
2. Keep fixed server and network-device addresses out of DHCP ranges.
3. Use .1 as a shared gateway only if we set up HSRP.
4. Write down which device provides DHCP and DNS.
5. Do not assume the core switches are the gateway for every VLAN.
6. Check the diagram and this plan together before entering configurations.

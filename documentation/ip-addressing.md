# IP Addressing Plan

> **Draft only.** Proposed voice details must be reconciled with the complete enterprise topology before configuration.

## Proposed voice subnet
| Purpose | VLAN | Network | Address |
|---|---:|---|---|
| Voice network | 30 | 10.10.30.0/24 | — |
| Voice gateway | 30 | 10.10.30.0/24 | 10.10.30.1 (proposed) |
| CME candidate | 30 | 10.10.30.0/24 | 10.10.30.10 (proposed) |
| Softphone endpoints | 30 | 10.10.30.0/24 | DHCP pool TBD |
| TFTP / Option 150 | 30 | 10.10.30.0/24 | 10.10.30.10 only if CME/TFTP resides there |

## Full enterprise addressing table
| VLAN | Function | Subnet | Gateway | DHCP source | Notes |
|---:|---|---|---|---|---|
| 10 | Administration (proposed) | TBD | TBD | TBD | Validate |
| 20 | Engineering (proposed) | TBD | TBD | TBD | Validate |
| 30 | Voice | 10.10.30.0/24 (proposed) | 10.10.30.1 (proposed) | TBD | Confirm gateway ownership |
| 40 | Servers (proposed) | TBD | TBD | TBD | Validate |
| 60 | Management (proposed) | TBD | TBD | TBD | Validate |
| 70 | Branch data (proposed) | TBD | TBD | TBD | Validate |
| 100 | DMZ (proposed) | TBD | TBD | TBD | Reconcile firewall design |
| 999 | Native/unused (proposed) | No SVI planned | None | None | Confirm platform policy |

## Address allocation rules
- Reserve low addresses for gateways and infrastructure.
- Exclude static infrastructure addresses from DHCP pools.
- Document DHCP relay/helper behavior.
- Confirm whether VLAN 30 gateway is an SVI, firewall interface, or router interface.
- Avoid duplicate gateways and DHCP servers.

# Port Mapping

Authoritative record of GNS3 links and interface assignments. Populate from the actual topology before applying switch configuration.

| Link | Device A | Interface A | Device B | Interface B | Purpose | VLAN/mode | Verified |
|---|---|---|---|---|---|---|---|
| L-001 | Cloud1 | eth1 (GNS3 VM host interface) | SW-Voice | TBD | Windows VM VOIP-LAB bridge | Access VLAN 30 planned | No |
| L-002 | R-CME-01 | FastEthernet0/0 candidate | SW-Voice | TBD | CME connection | Access VLAN 30 planned | No |
| L-003 | SW-Voice | TBD | SW-DIST-01 | TBD | Access/distribution uplink | Trunk planned | No |
| L-004 | SW-DIST-01 | TBD | CORE-01 | TBD | Distribution/core | Trunk planned | No |
| L-005 | SW-DIST-01 | TBD | CORE-02 | TBD | Redundant distribution/core | Trunk planned | No |

## Rules
- Replace TBD using actual GNS3 interfaces.
- Do not assume port numbering across switch images.
- Record both ends of every link.
- Verify trunks/access VLANs with device commands.
- Keep this file synchronized with the topology diagram.

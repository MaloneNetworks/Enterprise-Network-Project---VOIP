# Network Chaos Lab

A planned fault-injection and troubleshooting extension for the isolated GNS3 enterprise lab.

> Status: design only. No fault-injection script currently exists. Implement only after the baseline network is configured, backed up, and validated.

## Initial five scenarios

| ID | Scenario | Controlled fault example | Expected symptom |
|---|---|---|---|
| CHAOS-01 | VLAN/access port | Put a designated test access port in the wrong VLAN | Endpoint loses expected subnet/service access |
| CHAOS-02 | Trunk allowed VLAN | Remove one selected VLAN from a designated trunk | One VLAN fails across the affected uplink |
| CHAOS-03 | Routing | Add a reversible incorrect route or disable a designated lab-only routed interface | Selected remote subnet becomes unreachable |
| CHAOS-04 | HSRP | Change a designated group's priority or shut a pre-approved test interface | Gateway role changes or redundancy is lost |
| CHAOS-05 | Firewall policy | Add a temporary deny rule for one defined test flow | Selected service becomes blocked |

## Workflow
1. Confirm the GNS3 project is isolated.
2. Verify a known-good baseline and create backups.
3. Randomly select one enabled scenario.
4. Apply only its pre-defined reversible change.
5. Show symptoms without revealing the answer.
6. Let the learner diagnose and repair manually.
7. Verify recovery; restore the baseline if needed.

## Safety requirements
- Require explicit confirmation of the lab project and target devices.
- Refuse to run without backups and target mappings.
- Use only pre-defined interfaces, VLANs, routes, and firewall objects.
- Never target the host OS, VMware NAT, physical NICs, home router, or external networks.
- Run one fault at a time; include dry-run, status, verify, and reset operations.
- Keep credentials out of source and logs.

## Implementation approach
A Python controller can use the GNS3 API to inspect projects, nodes, and links, then use device console automation or SSH for appliance-specific changes. GNS3 API alone does not configure every appliance. Build and test one scenario at a time.

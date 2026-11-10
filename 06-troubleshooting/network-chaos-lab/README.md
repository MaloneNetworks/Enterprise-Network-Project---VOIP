# Network Troubleshooting Challenges

This is a planned feature for the GNS3 lab. It will create one safe, controlled network problem at a time so I can practice finding and fixing it.

> **Status: Planning only. There is no script yet.** Build this only after the main network works, has been tested, and has a backup.

## First five challenges

| ID | What breaks | Example of the planned change | What you may notice |
|---|---|---|---|
| CHAOS-01 | A computer's VLAN | Put a test computer port in the wrong VLAN | The computer cannot reach the network it should use |
| CHAOS-02 | A trunk link | Remove one VLAN from a test trunk | Devices in that VLAN lose connection across that link |
| CHAOS-03 | Routing | Add a wrong route or turn off a test-only routed link | A remote network cannot be reached |
| CHAOS-04 | Backup gateway | Change the priority of a test HSRP group or turn off an approved test link | The main/backup gateway role changes or backup service is lost |
| CHAOS-05 | Firewall rule | Add a temporary block for one test connection | One service stops responding |

## How a challenge should work

1. Check that the GNS3 project is isolated from real networks.
2. Check that a working backup exists.
3. Pick one challenge that has been approved.
4. Make only the planned change for that challenge.
5. Show the symptoms, but do not show the answer.
6. Let me find and fix the problem.
7. Test the network and restore the normal settings if needed.

## Safety rules

- Ask for confirmation before changing a device.
- Do not run without a backup and a clear list of target devices.
- Only change ports, VLANs, routes, or firewall rules that were chosen ahead of time.
- Never change the host computer, VMware NAT, physical network cards, home router, or internet-facing networks.
- Run one problem at a time.
- Include preview, status, test, and reset options.
- Never save passwords in the script or its logs.

## How it may be built

A Python program could use the GNS3 API to look at the project, devices, and links. It may then use each device's console or SSH connection to make the planned change. The GNS3 API does not configure every kind of router or firewall by itself, so each device type may need a different method.

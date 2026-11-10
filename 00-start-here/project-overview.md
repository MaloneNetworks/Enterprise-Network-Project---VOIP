# What This Project Is

## The goal

Build a large business-style network in GNS3 and VMware. Use it to practice setting up networks, connecting offices, securing traffic, running phone service, and fixing problems.

## What the lab will include

- Separate networks for different teams using VLANs.
- Switches that connect the networks and help keep them running if a link fails.
- Routers that move traffic between networks and offices.
- Cisco ASA and FortiGate firewalls to control what traffic can pass.
- A DMZ, which is a separate network for services that may need to be reached from outside.
- A branch office connected to the main office.
- A voice network with phone extensions and softphones.
- Tests and practice problems to help build troubleshooting skills.

## How the project will be built

1. Keep the current GNS3 layout and check every device and cable.
2. Finish one IP address and VLAN plan.
3. Make small changes and test them before moving on.
4. Check what each device can do before choosing commands.
5. Save proof when something works.
6. Remove passwords and private details before sharing settings.

## What is already known

- GNS3 runs inside VMware Workstation.
- A Windows 11 VM named `VOIP-PHONE-01` is installed.
- The Windows VM has one VMware NAT adapter and a second adapter on a LAN Segment named `VOIP-LAB`.
- GNS3 VM interface `eth1` is planned for the `VOIP-LAB) connection.
- The Cisco 3745 router reports IOS 12.4(25d) and image `C3745-ADVENTERPRISEK9-M`.
- The Cisco 3745 flash storage needs to be fixed or replaced before we can decide whether CME files can be used.

## Things still to decide

- Exact device models, software versions, and port numbers.
- Final VLANs, IP networks, and gateways.
- Which device gives out IP addresses.
- Whether the Cisco 3745 can run the needed CME version.
- Whether the Windows VM can reach GNS3 through Cloud1.

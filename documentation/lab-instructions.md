# Lab Build Instructions

> **Status: Instructions only.** These steps have not all been completed. Check off a step only after it has been configured and tested.

## Before changing anything

- Keep the current GNS3 layout and cables as they are.
- Check the real device model, software version, ports, and connections before entering commands.
- Save a copy of the project and current settings before making changes.
- Work on one part of the network at a time.
- Keep the lab separate from your home network.
- Remove passwords and other private details before uploading settings to GitHub.

## Step 1 — Check the equipment

1. Write down the GNS3 and VMware versions.
2. Check each device's model and software.
3. Check both ends of every cable in GNS3.
4. Write down the port names and number of ports. The two IOU L3 core switches have four ports each, so do not assume extra ports exist.
5. Check the Cisco 3745 storage and whether it can run the CME version we need.
6. Save a clean copy of the GNS3 project.

## Step 2 — Finish the IP and VLAN plan

1. Compare the VLAN and IP plan with the labels on the GNS3 diagram.
2. Decide which device will be the gateway for each VLAN.
3. Decide which device will hand out IP addresses (DHCP).
4. Decide where DNS and phone setup files (TFTP) will come from.
5. Choose addresses for the internet, firewall, and branch links.

## Step 3 — Set up the switches

1. Create the VLANs we approved.
2. Check the two existing links between CORE-01 and CORE-02 before setting up their LACP bundle. LACP combines links so they work as one logical connection.
3. Choose which switches should be in charge of Spanning Tree. Spanning Tree helps stop switching loops.
4. Set up the existing switch-to-switch links as trunks. A trunk carries more than one VLAN.
5. Set up computer, phone, and server ports in the correct VLANs.
6. Check the VLANs, trunks, LACP bundle, and Spanning Tree.

## Step 4 — Set up routing and backup gateways

1. Set up the gateway addresses based on the approved IP plan.
2. Set up HSRP only if the chosen devices support it and we need a backup gateway.
3. Set up routes between the networks and toward the internet.
4. Check the routing tables and test each gateway.
5. Test a failover, then return the lab to its normal state.

## Step 5 — Set up the firewalls and DMZ

1. Check the firewall models and cable connections.
2. Decide which traffic should be allowed between each network area.
3. Set up firewall rules and NAT (address translation).
4. Set up the DMZ servers.
5. Test traffic that should be allowed and traffic that should be blocked.

## Step 6 — Connect the branch office

1. Set up the internet connection and branch routes.
2. Set up GRE/IPsec only after checking that the router images support it.
3. Check that the tunnel is working and that only the intended branch traffic can pass.

## Step 7 — Set up VoIP

1. Check the Cisco 3745 IOS version, storage, CME support, phone files, and softphone compatibility.
2. Test the VMware VOIP-LAB connection to GNS3 Cloud1.
3. Make sure VLAN 30 reaches the correct gateway and has only one DHCP service.
4. Set up CME, phone extensions, and any required DHCP/TFTP settings.
5. Register the softphone and place test calls.

## Step 8 — Test and practice fixing problems

1. Follow the test list in `testing/test-plan.md`.
2. Save working settings before trying a fault.
3. Introduce only one planned problem at a time, and only inside the lab.
4. Find and fix the problem.
5. Check that the network works again.

## Step 9 — Prepare the portfolio

Save the final diagram, clean device settings, screenshots, test results, and a short walkthrough. Update the main README only when a feature is really working.

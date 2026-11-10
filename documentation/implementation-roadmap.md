# Build Plan

This is the order we'll use to build the lab. A task is only complete after we configure it and test that it works. The numbered sessions are suggestions, not deadlines.

## Stage 1 — Learn what we have and plan it

### 1. Check the devices
- [ ] Write down the GNS3 and VMware versions.
- [ ] Check each router, switch, firewall, and server.
- [ ] Record each device's software and available ports.
- [ ] Write down both ends of every cable in GNS3.
- [ ] Check the Cisco 3745 storage and whether it can run CME.
- Evidence: device list, topology screenshot, and command output.

### 2. Plan the network addresses
- [ ] Confirm each VLAN, network, and gateway.
- [ ] Decide which device gives out IP addresses (DHCP).
- [ ] Decide which addresses must stay reserved for servers and network devices.
- [ ] Check that no two networks use overlapping addresses.

## Stage 2 — Set up the switches

### 3. Set up the core switches
- [ ] Set device names and management access.
- [ ] Create the VLANs we approve.
- [ ] Set up the links between the core switches and the other switches.
- [ ] Set up routing only after we decide which device owns each gateway.
- [ ] Check that VLANs and trunks work.

### 4. Set up backup paths
- [ ] Decide which switch should be the main Spanning Tree switch.
- [ ] Set up HSRP or another supported backup-gateway feature if needed.
- [ ] Test what happens when a main link or device goes down.

### 5. Set up the distribution and access switches
- [ ] Configure the links to each access switch.
- [ ] Set up the ports used by computers, phones, and servers.
- [ ] Record both ends of each link.
- [ ] Check that devices can reach the correct networks.

## Stage 3 — Connect networks and add security

### 6. Set up routing
- [ ] Configure the paths between networks.
- [ ] Check the routing tables and test reachability.
- [ ] Write down any traffic that should be blocked.

### 7. Set up the firewalls and DMZ
- [ ] Confirm firewall models and port connections.
- [ ] Decide which traffic is allowed between network areas.
- [ ] Set up firewall rules and NAT.
- [ ] Test both allowed and blocked traffic.

### 8. Connect the branch office
- [ ] Set up the internet/WAN links.
- [ ] Set up branch routing.
- [ ] Set up GRE/IPsec only if the selected devices support it.
- [ ] Check the tunnel and branch network access.

## Stage 4 — Set up phone service

### 9. Build the voice network
- [ ] Confirm VLAN 30 and its IP network.
- [ ] Carry VLAN 30 across the required switch links.
- [ ] Set the phone-facing switch ports.
- [ ] Connect the VMware VOIP-LAB network to GNS3 Cloud1.
- [ ] Test the connection from Windows to the voice network.

### 10. Check whether CME will work
- [ ] Check the 3745 IOS version and memory.
- [ ] Check whether flash storage is available and large enough.
- [ ] Check that the CME version, phone software, and softphone can work together.
- [ ] Choose a softphone we can legally and practically use.

### 11. Set up the first phone
- [ ] Configure CME after the checks pass.
- [ ] Set up DHCP and TFTP details if the phone needs them.
- [ ] Create the first extension.
- [ ] Test phone registration and a call.

### 12. Add more phones
- [ ] Create more Windows VMs if needed.
- [ ] Give each one its own name and network identity.
- [ ] Add extensions and test calls between them.

## Stage 5 — Test and share the project

### 13. Check security and voice quality
- [ ] Check traffic rules and network separation.
- [ ] Check QoS support if the devices allow it.
- [ ] Make sure management access is not open to everyone.

### 14. Test the whole lab
- [ ] Test VLANs, routing, backup links, firewalls, branch access, DHCP, and phones.
- [ ] Record what worked and what still needs fixing.

### 15. Finish the portfolio
- [ ] Update the diagrams and instructions.
- [ ] Add safe-to-share configurations and screenshots.
- [ ] Record a short walkthrough.
- [ ] Update LinkedIn only with features that have been built and tested.

## When is a stage finished?

A stage is finished when the settings are saved, the tests pass, screenshots or other proof are saved, and the notes match what is really working. Remove passwords and other private information before uploading files.

# Enterprise Network Lab Instructions

> Status: build guide; not yet executed. Mark tasks complete only after testing.

## Ground rules
- Preserve the existing GNS3 topology and cabling.
- Inventory exact appliance models, versions, interfaces, and links before configuration.
- Save baseline configurations before changes.
- Configure one layer at a time and verify each phase.
- Keep the lab isolated; sanitize secrets before committing files.

## Phase 0 — Inventory
1. Record every node's GNS3 template and software version.
2. Verify both endpoints of every GNS3 link.
3. Record interface names and counts, especially the four-port IOU L3 cores.
4. Check the Cisco 3745 flash/storage and CME compatibility.
5. Save an untouched GNS3 project backup.

## Phase 1 — Addressing and VLANs
1. Reconcile the proposed VLANs/subnets in ip-addressing.md with the topology labels.
2. Decide gateway ownership for every VLAN.
3. Decide DHCP authority, relay/helper addresses, DNS, and TFTP/Option 150 behavior.
4. Allocate point-to-point networks for WAN, firewall, and branch links.

## Phase 2 — Switching
1. Create the approved VLANs.
2. Verify the existing two-link core EtherChannel ports and platform support before configuring LACP.
3. Configure spanning-tree root roles.
4. Configure the existing core/distribution links as trunks with explicit allowed VLANs.
5. Configure access uplinks and endpoint access ports.
6. Verify VLANs, trunks, EtherChannel, and spanning tree.

## Phase 3 — Routing and redundancy
1. Configure SVIs or routed interfaces according to the approved gateway plan.
2. Configure HSRP only where supported and required.
3. Configure inter-VLAN and upstream routing.
4. Verify route tables and gateway reachability.
5. Test failover and restore normal operation.

## Phase 4 — WAN, firewalls, and DMZ
1. Configure ISP and HQ edge links using the approved point-to-point plan.
2. Define separate ASA and FortiGate security responsibilities.
3. Configure NAT and least-privilege policies.
4. Configure DMZ servers and test permitted/denied flows.
5. Check routing symmetry and avoid competing gateways.

## Phase 5 — Branch
1. Configure WAN underlay and branch routing.
2. Configure GRE/IPsec only after verifying image support and peer/interface details.
3. Verify tunnel state and allowed branch traffic.

## Phase 6 — VoIP
1. Validate 3745 IOS, flash/storage, CME release support, files, and endpoint protocol compatibility.
2. Validate VMware VOIP-LAB to GNS3 Cloud connectivity.
3. Confirm VLAN 30 routing and a single DHCP authority.
4. Configure CME, directory numbers, DHCP/TFTP settings, and softphone registration.
5. Place test calls and capture evidence.

## Phase 7 — Testing and fault injection
1. Run testing/test-plan.md.
2. Save known-good configurations.
3. Run one controlled fault at a time in the isolated lab.
4. Diagnose, repair, reset, and verify baseline connectivity.

## Phase 8 — Portfolio
Capture final topology, sanitized configs, CLI/GUI evidence, test results, and a walkthrough. Update README status only for features actually implemented and tested.

# Implementation Roadmap

Milestones are complete only after configuration and verification evidence are recorded. Day labels are suggested work sessions, not deadlines.

## Phase 1 — Discovery and design

### 01: Environment inventory
- [ ] Record GNS3 and VMware versions.
- [ ] Inventory router, switch, firewall, and server templates.
- [ ] Record software versions, resources, and interfaces.
- [ ] Record current links and port assignments.
- [ ] Investigate Cisco 3745 flash storage and voice feature support.
- Evidence: inventory, topology screenshot, version outputs.

### 02: Addressing and VLAN plan
- [ ] Confirm VLANs, subnets, gateways, and DHCP scopes.
- [ ] Confirm management and native VLAN policy.
- [ ] Define reservations and exclusions.
- [ ] Check for overlapping subnets.

## Phase 2 — Switching

### 03: Core switching
- [ ] Configure hostnames and management.
- [ ] Create approved VLANs.
- [ ] Configure core links and trunks.
- [ ] Configure Layer 3 interfaces after gateway ownership is agreed.
- [ ] Verify VLANs and trunks.

### 04: Redundancy
- [ ] Define spanning-tree root roles.
- [ ] Configure HSRP or supported first-hop redundancy.
- [ ] Test active/standby behavior and failover.

### 05: Distribution and access
- [ ] Configure distribution uplinks and access ports.
- [ ] Record both ends of every link.
- [ ] Verify spanning tree and Layer 2 reachability.

## Phase 3 — Routing and security

### 06: Routing
- [ ] Configure inter-VLAN routing and routes as designed.
- [ ] Verify route tables and reachability.
- [ ] Document intentional traffic restrictions.

### 07: Firewall and DMZ
- [ ] Confirm firewall platform and interface mappings.
- [ ] Define zones and permitted flows.
- [ ] Configure ACLs and NAT.
- [ ] Verify allowed and denied traffic.

### 08: Branch/WAN
- [ ] Configure ISP and edge links.
- [ ] Configure branch routing.
- [ ] Implement GRE/IPsec only if supported by selected images.
- [ ] Verify tunnel and route behavior.

## Phase 4 — VoIP

### 09: Voice network
- [ ] Confirm VLAN 30 and subnet design.
- [ ] Extend VLAN across required trunks.
- [ ] Configure endpoint access port.
- [ ] Connect Cloud1 to GNS3 VM interface attached to `VOIP-LAB`.
- [ ] Test Layer 2 and Layer 3 connectivity.

### 10: CME validation
- [ ] Confirm 3745 IOS image and memory.
- [ ] Confirm flash device availability/capacity.
- [ ] Confirm compatible CME release, phone model, firmware, and protocol.
- [ ] Select a licensed softphone endpoint.

### 11: Call control and first endpoint
- [ ] Configure CME after compatibility is established.
- [ ] Configure DHCP/TFTP and Option 150 where appropriate.
- [ ] Configure first extension.
- [ ] Test registration and dialing.

### 12: Additional endpoints
- [ ] Create additional VMs with unique hostnames and MAC addresses.
- [ ] Configure extensions.
- [ ] Test calls between endpoints.

## Phase 5 — Validation and publication

### 13: QoS and security
- [ ] Validate QoS support and classification.
- [ ] Review access policies and management exposure.
- [ ] Test segmentation boundaries.

### 14: End-to-end testing
- [ ] Test VLANs, routing, redundancy, firewall, branch, DHCP/TFTP, and VoIP.
- [ ] Record actual results and unresolved issues.

### 15: Portfolio publication
- [ ] Finalize diagrams and documentation.
- [ ] Publish sanitized configurations and evidence.
- [ ] Record demonstration.
- [ ] Update LinkedIn with verified capabilities.

## Definition of done
A milestone is complete when configuration is saved, tests demonstrate expected behavior, evidence is captured, documentation reflects actual behavior, and sensitive/proprietary material is excluded.

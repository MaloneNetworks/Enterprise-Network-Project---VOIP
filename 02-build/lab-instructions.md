# First-Time Lab Startup & Operating Instructions

> **Purpose:** Follow this guide whenever you open the lab. It explains how to prepare, open, start, operate, and safely shut down the existing GNS3 environment.
>
> **Current design reference:** Enterprise Network Baseline v1.3.
>
> **Important:** The topology and cable/interface mapping have been reviewed. This does not mean every device is configured or that end-to-end connectivity works. Start the lab in stages and verify each part.

## 1. What you need

| Software / resource | Purpose |
|---|---|
| Windows host | Computer running the lab |
| VMware Workstation | Runs the GNS3 VM and optional Windows endpoint VM |
| GNS3 desktop application | Opens the project and controls network nodes |
| GNS3 VM | Provides compute resources for supported GNS3 appliances |
| Saved GNS3 project | Contains the actual topology and node connections |
| Appliance images/templates | Required to run the routers, switches, and firewalls |
| Windows 11 endpoint VM | Optional endpoint for network and future softphone testing |

The documentation repository does not automatically include the saved GNS3 project or licensed appliance images. Those must already be available on the computer running the lab.

## 2. Know the project documents

- [Current topology — v1.3](../01-design/topology/Enterprise_Network_BASELINE_v1.3.png): visual layout of the intended network.
- [Network cut sheet](../01-design/cut-sheet-working-draft.md): device names, connections, interfaces, VLANs, and planned addresses.
- [IP addressing plan](../01-design/ip-addressing.md): subnet and address assignments.
- [Device inventory](../01-design/device-inventory.md): device images and known versions.
- [Port mapping](../01-design/port-mapping.md): cable endpoints and interface names.
- [Build instructions](BUILD-INSTRUCTIONS.md): device configuration sequence and verification commands.
- [Test plan](../05-testing/test-plan.md): tests to perform after configuration.

If the live GNS3 project does not match the diagram or cut sheet, stop and reconcile the difference before changing cables or configuring interfaces.

## 3. First-time preparation

1. Start VMware Workstation.
2. Confirm the GNS3 VM is present in the VMware library and is not showing an error.
3. Open GNS3 and confirm it is configured to use the intended GNS3 VM/server.
4. Wait until GNS3 reports that its compute server is connected and ready.
5. Locate the saved Enterprise Network GNS3 project on your computer.
6. Make a backup copy of the project before the first session.
7. Confirm the Windows endpoint VM is available if you plan to use it. It is not required just to start the network topology.

**Do not create a new topology from scratch if the saved project already exists.** Open the existing project so its nodes and cable connections are preserved.

## 4. Open the GNS3 project

1. Open the GNS3 desktop application.
2. Wait until the GNS3 server/compute status is connected.
3. Select **File → Open Project**.
4. Browse to the saved Enterprise Network project and open its `.gns3` project file.
5. If GNS3 asks whether to open or restore a project, choose the option that opens the existing saved project.
6. Check that the topology loads and the expected devices and links are visible.
7. Compare the layout with the v1.3 topology image and network cut sheet.
8. Save the project once it has loaded successfully.

The exact project filename and storage path depend on where the project was saved. Cloning this documentation repository does not automatically download or open the GNS3 project file.

## 5. Check the topology before powering on devices

- Confirm the expected routers, firewalls, switches, servers, and endpoint nodes are present.
- Confirm the cables are connected to the intended interfaces.
- Confirm no node reports a missing-image or appliance-template error.
- Confirm the GNS3 VM/server is connected.
- Do not delete, move, or reconnect cables just because a link is red or a device is powered off. A red link can be normal before both endpoints are running or configured.
- A visible cable does not prove that the link is operational.

If an appliance image is missing, resolve the image/template issue rather than substituting another image without updating the inventory and documentation.

## 6. Start the lab in stages

Do not immediately start every node and assume the network is ready. Bring the lab online in manageable groups:

1. Start or confirm the GNS3 VM/server.
2. Start the core and distribution switching nodes.
3. Start the access switches.
4. Start the routers and firewall appliances.
5. Start server nodes and other endpoints only when needed for the current exercise.
6. Start the Windows 11 endpoint VM separately in VMware Workstation when needed for endpoint or softphone testing.

Some appliances take longer to boot than others. Wait for each device to finish booting before opening its console or continuing troubleshooting.

**Project status:** Device configurations and end-to-end services are still being brought up. A node showing as started in GNS3 only confirms that the virtual device is running; it does not confirm that its interfaces, routing, firewall policies, or services are configured correctly.

## 7. Access device consoles

1. In GNS3, right-click a device.
2. Select **Console**.
3. Wait for the device prompt or boot process.
4. Identify the device before entering commands.
5. Use read-only discovery commands first.

For Cisco IOS devices, commonly useful commands include:

```text
enable
show version
show ip interface brief
show interfaces
show running-config
show ip route
```

For switches, where supported:

```text
show vlan brief
show interfaces trunk
show etherchannel summary
show spanning-tree
show cdp neighbors detail
```

Not every command is supported by every image. Record unsupported commands rather than assuming the device behaves like another Cisco model. ASA and FortiGate use their own CLI syntax; do not paste Cisco IOS commands into firewall consoles.

## 8. Windows endpoint and VOIP-LAB connection

The Windows endpoint is optional for general topology startup. It is used for endpoint testing and the planned softphone work.

The intended lab-side path is:

```text
Windows 11 VM
    |
VMware LAN Segment: VOIP-LAB
    |
GNS3 VM second adapter (intended eth1)
    |
GNS3 Cloud node
    |
SW-Voice
    |
Voice VLAN 30
    |
R-CME-01
```

When using the Windows endpoint:

1. Start the Windows VM in VMware Workstation.
2. Confirm its normal internet adapter remains separate from the lab adapter.
3. Confirm the second adapter is attached to the VMware LAN Segment named `VOIP-LAB`.
4. Confirm the GNS3 VM has its intended second adapter connected to that same LAN Segment.
5. Confirm the GNS3 Cloud node is bound to the correct GNS3 VM interface.
6. Check the Windows adapter status and IP settings before attempting connectivity tests.

This path still needs end-to-end verification. Do not bridge the lab into your home LAN or change the host's physical network adapter settings to make the lab work.

## 9. Normal session checklist

At the beginning of each session:

- [ ] Start VMware Workstation.
- [ ] Start or confirm the GNS3 VM/server is ready.
- [ ] Open the existing GNS3 project.
- [ ] Confirm the topology matches the current v1.3 design.
- [ ] Check for missing images or failed nodes.
- [ ] Start only the devices needed for the current task.
- [ ] Open the relevant consoles.
- [ ] Record the starting state before making configuration changes.

During the session:

- Change one thing at a time.
- Save configurations after a verified milestone.
- Record commands, results, and errors.
- Update the cut sheet when an approved address or interface assignment changes.
- Do not mark a feature verified until it has been tested.

## 10. Save and shut down safely

1. Save the GNS3 project.
2. Save device configurations using the platform's supported save command. On Cisco IOS, this is commonly `copy running-config startup-config`.
3. Capture relevant command output or screenshots as evidence.
4. Stop GNS3 nodes using the GNS3 controls. Avoid abruptly closing VMware while appliances are writing data.
5. Shut down the Windows endpoint VM from inside Windows if it was used.
6. Shut down the GNS3 VM through its supported shutdown method when finished.
7. Close GNS3 and VMware Workstation after the virtual machines have stopped.
8. Keep a backup of the project and known-good configurations.

Do not rely on saving the GNS3 project alone to save every device's running configuration. Save device configurations separately.

## 11. Common first-start problems

| Symptom | What to check first |
|---|---|
| GNS3 says it is not connected to the controller/server | Confirm the GNS3 VM is running and the server connection is configured correctly |
| A node cannot start | Check its appliance template, image path, virtualization support, and available host resources |
| Console window is blank | Wait for boot, reopen the console, and confirm the selected console type is supported |
| Link is red | Check whether both nodes are running, then inspect interface state and configuration |
| Device image is missing | Confirm the required image is installed and mapped to the correct appliance template |
| Windows VM has internet but cannot reach the lab | Check the separate `VOIP-LAB` adapter path; NAT internet access does not prove lab connectivity |
| Devices start but cannot communicate | Check interface state, VLANs, IP addresses, routes, and firewall policies |

## 12. Lab safety rules

- Keep the network lab isolated from your home network.
- Do not connect experimental WAN/DMZ links to a real home or public network.
- Do not run fault-injection exercises against physical adapters or external systems.
- Back up the project before major changes.
- Never upload passwords, private keys, tokens, or other secrets to GitHub.
- Treat planned, configured, tested, and verified as different statuses.

## 13. Where to go next

Once the project opens and the nodes start correctly, follow the [Build Instructions](BUILD-INSTRUCTIONS.md) to configure the network in stages. Use the [test plan](../05-testing/test-plan.md) to record results.

A successful first startup means the project opens and the required virtual nodes can start. It does **not** mean the network is fully configured or operational.

# Phone Network (VoIP)

## The goal

Connect softphones to a phone system so we can make calls between extensions. The planned phone network is VLAN 30, using `10.10.30.0/24). This plan still needs to be tested.

## What is set up so far

- Windows 11 VM named `VOIP-PHONE-01` is installed.
- Its first network adapter uses VMware NAT for internet access.
- Its second adapter is connected to a VMware LAN Segment named `VOIP-LAB`.
- GNS3 VM interface `eth1) is meant to connect to that same LAN Segment.
- GNS3 Cloud1 is set to use GNS3 VM interface `eth1`.
- Cisco 3745 is being checked as the possible CME phone server. Its IOS, storage, and phone compatibility still need to be checked.

## Important phone software note

A Cisco 7960/7940 phone firmware file does not turn a GNS3 router into a phone. Those files are meant for real phone hardware. For this lab, we need a softphone program that works with the phone system we choose.

Cisco IP Communicator is one possible Cisco softphone, but we still need to check whether we can get it, whether we can use it, whether it works on Windows 11, and whether it works with our CME version.

SIP and SCCP are two different ways phones talk to a phone system. A SIP phone will not automatically work with a setup that only supports SCCP.

## Planned phones

| Phone | Extension | Address plan | Status |
|---|---:|---|---|
| VOIP-PHONE-01 | 1001 | DHCP on the voice network | Windows installed; softphone not set up |
| VOIP-PHONE-02 | 1002 | DHCP on the voice network | Not created |
| VOIP-PHONE-03 | 1003 | DHCP on the voice network | Not created |

## To-do list

- [ ] Make sure VLAN 30 reaches the whole path.
- [ ] Test the Cloud1 connection.
- [ ] Confirm the voice gateway and DHCP server.
- [ ] Check CME and storage requirements.
- [ ] Choose a softphone that works with the phone system.
- [ ] Set up phone addresses and TFTP if needed.
- [ ] Create extensions.
- [ ] Test phone registration and two-way audio.
- [ ] Save screenshots and test results.

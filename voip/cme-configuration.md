# Cisco CME Phone Server Notes

> **Status: Still checking compatibility.** CME has not been configured. The planned router is a Cisco 3745 running IOS 12.4(25d), image `C3745-ADVENTERPRISEK9-M`. The router has reported that its flash storage is missing or unavailable.

## Planned settings

- Router name: R-CME-01
- Voice VLAN: 30
- Router address: 10.10.30.10/24
- Planned gateway: 10.10.30.1, if that is confirmed as the voice network's gateway

## Commands used to check the router

Run these commands and save the results:

```cisco
enable
show version
show ip interface brief
show running-config
show file systems
show flash:
show inventory
```

## Checks we must finish first

- Make sure this IOS version supports the CME version we want.
- Make sure the router has working storage and enough free space.
- Make sure the CME files are available to use.
- Make sure the softphone uses a phone protocol supported by this CME version.
- Confirm the router port, VLAN 30 gateway, and route to the rest of the lab.
- Decide which device will give IP addresses to phones. Only one device should manage the voice DHCP range.

Do not paste a full phone-server configuration until these checks are complete. The final setup may need the router name, login access, voice interface, routing, DHCP or DHCP relay, TFTP/Option 150, CME phone settings, extensions, and phone registration. The exact commands depend on the IOS version.

## How we will test it

Check that the router port is up, a phone gets the right IP address, the phone can reach CME, the phone registers, and calls work in both directions. Save a working copy before making changes. Never upload passwords or other secrets to GitHub.

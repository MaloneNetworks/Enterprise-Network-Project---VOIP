# Cisco CME Implementation Notes

> Status: compatibility validation pending. No CME configuration has been applied. The candidate is a Cisco 3745 running IOS 12.4(25d), image C3745-ADVENTERPRISEK9-M. Flash previously appeared unavailable/removed.

## Intended design
- Hostname: R-CME-01
- Voice VLAN: 30
- Candidate address: 10.10.30.10/24
- Proposed gateway: 10.10.30.1, only if confirmed as VLAN 30's gateway

## Preflight
Run and save:

```cisco
enable
show version
show ip interface brief
show running-config
show file systems
show flash:
show inventory
```

## Compatibility checklist
- Confirm IOS feature set and platform support for the intended CME release.
- Confirm flash/storage exists and has sufficient free space.
- Confirm the required CME files are legitimately available.
- Confirm the softphone protocol and firmware are compatible with the selected CME release.
- Confirm interface mapping, VLAN 30 gateway ownership, and routing.
- Confirm only one DHCP authority serves the voice subnet.

Do not paste a final configuration until these checks pass. The eventual configuration may include hostname, management access, voice-facing interface, routing, DHCP or relay, TFTP/Option 150 if required, CME call control, directory numbers, and endpoint registration. Use only commands supported by the actual IOS image.

## Validation
Verify interface up/up, endpoint DHCP, CME reachability, registration, and successful calls in both directions. Save known-good configuration before each change. Never commit passwords or authentication secrets.

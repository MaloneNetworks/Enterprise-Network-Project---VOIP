# Test Plan

Record actual commands, expected/observed results, timestamps, and evidence. A test is not passed until performed.

| ID | Area | Test | Expected result | Status | Evidence |
|---|---|---|---|---|---|
| T-001 | Layer 2 | Verify VLAN presence | Required VLANs exist on intended switches | Not run | |
| T-002 | Layer 2 | Verify trunks | Expected VLANs allowed and forwarding | Not run | |
| T-003 | Layer 3 | Verify gateway | Endpoint reaches configured gateway | Not run | |
| T-004 | Redundancy | Simulate core failure | Redundant gateway continues forwarding | Not run | |
| T-005 | Security | Test permitted traffic | Explicitly allowed flows succeed | Not run | |
| T-006 | Security | Test denied traffic | Prohibited flows are blocked | Not run | |
| T-007 | WAN | Verify branch path | Intended branch networks are reachable | Not run | |
| T-008 | VoIP | Obtain DHCP lease | Endpoint receives intended voice subnet address | Not run | |
| T-009 | VoIP | Obtain TFTP configuration | Endpoint retrieves supported configuration | Not run | |
| T-010 | VoIP | Register endpoint | Endpoint registers to call control | Not run | |
| T-011 | VoIP | Place extension call | Two endpoints establish a call | Not run | |
| T-012 | VoIP | Verify audio | Two-way audio works | Not run | |

## Test result template
- Test ID:
- Date/time:
- Device(s):
- Preconditions:
- Commands/actions:
- Expected:
- Actual:
- Result: PASS / FAIL / BLOCKED
- Evidence path:
- Notes/corrective action:

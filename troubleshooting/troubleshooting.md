# Troubleshooting Log

Record each incident using the template below. Keep only cases you personally reproduced and verified.

## Case 1 — VLAN 10 DHCP failure

- **Symptom:** VLAN 20 clients received DHCP addresses; VLAN 10 clients did not.
- **Commands/checks:** `show port-security interface fa0/3`, `show interfaces fa0/3`, `show port-security interface fa0/2`, `show interfaces fa0/2`, `show ip dhcp pool`, `show ip dhcp binding`, `show access-lists SALES_RESTRICTIONS`.
- **Findings:** SW1 Fa0/3 and SW2 Fa0/2 were `Secure-up`, interfaces were `up/up`, and security violation counts were zero. The DHCP pool existed. R1's inbound `SALES_RESTRICTIONS` ACL on G0/0.10 lacked a permit for initial DHCP client requests.
- **Root cause:** DHCP Discover packets initially use source `0.0.0.0` and UDP ports 68 -> 67, so they did not match the existing subnet-based ACL rules and could be dropped by the implicit deny.
- **Fix:** Added `permit udp any eq 68 any eq 67` to the named extended ACL.
- **Verification:** VLAN 10 clients subsequently received DHCP addresses.
- **Lesson:** Check ACLs on the gateway interface as well as DHCP pool and switch-port state.

## Case 2 — Wrong access VLAN

- **Symptom:**
- **Commands used:**
- **Root cause:**
- **Fix:**
- **Verification:**

## Case 3 — Trunk allowed-VLAN mismatch

- **Symptom:**
- **Commands used:**
- **Root cause:**
- **Fix:**
- **Verification:**

## Case 4 — OSPF network or area mismatch

- **Symptom:**
- **Commands used:**
- **Root cause:**
- **Fix:**
- **Verification:**

## Case 5 — Incorrect ACL direction or rule order

- **Symptom:**
- **Commands used:**
- **Root cause:**
- **Fix:**
- **Verification:**

## Case 6 — Incorrect IP address or subnet mask

- **Symptom:**
- **Commands used:**
- **Root cause:**
- **Fix:**
- **Verification:**

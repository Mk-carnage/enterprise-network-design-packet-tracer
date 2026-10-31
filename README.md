Enterprise Network Design & Implementation | Cisco Packet Tracer
A multi-site enterprise network lab built in Cisco Packet Tracer. The project covers HQ and branch connectivity, VLAN segmentation, inter-VLAN routing, dynamic IP addressing, OSPF routing, NAT/PAT, access control lists, secure device management, Layer 2 redundancy, and structured troubleshooting.
Project status: Completed lab implementation. Add your own topology screenshot, Packet Tracer file, and exported device configurations before publishing.

Project objectives
- Segment HQ and branch users into separate VLANs.
- Route between VLANs using router-on-a-stick.
- Assign client addresses dynamically with DHCP.
- Enable HQ-to-branch routing using OSPF.
- Simulate internet connectivity through an ISP router and NAT/PAT.
- Apply security controls using ACLs, SSH, port security, and switch-port hardening.
- Improve Layer 2 resilience using LACP EtherChannel and Spanning Tree Protocol.
- Diagnose common network faults and document the fixes.
Topology
Place your exported topology image at docs/topology.png, then replace or retain this line:

High-level design
- R1: HQ router; VLAN gateways, DHCP for HQ VLANs, OSPF, default route, and PAT toward the ISP.
- R2: Branch router; branch VLAN gateways, DHCP for branch VLANs, OSPF, and branch-side routing/NAT as implemented.
- R3: ISP simulation router, including the external test destination/loopback used for connectivity tests.
- SW1 and SW2: HQ access/distribution switching, VLAN trunks, and LACP EtherChannel.
- SW3: Branch access switching.
- Client VLANs: VLAN 10 (Sales), VLAN 20 (IT), VLAN 30, and VLAN 40 (Guest, according to the lab policy).
- VLAN 99: Additional HQ VLAN used in the switching/router configuration.
Update labels if your final Packet Tracer topology uses different names or roles.
Technologies and concepts
- Cisco Packet Tracer
- VLANs and 802.1Q trunking
- Router-on-a-stick inter-VLAN routing
- DHCP pools and excluded addresses
- OSPF, area 0
- Static/default routing
- NAT/PAT (overload)
- Extended ACLs and traffic filtering
- SSH and local authentication
- Port security with sticky MAC addresses
- Unused-port shutdown
- EtherChannel with LACP
- Spanning Tree Protocol, root bridge, PortFast, and BPDU Guard
- CLI-based verification and troubleshooting
Addressing plan
Fill in this table from your final saved configuration before publishing. The HQ/branch VLAN gateway addresses below reflect the lab values used during implementation; verify the remaining entries against your .pkt file.
Segment	Network	Gateway / interface
HQ VLAN 10	192.168.10.0/24	R1 192.168.10.1
HQ VLAN 20	192.168.20.0/24	R1 192.168.20.1
HQ VLAN 99	192.168.99.0/24	R1 192.168.99.1
Branch VLAN 30	192.168.30.0/24	R2 192.168.30.1
Branch VLAN 40	192.168.40.0/24	R2 192.168.40.1
R1–R2 transit	10.0.0.0/30	R1 10.0.0.2, R2 10.0.0.1
R1–ISP transit	203.0.113.0/30	R1 203.0.113.1; verify R3 address
External test destination	Verify final topology	Loopback/test IP on R3 (lab target included 8.8.8.8)


Note: 8.8.8.8 is commonly used as a public DNS address on real networks. In this lab, describe it as an emulated external test destination only if your Packet Tracer configuration assigns that address to R3. Do not imply the simulation provides real internet access.
Implementation phases
Day 1 — HQ foundation
- Built the HQ topology with R1, SW1, SW2, client devices, and a server.
- Created VLANs 10, 20, and 99.
- Configured access ports and 802.1Q trunks.
- Configured R1 router-on-a-stick subinterfaces.
- Tested inter-VLAN connectivity with static client addresses.
Day 2 — Branch and DHCP
- Added R2 and SW3 with branch VLANs 30 and 40.
- Connected R1 and R2 over 10.0.0.0/30.
- Configured DHCP pools for HQ and branch VLANs.
- Verified clients could receive addresses automatically.
Day 3 — OSPF and external connectivity
- Configured OSPF area 0 between R1 and R2.
- Added R3 to simulate the ISP.
- Configured a default route and OSPF default-route advertisement.
- Configured and tested NAT/PAT according to the final lab design.
Day 4 — Security
- Applied ACLs to enforce VLAN communication policies.
- Configured SSH and local authentication on network devices.
- Enabled port security on access ports.
- Shut down unused ports and added device hardening settings.
Day 5 — Redundancy
- Bundled parallel SW1–SW2 links using LACP EtherChannel.
- Configured SW1 as the STP root for VLANs 10, 20, and 99.
- Enabled PortFast and BPDU Guard on appropriate end-device ports.
- Tested connectivity during a link failure.
Day 6 — Break/fix troubleshooting
Practiced diagnosing faults such as:
- Incorrect access VLAN assignment
- Trunk allowed-VLAN mismatch
- OSPF network/area mismatch
- ACL direction or rule-order problems
- Incorrect IP address or subnet mask
Document each verified incident in troubleshooting/troubleshooting.md.
Day 7 — Documentation and publication
- Saved the .pkt project file.
- Exported the topology image.
- Saved final device configurations.
- Wrote this README and documented troubleshooting cases.
Security policy examples
The lab includes policy goals such as:
- VLAN 10 (Sales) must not initiate traffic to VLAN 20 (IT).
- VLAN 40 (Guest) may reach the simulated external network but must not reach internal subnets.
- Network-device administration should use SSH rather than Telnet.
- Access ports should limit learned MAC addresses and unused switch ports should be disabled.
Verify the final behavior in Packet Tracer before claiming each policy is enforced. A failed ping alone may not prove an entire ACL policy; use ACL counters and test both permitted and denied traffic.
Verification commands
Run commands on the relevant devices and record the successful output in your notes.
Switches
show vlan brief
show interfaces trunk
show interfaces status
show etherchannel summary
show spanning-tree
show port-security
show port-security interface fa0/3
Routers
show ip interface brief
show ip route
show ip ospf neighbor
show ip ospf database
show ip dhcp pool
show ip dhcp binding
show access-lists
show ip nat translations
show ip nat statistics
Client tests
- Confirm each client receives an address from the correct subnet.
- Ping its default gateway.
- Test allowed and restricted inter-VLAN traffic.
- Test HQ-to-branch connectivity.
- Test the simulated external destination.
- Disconnect one EtherChannel member and confirm connectivity remains through the surviving member.
Some commands vary by Packet Tracer device model and IOS feature support.
Troubleshooting case study: VLAN 10 DHCP failure
Symptom: VLAN 20 clients obtained DHCP addresses, but VLAN 10 clients did not.

Checks performed:
1. Checked VLAN 10 access ports on SW1 and SW2.
2. Confirmed show port-security interface reported Secure-up and zero security violations.
3. Confirmed interfaces were up/up.
4. Reviewed the DHCP pools on R1.
5. Inspected the inbound SALES_RESTRICTIONS ACL applied to R1 G0/0.10.
Root cause: The inbound ACL permitted ordinary traffic sourced from 192.168.10.0/24 but did not explicitly permit initial DHCP client requests. DHCP Discover packets initially use source address 0.0.0.0, so they did not match the existing rules and could be dropped by the implicit deny.

Fix applied:
R1(config)# ip access-list extended SALES_RESTRICTIONS
R1(config-ext-nacl)# permit udp any eq 68 any eq 67
Verification: VLAN 10 clients subsequently obtained DHCP addresses. The existing Sales-to-IT restriction was retained.
Repository structure
enterprise-network-project/
├── README.md
├── topology.pkt                 # Add your saved Packet Tracer file
├── configs/
│   ├── R1-running-config.txt
│   ├── R2-running-config.txt
│   ├── R3-running-config.txt
│   ├── SW1-running-config.txt
│   ├── SW2-running-config.txt
│   └── SW3-running-config.txt
├── docs/
│   └── topology.png
└── troubleshooting/
|   └── troubleshooting.md
├── Passwords/
│   └── Device_Password_Reference.docs
Only include files you have actually exported. Remove placeholder filenames for devices that are not in your final topology.
How to use
1. Install/open Cisco Packet Tracer.
2. Download or clone this repository.
3. Open topology.pkt.
4. Review the device configurations under configs/.
5. Follow the verification commands above to reproduce the tests.
Skills demonstrated
Network segmentation • Routing and switching • DHCP • OSPF • NAT/PAT • ACLs • Secure remote administration • Port security • EtherChannel • STP • Troubleshooting • Technical documentation
Author
Kailasanathan R.

LinkedIn : https://www.linkedin.com/in/kailasanathan-r/ .
This is an educational simulation project. IP addresses, security policies, and routing behavior should be checked against the included final Packet Tracer file and device configurations.

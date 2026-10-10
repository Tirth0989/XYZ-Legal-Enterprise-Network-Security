# XYZ Legal Enterprise Network Security

A Cisco Packet Tracer project for the COMP702 Enterprise Networking and Security case study. The scenario connects the Wellington head office of XYZ Legal Solutions to its Auckland branch and addresses security weaknesses in the head office LAN.

## Open the simulation

[Download the Packet Tracer project](simulation/COMP702_XYZ_Legal_Final.pkt)

1. Install Cisco Packet Tracer on your computer.
2. Download the `.pkt` file from the link above.
3. Open the file in Packet Tracer.
4. Inspect the topology, interface addressing, and saved device configurations.
5. Use the verification checklist below to test connectivity, routing, and security features.

The file is a Packet Tracer simulation and does not configure a physical network.

## Case study objectives

The supplied case study specifies two office routers connected by a simulated serial WAN. The head office design requires at least three switches: one distribution switch and two access switches.

The project scope includes:

- Head office switching, inter-VLAN routing, and DHCP.
- A WAN link between the Wellington and Auckland offices.
- Single-area OSPF, at least two branch loopback networks, and MD5 authentication between OSPF neighbours.
- Router and switch configuration to mitigate VLAN manipulation, STP manipulation, unauthorised device access, rogue DHCP, and ARP poisoning.
- An IPsec tunnel to protect traffic between the offices.
- Troubleshooting records and verification evidence.

These are the assignment requirements. They are not an independent confirmation that every feature is configured or operational in the attached simulation.

## Security review guide

| Threat in the case study | Configuration to inspect | Expected security purpose |
| --- | --- | --- |
| Unauthorised VLAN manipulation | VTP mode, explicit trunk/access modes, trunk VLAN permissions, and DTP settings where supported | Limit unauthorised VLAN changes and unexpected trunk negotiation |
| STP manipulation | PortFast and BPDU Guard on end-device ports; Root Guard where appropriate | Prevent an unauthorised switch from influencing the spanning-tree topology |
| Unauthorised device access | Port security and shutdown of unused ports | Restrict device attachment to access ports |
| Rogue DHCP and traffic interception | DHCP snooping, enabled VLANs, and correctly trusted DHCP paths | Reject DHCP server replies received on untrusted ports |
| ARP poisoning | Dynamic ARP Inspection, trusted interfaces, and valid binding information where supported | Reject forged ARP messages |
| Unauthorised routing updates | OSPF MD5 authentication and matching neighbour settings | Require matching authentication for OSPF adjacency |
| WAN traffic exposure | Matching IPsec policies, peers, traffic selectors, and crypto-map assignments | Authenticate peers and protect selected interoffice traffic |

The controls above are review targets. Confirm the actual configuration in the saved simulation. Port security restricts attachment; it does not scan for malware or prevent all infections.

## Verification checklist

Run commands on the appropriate devices and record the results. Some commands depend on the simulated device model and Packet Tracer support.

| Area | Suggested checks | Evidence to collect |
| --- | --- | --- |
| Interfaces and WAN | `show ip interface brief`; inspect serial clocking and encapsulation | Addressed interfaces and the WAN link are up |
| VLANs and trunks | `show vlan brief`; `show interfaces trunk` | Expected VLAN membership and trunk permissions |
| DHCP | `show ip dhcp binding` on the DHCP router; inspect client addressing | Clients receive the intended address, gateway, and DNS settings |
| OSPF | `show ip ospf neighbor`; `show ip route`; inspect OSPF configuration | Established adjacency and learned remote routes |
| OSPF authentication | Inspect authentication settings on both WAN interfaces | Matching authentication type, key ID, and key settings without publishing secret values |
| STP protection | `show spanning-tree`; inspect access-port configuration | Intended root selection and edge-port protections |
| Port security | `show port-security`; inspect selected access interfaces | Limits, learned addresses, and intended violation action |
| DHCP snooping | `show ip dhcp snooping`; `show ip dhcp snooping binding` | Enabled VLANs, correct trust boundaries, and bindings |
| ARP inspection | `show ip arp inspection`, where supported | Inspection configuration consistent with legitimate host bindings |
| IPsec | Generate matching interoffice traffic; run `show crypto isakmp sa` and `show crypto ipsec sa` | Established security associations and increasing encryption/decryption counters |
| End-to-end reachability | Ping and trace between intended local and remote hosts | Successful communication over the expected path |

A successful ping alone does not establish that the traffic was encrypted. Inspect IPsec counters after generating traffic that matches the configured selectors.

## Troubleshooting documentation

For each issue, record the observed symptom, root cause, configuration change, and verification result. The assignment calls for five troubleshooting cases. No completed troubleshooting journal or test screenshots were supplied with this upload, so none are presented here as completed evidence.

## Repository contents

```text
XYZ-Legal-Enterprise-Network-Security/
├── README.md
└── simulation/
    └── COMP702_XYZ_Legal_Final.pkt
```

The blank case study document and assessment outline are excluded. This README provides project context and a verification guide instead of republishing the assignment templates.

## Validation status

The uploaded Packet Tracer file is included as supplied. It has not been opened or executed in Packet Tracer during repository preparation. Device counts, addresses, protocol settings, tunnel operation, and security behaviour must be confirmed in the simulator.

## Technical topics

Cisco Packet Tracer, enterprise LAN/WAN design, VLANs, inter-VLAN routing, DHCP, serial WAN connectivity, OSPF authentication, switch hardening, DHCP snooping, Dynamic ARP Inspection, IPsec, and network troubleshooting.

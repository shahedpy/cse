# Networking

Comprehensive networking course materials organized by topic, following the course syllabus.

## Table of Contents

### 1. [IP Addressing & Address Management](addressing/README.md)
- [Classless Addressing (CIDR)](addressing/classless-addressing.md)
- [Network Address Translation (NAT)](addressing/nat.md)
- [IANA & Regional Internet Registries](addressing/iana-rir.md)
- [ISP Roles](addressing/isp-roles.md)
- [IPv4 Address Anatomy](addressing/ipv4-anatomy.md)
- [Subnet Mask](addressing/subnet-mask.md)
- [Subnetting Basics](addressing/subnetting-basics.md)
- [Variable Length Subnet Masking (VLSM)](addressing/vlsm.md)

### 2. [Network Security](security/README.md)
- [Asymmetric Key Cryptography](security/asymmetric-crypto.md)
- [Public Key Cryptography (RSA)](security/rsa.md)
- [RSA Practice Problems](security/rsa-problems.md)

### 3. [Routing Protocols](routing/README.md)
- [Routing Concepts](routing/concepts.md)
- [Distance Vector Routing / RIP](routing/rip.md)
- [Link-State Routing / OSPF](routing/ospf.md)
- [Path-Vector Routing / BGP](routing/bgp.md)
- [Hybrid Protocols / EIGRP](routing/eigrp.md)
- [Routing Commands & CLI](routing/commands.md)

### 4. [Network Protocols](protocols/README.md)
- [Address Resolution Protocol (ARP)](protocols/arp.md)
- [Reverse ARP (RARP)](protocols/rarp.md)
- [Dynamic Host Configuration Protocol (DHCP)](protocols/dhcp.md)
- [RTS/CTS Protocol](protocols/rts-cts.md)

### 5. [Wireless Networking](wireless/README.md)
- [Wireless Basics](wireless/basics.md)
- [RTS/CTS Protocols](wireless/rts-cts.md)
- [Wi-Fi Architecture](wireless/wifi.md)
- [WiMAX Architecture](wireless/wimax.md)
- [Mobile Networks](wireless/mobile-networks.md)

### 6. [Course Materials (PDFs & Slides)](docs/pdfs/index.md)

---

---

## Quick Reference

### IP Addressing Fundamentals

→ **See [IP Addressing](addressing/README.md) for comprehensive coverage**

---

## Study by Topic

Follow the syllabus order for structured learning:

1. **Start with [Addressing](addressing/README.md)** — understand IP structure, CIDR, NAT, subnetting
2. **Then [Security](security/README.md)** — learn cryptography fundamentals
3. **Move to [Routing](routing/README.md)** — understand how packets find paths
4. **Study [Protocols](protocols/README.md)** — ARP, DHCP, and address resolution
5. **Finish with [Wireless](wireless/README.md)** — Wi-Fi, WiMAX, mobile networks

---

## Legacy Content (For Reference)

The sections below provide quick reference material. For comprehensive study, use the organized folders above.

### IPv4 Quick Reference

An IPv4 address is a 32-bit number that identifies a network interface (for example, a computer or a router).

- Connectionless protocol (best-effort delivery).
- Supports packet fragmentation when necessary.
- Uses 32-bit Internet addresses.
- IP does not provide end-to-end reliability or flow control; higher-layer protocols such as TCP provide those features.

## Address types

- **Public address:** Assigned by an ISP; globally routable and unique.
- **Private address:** Used within private networks (RFC 1918); not routable on the public Internet.

## IPv6

- Uses 128-bit addresses (vastly larger address space).
- Simplified fixed-size header improves routing performance.
- Provides better support for authentication, privacy, and quality of service.
- IPv6 is not directly compatible with IPv4; transition mechanisms are used during migration.

## IP Address Structure

Each IP address typically consists of two logical parts:

- **Network portion:** identifies the network (used by routers for forwarding).
- **Host portion:** identifies the host/interface within that network.

IPv4 addresses are commonly written as four decimal octets (0–255), e.g. `192.0.2.1`.

## ARP — Address Resolution Protocol

ARP (Address Resolution Protocol) is a network protocol used to determine the MAC address (hardware address) corresponding to an IP address. When one device in a LAN (Local Area Network) wants to communicate with another, it must know the destination’s MAC address. Since users and applications work with IP addresses, ARP acts as the translator, converting IP addresses into MAC addresses.

Note: ARP operates at the Network Layer (Layer 3) but interacts closely with the Data Link Layer (Layer 2).

### Important ARP Terms
- **ARP Cache:** A table where resolved MAC addresses are stored for quick future use.
- **ARP Cache Timeout:** The duration for which an entry remains valid in the ARP cache before it expires and may be refreshed.
- **ARP Request:** A broadcast message asking, "Who has this IP address?" so the requester can learn the destination MAC.
- **ARP Reply/Response:** A unicast message containing the MAC address of the requested IP, sent back to the original requester.

### Types of ARP
1. **Proxy ARP** — A proxy device (usually a router) replies to ARP requests on behalf of another host. This can be used to hide network topology or help connect different subnets.
2. **Gratuitous ARP** — A host broadcasts an ARP request (or unsolicited ARP reply) for its own IP. It is commonly used to detect duplicate IPs and to refresh other hosts' ARP caches.
3. **Reverse ARP (RARP)** — Historically used by devices that only know their MAC address to discover their IP address (for example, diskless machines at boot). Mostly replaced by DHCP.
4. **Inverse ARP (InARP)** — Opposite of standard ARP: used by a device with a known Layer 2 address (MAC) to discover the corresponding IP address; commonly used in older technologies like Frame Relay and ATM.

### How ARP works (basic)
The following steps are involved:
1. **Sender checks ARP Cache:** If the MAC address for the destination IP is already cached, communication starts immediately.
2. **ARP Request Broadcast:** If not cached, the sender broadcasts an ARP request on the LAN: "Who has <IP>? Tell <sender IP>."
3. **All Devices Receive Request:** Every device on the local segment receives the request and checks whether the requested IP matches its own.
4. **Destination Replies:** The device whose IP matches sends an ARP reply (unicast) containing its MAC address.
5. **Cache Update:** The sender updates its ARP cache with the new IP → MAC mapping for future use.

### ARP cache / ARP table
- Hosts maintain an ARP cache (table) with IP-to-MAC mappings to avoid repeating requests for every packet. Entries have a timeout and may be refreshed on demand.
- You can view the ARP table on many systems (e.g., `arp -a` on macOS/Linux/Windows) and flush it with system-dependent commands.

### Variants and related protocols
- **Gratuitous ARP** — a host broadcasts an ARP notification for its own IP (used for duplicate IP detection or to update other hosts' caches).
- **Proxy ARP** — a router or device answers ARP requests on behalf of another host (useful for certain bridging or NAT scenarios).
- **Reverse ARP (RARP)** — historical protocol used by diskless clients to discover their IP from a MAC (largely obsolete; replaced by DHCP).

### Security and issues
- ARP is unauthenticated, which makes it vulnerable to ARP spoofing/poisoning attacks where an attacker sends fake ARP replies to intercept or disrupt traffic.
- Mitigations include using static ARP entries (where feasible), DHCP + dynamic security features, or network switch protections like Dynamic ARP Inspection (DAI) on managed switches.

### Common commands
- macOS/Linux: `arp -a` — list ARP table, `ip neigh` (Linux) — show neighbor table, `sudo ip -s -s neigh flush all` — clear the neighbor table.
- Windows: `arp -a` — list ARP table, `arp -d <ip>` — delete entry, `arp -v`/`Get-NetNeighbor` (PowerShell) on modern systems.

### Summary
ARP is a fundamental local network protocol that maps IP addresses to MAC addresses to allow Ethernet frames to reach the correct host on a LAN. Because it sits at the boundary between Layer 2 and Layer 3, it is widely used in IP-over-Ethernet networks for local delivery of packets.

### ARP Message Format 🔧

An ARP message consists of several fields:

- **Hardware Type (2 bytes):** Defines hardware (Ethernet = 1).
- **Protocol Type (2 bytes):** Defines protocol (IPv4 = 0x0800).
- **Hardware Address Length (1 byte):** Length of MAC address (6 for Ethernet).
- **Protocol Address Length (1 byte):** Length of IP address (4 for IPv4).
- **Operation Code (2 bytes):** 1 for request, 2 for reply.
- **Sender Hardware Address:** MAC of the sender.
- **Sender Protocol Address:** IP of the sender.
- **Target Hardware Address:** Empty in request; receiver’s MAC in reply.
- **Target Protocol Address:** Receiver’s IP.

### Advantages of the ARP Protocol ✅

- **Automatic Mapping:** No need for manual configuration to resolve MAC addresses.
- **Efficiency:** Ensures smooth communication within LANs by allowing devices to dynamically discover MAC addresses.
- **Transparency:** Works in the background without user intervention.
- **Flexibility:** Supports different types (Proxy, Gratuitous, Reverse, Inverse) for varied networking needs.

### RARP — Reverse Address Resolution Protocol 🔄

Reverse Address Resolution Protocol (RARP) is a network protocol that allows a device to discover its IP address when only its MAC (Media Access Control) address is known. Typical uses and components include:

- **IP Address Assignment:** Normally, a machine stores its IP address in a configuration file. Diskless systems cannot do this and rely on RARP or other mechanisms (historically RARP was used) for IP assignment.
- **Physical Address:** Every network device has a unique MAC address stored in its Network Interface Card (NIC).
- **RARP Request:** A device broadcasts a request containing its MAC address to ask for the corresponding IP address.
- **RARP Server:** The server maintains a mapping of MAC addresses to IP addresses and, on receiving a request, replies with the appropriate IP address.

Note: RARP has largely been superseded by DHCP (Dynamic Host Configuration Protocol), which provides more features (e.g., default gateway, DNS), but the historical role of RARP in diskless boot scenarios is still useful to understand.

### How it works
When a machine doesn't have the memory to store its IP address, such as diskless machines or newly configured systems, it uses RARP to request an IP address.

- **RARP Request:** A client broadcasts a RARP request containing its MAC address.
- **Server Lookup:** A RARP server (or gateway/router with an ARP/RARP table) checks its mapping of MAC -> IP.
- **RARP Reply:** If a match is found, the server responds with the client’s IP address.
- **Client Configuration:** The client configures itself with the provided IP and can now communicate on the network.

### RARP Packet Format & Encapsulation 🔧
RARP uses the same packet format as ARP (same fields and lengths) but uses a distinct EtherType to distinguish RARP frames. In Ethernet the RARP EtherType is `0x8035` (ARP uses `0x0806`). The ARP/RARP message contains fields such as hardware type, protocol type, hardware address length, protocol address length, operation code (indicating ARP vs RARP and request vs reply), sender hardware address, sender protocol address, target hardware address, and target protocol address. RARP requests typically include the client's MAC address and a zero or placeholder IP, and a server fills in the appropriate IP on reply.
## Dynamic Host Configuration Protocol (DHCP)

Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automate the process of assigning IP addresses and other network configuration parameters to devices such as computers, smartphones and printers. Instead of manually configuring each device, DHCP enables devices to join a network and automatically receive:

- **IP Address**
- **Subnet Mask**
- **Default Gateway**
- **DNS Server addresses**
- **Other TCP/IP configuration options**

### How DHCP works (DORA)
DHCP commonly follows a four-step process often called DORA:

1. **Discover:** A client broadcasts a DHCPDISCOVER message to locate available DHCP servers.
2. **Offer:** A DHCP server responds with a DHCPOFFER listing an available IP and other network settings.
3. **Request:** The client broadcasts a DHCPREQUEST to accept an offer from a server (or to renew/confirm a lease).
4. **Acknowledge:** The DHCP server sends a DHCPACK to confirm the assignment and lease parameters.

DHCP replaced RARP for most cases because it provides richer configuration capabilities (gateway, DNS, lease time, options) beyond just assigning an IP address.

### Components of DHCP

- **DHCP Server:** Stores IP addresses and configuration details. Allocates addresses dynamically or can provide static reservations for clients.
- **DHCP Relay (Agent):** Forwards DHCP messages between clients and servers when they are not on the same subnet (often implemented as `ip helper` or DHCP relay on routers).
- **DHCP Client:** Any device (PC, phone, printer, IoT device, etc.) requesting an IP address and configuration from a DHCP server.
- **IP Address Pool (Scope):** A predefined range of IP addresses the server can lease to clients. Administrators often configure excluded addresses for network devices.
- **Subnets/Scopes:** DHCP servers commonly maintain separate pools (scopes) per subnet so clients get addresses appropriate to their network.
- **Lease:** The duration the IP is assigned to the client. During the lease lifetime clients must renew; otherwise the address returns to the pool on expiry.
- **DNS Servers:** DHCP can provide DNS server address(es) to clients so they can resolve domain names.
- **Default Gateway (Router):** DHCP provides the router IP (default gateway) so clients can communicate outside their local subnet.
- **Options:** Additional DHCP options (e.g., subnet mask, domain name, NTP servers, WINS) which extend the configuration the server provides.

### DHCP messages & lifecycle

DHCP operates on the Application Layer and uses UDP ports 67 (server) and 68 (client). It follows a client-server model and often begins with the DORA exchange, but DHCP defines several message types and extensions that cover the full lease lifecycle and other behaviors:

1. **DHCPDISCOVER (Discover):**
	- Sent by a client to the broadcast address 255.255.255.255 (source IP 0.0.0.0) to discover DHCP servers on the local network.
	- May include requests for options like subnet mask, domain name, DNS, etc.

2. **DHCPOFFER (Offer):**
	- A server replies with an offer of an IP address and configuration parameters.
	- If multiple servers respond, the client generally accepts the first offer it receives; servers include a server identifier so they can be distinguished.

3. **DHCPREQUEST (Request):**
	- The client responds with a DHCPREQUEST to accept an offer and indicate the selected server.
	- This message may also be used for lease renewals; when renewing, the client unicasts to the known DHCP server (ports may be server 67), and the server can reply directly.
	- After a DHCPREQUEST is broadcast, other DHCP servers that had offered an IP will return the offered addresses to their pool.

4. **DHCPACK (Acknowledge):**
	- The server acknowledges the lease and supplies final lease parameters. The client may now use the IP and provided settings until the next renewal or expiry.

5. **DHCPREQUEST / DHCPACK (Renewal & Rebinding):**
	- When a lease reaches 50% of its duration, the client attempts a renewal by sending DHCPREQUEST directly to the leasing server. If the lease owner responds with DHCPACK the lease is renewed.
	- If the server does not respond, the client may try broadcast renewal (rebinding) near expiry; if no server responds before expiry, the client must restart the DORA process.

6. **DHCPRELEASE (Release):**
	- The client may voluntarily end the lease early by sending a DHCPRELEASE; the server then returns the address to the available pool.

Other messages and notes:
- **DHCPNAK:** Sent by the server to indicate the requested lease or renewal is denied (e.g., the address is no longer valid), prompting the client to restart discovery.
- **DHCPINFORM:** A client already has an IP (e.g., statically assigned) and requests additional configuration parameters from a DHCP server.
- **DHCP Options:** DHCP uses options to communicate extra information (e.g., option 1: subnet mask, option 3: router/default gateway, option 6: DNS servers, option 51: lease time, option 54: server identifier).
- **DHCP Relay Behavior:** When clients and servers are on different networks, routers are configured to forward broadcasts (DHCPDISCOVER) to DHCP servers as unicast to a server; replies are forwarded to clients accordingly.

Keep in mind DHCP may also be integrated with DNS dynamic updates, address reservations (static mappings by MAC), and access control mechanisms in enterprise environments.


## Classes of IP addresses (historical)

> Note: Classful addressing is largely obsolete, retained here for historical context.

- **Class A:** 1.0.0.0 — 127.255.255.255 (default mask: `255.0.0.0`, `/8`).
- **Class B:** 128.0.0.0 — 191.255.255.255 (default mask: `255.255.0.0`, `/16`).
- **Class C:** 192.0.0.0 — 223.255.255.255 (default mask: `255.255.255.0`, `/24`).
- **Class D:** 224.0.0.0 — 239.255.255.255 (multicast).
- **Class E:** 240.0.0.0 — 255.255.255.255 (reserved).

Classful layout by octet:

| Class | Byte 1 | Byte 2 | Byte 3 | Byte 4 |
|-------|--------|--------|--------|--------|
| A     | Net ID | Host   | Host   | Host   |
| B     | Net ID | Net ID | Host   | Host   |
| C     | Net ID | Net ID | Net ID | Host   |
| D     | Multicast (address group)               |
| E     | Reserved                                |

## Strategies to Conserve Addresses

To reduce pressure on the IPv4 address space, several strategies are used:

- **Private addressing (RFC 1918)** — use private ranges inside organizations and map to public addresses at network edges.
- **CIDR (Classless Inter-Domain Routing)** — allocate and route blocks by arbitrary prefix lengths instead of fixed classes.

### Private addressing (RFC 1918)

Private address ranges designated by RFC 1918:

- `10.0.0.0/8` (10.0.0.0 — 10.255.255.255)
- `172.16.0.0/12` (172.16.0.0 — 172.31.255.255)
- `192.168.0.0/16` (192.168.0.0 — 192.168.255.255)

Summary table:

| Address Block | Classful Equivalent | Prefix Length | Number of Addresses |
|---------------:|--------------------:|:-------------:|--------------------:|
| `10.0.0.0/8`    | 1 Class A           | `/8`          | 16,777,216          |
| `172.16.0.0/12` | 16 Class B          | `/12`         | 1,048,576           |
| `192.168.0.0/16`| 1 Class B           | `/16`         | 65,536              |

### Address translation: NAT and PAT

- **Network Address Translation (NAT):** maps private addresses to public addresses using a pool of public IPs. Basic NAT mappings can be 1:1 (private:public).
- **Port Address Translation (PAT) / NAT overload:** maps many private addresses to a single public IP using distinct source ports; this conserves public IPs and is the common form of NAT used in home routers.

## Classless Inter-Domain Routing (CIDR)

CIDR represents addresses as `A.B.C.D/N` where `/N` is the prefix length (number of network bits). For example, `192.9.205.22/18` means the first 18 bits identify the network and the remaining 14 bits identify hosts.

CIDR allows flexible block sizes (e.g., `/28`, `/27`, `/24`) and is used extensively by ISPs to allocate address space.

Subnet mask and CIDR examples (common Class C-style subnets):

| Binary       | Decimal | CIDR |
|--------------|--------:|:----:|
| `10000000`   | 128     | `/25`|
| `11000000`   | 192     | `/26`|
| `11100000`   | 224     | `/27`|
| `11110000`   | 240     | `/28`|
| `11111000`   | 248     | `/29`|
| `11111100`   | 252     | `/30`|

## Subnetting (Basic terminology & VLSM)

Subnetting divides an IP address block into smaller blocks. This is commonly done to isolate networks, conserve addresses, and match subnet sizes to host requirements.

### Basic terminology

- **Network ID** — the first address in the subnet (all host bits are 0). Not assignable to hosts in most cases.
- **Broadcast address** — the last address in the subnet (all host bits are 1). Used to send to all hosts in that subnet.
- **Host ID** — bits in the address reserved to identify hosts within a subnet.
- **Prefix length** (`/N`) — the number of bits of the address that belong to the network portion; subnet mask is the 32-bit mask with N leading ones.
- **Subnet mask** — a dotted decimal form of the prefix (`255.255.255.0` for `/24`).
- **Usable hosts** — the number of assignable addresses: normally `2^(host bits) - 2` (subtract 2 for network and broadcast), except in special cases like `/31` and `/32`.

### Steps to subnet a network

1. Determine the number of hosts (or required subnets) and the size of each subnet.
2. For each required subnet that needs H hosts, find the smallest k such that `2^k - 2 >= H` (k = number of host bits). The prefix becomes `/(32 - k)`.
3. Assign subnets by incrementing the network address by the size of the allocated block (2^k addresses).
4. For VLSM (variable-length subnet masks), sort requirements from largest to smallest and allocate the largest subnets first to avoid fragmentation.

### Example — Splitting a `/24` into 4 equal subnets

Start: `192.168.1.0/24` (256 addresses).

- Required: 4 equal subnets -> need 2 extra prefix bits (2^2 = 4), new prefix `/26` (64 addresses each).

The four `/26` subnets:

| Subnet | Address range | Usable hosts | Broadcast |
|--------|---------------:|-------------:|----------:|
| `192.168.1.0/26`   | .0 - .63   | .1 - .62 (62) | .63 |
| `192.168.1.64/26`  | .64 - .127 | .65 - .126 (62) | .127 |
| `192.168.1.128/26` | .128 - .191| .129 - .190 (62) | .191 |
| `192.168.1.192/26` | .192 - .255| .193 - .254 (62) | .255 |

### Example — VLSM (subnetting a subnet)

Given a network `192.168.1.0/24`, allocate subnets for three groups requiring: 50, 20, and 10 hosts.

Plan:
1. Sort largest to smallest: 50, 20, 10.
2. For 50 hosts, find smallest k: `2^6 - 2 = 62` -> `/26` (64 addresses).
3. For 20 hosts, `2^5 - 2 = 30` -> `/27` (32 addresses).
4. For 10 hosts, `2^4 - 2 = 14` -> `/28` (16 addresses).

Allocate from the start of the block:

- `192.168.1.0/26` (addresses .0 - .63) — usable .1 - .62 (62 hosts) — satisfies 50-host subnet.
- Next available: `192.168.1.64` → allocate `192.168.1.64/27` (addresses .64 - .95) — usable .65 - .94 (30 hosts) — satisfies 20-host subnet.
- Next available: `192.168.1.96` → allocate `192.168.1.96/28` (addresses .96 - .111) — usable .97 - .110 (14 hosts) — satisfies 10-host subnet.

The remaining address space (`192.168.1.112/28` and further) may be used for additional subnets.

### Important notes

- When allocating subnets be careful to not overlap ranges; VLSM avoids wasted addresses by using different prefix lengths per subnet.
- Very small networks sometimes use `/31` for point-to-point links (RFC 3021) and `/32` for single-host addresses.

### Practice problems

1. You have `10.0.0.0/24`. Create subnets to support 3 small offices: 60 hosts, 12 hosts, and 6 hosts. Show the subnets and usable host ranges.
2. Convert the subnet mask `255.255.255.224` to prefix length and state how many usable hosts it provides.

Answers:
1. 60 -> `/26` (64 addresses), 12 -> `/28` (16 addresses), 6 -> `/29` (8 addresses). Allocate in descending order starting at `10.0.0.0`.
	- `10.0.0.0/26` (usable: .1 - .62), `10.0.0.64/28` (usable .65 - .78), `10.0.0.80/29` (usable .81 - .86).
2. `255.255.255.224` is `/27` and gives `2^(32-27) - 2 = 30` usable hosts.
## Internet number governance (IANA & RIRs)

The Internet Assigned Numbers Authority (IANA) manages global coordination for the assignment of IP address blocks, autonomous system (AS) numbers, and other protocol parameters.

- IANA allocates large blocks of addresses and ASNs to Regional Internet Registries (RIRs) such as ARIN, RIPE NCC, APNIC, AFRINIC, and LACNIC.
- RIRs allocate smaller blocks to Internet Service Providers (ISPs) and sometimes directly to large organizations.
- This hierarchical model ensures global uniqueness and coordinated routing of Internet address space.

See: https://www.iana.org and the RIRs' websites for regional policies and allocations.

## ISP roles

Internet Service Providers (ISPs) play several important roles in the IP addressing ecosystem and in general Internet connectivity:

- Allocation and assignment — ISPs receive address blocks from RIRs and assign public addresses to customers (either dynamically via DHCP or as static assignments).
- Routing and peering — ISPs announce IP prefixes via routing protocols (e.g., BGP) and establish peering or transit agreements to exchange traffic.
- NAT and address conservation — Many ISPs use NAT/PAT at customer premises or within their networks to conserve public address space.
- Core services — ISPs often provide DNS resolvers, DHCP servers, and other gateway services for customers, and help with IPv6 migration.

These roles make ISPs a critical point of contact for both address allocation and operational support on the public Internet.

## Routing Protocols

This README includes a short summary of routing concepts, but for more detail please see `routing/README.md`.
The routing folder contains dedicated pages for DVR/RIP, Link-State/OSPF, Path-Vector/BGP, Hybrid protocols (EIGRP), concepts, and a CLI commands cheatsheet — and the course PDFs are listed in `docs/pdfs/index.md`.



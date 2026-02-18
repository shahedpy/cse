# Networking

An overview of the Internet Protocol (IP), addressing, and common strategies for conserving IPv4 address space.

## Table of contents

- [Internet Protocol (IP)](#internet-protocol-ip)
- [IPv4 Basics](#ipv4-basics)
- [Address Types](#address-types)
- [IPv6](#ipv6)
- [IP Address Structure](#ip-address-structure)
- [Classes of IP Addresses](#classes-of-ip-addresses)
- [Strategies to Conserve Addresses](#strategies-to-conserve-addresses)
- [Internet number governance (IANA & RIRs)](#internet-number-governance-iana--rirs)
- [ISP roles](#isp-roles)
- [Routing Protocols](routing/README.md)
- [Classless Inter-Domain Routing (CIDR)](#classless-inter-domain-routing-cidr)
- [Subnetting (Basic terminology & VLSM)](#subnetting-basic-terminology--vlsm)
- [ARP — Address Resolution Protocol](#arp---address-resolution-protocol)
- [Dynamic Host Configuration Protocol (DHCP)](#dynamic-host-configuration-protocol-dhcp)
- [Course materials (slides & PDFs)](docs/pdfs/index.md)

## Internet Protocol (IP)

The Internet Protocol is the cornerstone of the TCP/IP architecture. It is a connectionless, best-effort protocol used to deliver packets between hosts on different networks.

### Main tasks of IP

- Addressing — assigning unique addresses to hosts.
- Fragmentation — splitting packets when necessary to traverse smaller MTUs.

### IP versions

- **IPv4** — the widely deployed IP version (32-bit addresses).
- **IPv6** — the successor to IPv4 (128-bit addresses) with improvements in address space and header design.

## IPv4 basics

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

## Classes of IP addresses (historical)

> Note: Classful addressing is largely obsolete, retained here for historical context.

- **Class A:** 1.0.0.0 — 127.255.255.255 (default mask: `255.0.0.0`, `/8`).
- **Class B:** 128.0.0.0 — 191.255.255.255 (default mask: `255.255.0.0`, `/16`).
- **Class C:** 192.0.0.0 — 223.255.255.255 (default mask: `255.255.255.0`, `/24`).
- **Class D:** 224.0.0.0 — 239.255.255.255 (multicast).
- **Class E:** 240.0.0.0 — 255.255.255.255 (reserved).

## Strategies to Conserve Addresses

To reduce pressure on the IPv4 address space, several strategies are used:

- **Private addressing (RFC 1918)** — use private ranges inside organizations and map to public addresses at network edges.
- **CIDR (Classless Inter-Domain Routing)** — allocate and route blocks by arbitrary prefix lengths instead of fixed classes.

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

Routing protocols are covered in the `routing/` folder. For detailed notes and summaries on routing protocols, see `routing/README.md` and the protocol pages under `routing/`.

## Classless Inter-Domain Routing (CIDR)

CIDR represents addresses as `A.B.C.D/N` where `/N` is the prefix length (number of network bits). For example, `192.9.205.22/18` means the first 18 bits identify the network and the remaining 14 bits identify hosts.

CIDR allows flexible block sizes (e.g., `/28`, `/27`, `/24`) and is used extensively by ISPs to allocate address space.

## Subnetting (Basic terminology & VLSM)

Subnetting divides an IP address block into smaller blocks. This is commonly done to isolate networks, conserve addresses, and match subnet sizes to host requirements.

- **Network ID** — the first address in the subnet (all host bits are 0). Not assignable to hosts in most cases.
- **Broadcast address** — the last address in the subnet (all host bits are 1). Used to send to all hosts in that subnet.
- **Host ID** — bits in the address reserved to identify hosts within a subnet.
- **Prefix length** (`/N`) — the number of bits of the address that belong to the network portion; subnet mask is the 32-bit mask with N leading ones.
- **Subnet mask** — a dotted decimal form of the prefix (`255.255.255.0` for `/24`).
- **Usable hosts** — the number of assignable addresses: normally `2^(host bits) - 2` (subtract 2 for network and broadcast), except in special cases like `/31` and `/32`.

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

## Dynamic Host Configuration Protocol (DHCP)

Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automate the process of assigning IP addresses and other network configuration parameters to devices such as computers, smartphones and printers. Instead of manually configuring each device, DHCP enables devices to join a network and automatically receive IP address, subnet mask, default gateway, and DNS server addresses.

### How DHCP works (DORA)

1. **Discover:** A client broadcasts a DHCPDISCOVER message to locate available DHCP servers.
2. **Offer:** A DHCP server responds with a DHCPOFFER listing an available IP and other network settings.
3. **Request:** The client broadcasts a DHCPREQUEST to accept an offer from a server (or to renew/confirm a lease).
4. **Acknowledge:** The DHCP server sends a DHCPACK to confirm the assignment and lease parameters.

### Components of DHCP
- **DHCP Server:** Stores IP addresses and configuration details. Allocates addresses dynamically or can provide static reservations for clients.
- **DHCP Relay (Agent):** Forwards DHCP messages between clients and servers when they are not on the same subnet.
- **DHCP Client:** Any device requesting an IP address and configuration from a DHCP server.
- **IP Address Pool (Scope):** A predefined range of IP addresses the server can lease to clients.

### DHCP messages & lifecycle
DHCP operates on UDP ports 67 (server) and 68 (client), and the DORA exchange is standard.

## Internet governance & resources
- For course slides and reference PDFs, see: `docs/pdfs/index.md`.

---

_This README intentionally summarizes course-level topics. For detailed routing content, see `routing/README.md` which contains protocol pages and references._


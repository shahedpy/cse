# ISP Roles

## Overview

Internet Service Providers (ISPs) play a critical role in the IP addressing ecosystem and general Internet connectivity. They serve as intermediaries between end users and the global Internet.

## Key ISP Roles

### 1. Address Allocation & Assignment

**Obtaining Addresses:**
- ISPs receive IP address blocks from Regional Internet Registries (RIRs)
- Must justify allocation size based on customer base and growth projections
- Larger ISPs may receive /16 or /20 blocks; smaller ISPs get /22 or /24

**Assigning to Customers:**
- **Residential** — typically dynamic IPs via DHCP (changes periodically)
- **Business** — static IPs or static blocks for servers/services
- **Hosting/Colocation** — larger blocks for data centers

### 2. Routing & Connectivity

**BGP Peering:**
- ISPs use BGP (Border Gateway Protocol) to exchange routing information
- Peer with other ISPs to provide global Internet connectivity
- Announce customer IP prefixes to the Internet

**Types of Peering:**
- **Transit** — purchasing connectivity from upstream ISP (Tier 1/2)
- **Peering** — free mutual exchange of traffic with other ISPs
- **IXP (Internet Exchange Point)** — physical interconnection facility

### 3. Network Address Translation (NAT)

ISPs use NAT to conserve IPv4 addresses:
- **Carrier-Grade NAT (CGN/CGNAT)** — large-scale NAT at ISP level
- Maps many customer private IPs to fewer public IPs
- Enables IPv4 conservation but complicates incoming connections

### 4. Core Services

**DNS Resolvers:**
- ISPs provide DNS servers for customer queries
- Example: ISP DNS at 8.8.8.8 (Google), 1.1.1.1 (Cloudflare)

**DHCP Servers:**
- Automatically assign IPs to customers
- Provide default gateway, subnet mask, DNS servers

**Email Services:**
- Many ISPs provide email hosting
- Spam filtering and security

### 5. IPv6 Migration Support

- Allocating IPv6 address space to customers
- Providing dual-stack (IPv4 + IPv6) connectivity
- Implementing transition mechanisms (6to4, tunneling)

## ISP Tiers

### Tier 1 ISPs
- **Definition:** Can reach entire Internet without purchasing transit
- **Characteristics:**
  - Operate backbone infrastructure
  - Peer with other Tier 1s
  - Global presence
- **Examples:** AT&T, Verizon, Level 3, NTT, Telia

### Tier 2 ISPs
- **Definition:** Purchase some transit from Tier 1, peer with others
- **Characteristics:**
  - Regional or national presence
  - Mix of transit and peering
  - Serve Tier 3 ISPs and large enterprises
- **Examples:** Regional carriers, national ISPs

### Tier 3 ISPs
- **Definition:** Purchase all transit from upstream ISPs
- **Characteristics:**
  - Local/regional focus
  - Serve end customers directly
  - Rely entirely on upstream connectivity
- **Examples:** Local broadband providers, cable companies

## ISP Network Topology

```
    [Tier 1 ISPs]
         |
    [Tier 2 ISPs]
         |
    [Tier 3 ISPs]
         |
   [End Customers]
```

## Peering Relationships

### Public Peering (IXP)
- Multiple ISPs connect at Internet Exchange Point
- Physical switch/fabric for interconnection
- Lower latency and cost than transit

**Major IXPs:**
- DE-CIX (Frankfurt)
- AMS-IX (Amsterdam)
- LINX (London)
- Equinix exchanges (global)

### Private Peering (PNI)
- Direct connection between two ISPs
- Dedicated fiber or wavelength
- Higher bandwidth, better control

### Transit
- One ISP pays another for connectivity
- Typical cost: per-Mbps or per-port pricing
- Includes access to provider's entire routing table

## ISP Responsibilities

1. **Address management** — efficient allocation and tracking
2. **Routing policy** — BGP configuration and filtering
3. **Security** — DDoS mitigation, abuse handling
4. **Network monitoring** — uptime, performance
5. **Customer support** — troubleshooting, provisioning
6. **Compliance** — government regulations, data retention

## Impact on Users

**What ISPs Control:**
- Your public IP address
- Default gateway and routing
- DNS resolution (unless you override)
- Upload/download speed limits
- Access to certain content (may block/filter)

**What You Can Do:**
- Request static IP (often extra cost)
- Use third-party DNS (Google, Cloudflare)
- Use VPN to bypass ISP-level filtering
- Monitor for NAT issues (CGNAT)

## ISP and NAT

Many ISPs now use **Carrier-Grade NAT (CGNAT)** due to IPv4 exhaustion:

**Implications:**
- Multiple customers share one public IP
- Harder to run servers from home
- Port forwarding may not work
- Some online games/P2P affected

**Check if you're behind CGNAT:**
```bash
# Check your public IP
curl ifconfig.me

# Compare to your router's WAN IP
# If they differ, you're likely behind CGNAT
```

## See Also

- [IANA & RIRs](iana-rir.md)
- [NAT](nat.md)
- [BGP](../routing/bgp.md)

## Course Materials

- Reference [Course PDFs](../docs/pdfs/index.md)

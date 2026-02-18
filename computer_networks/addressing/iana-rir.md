# IANA & Regional Internet Registries

## Overview

The Internet Assigned Numbers Authority (IANA) and Regional Internet Registries (RIRs) form the hierarchical system for global IP address allocation and management.

## IANA (Internet Assigned Numbers Authority)

IANA is responsible for coordinating:
- **IP address space allocation** — distributing address blocks to RIRs
- **Autonomous System (AS) numbers** — for BGP routing
- **Protocol parameters** — port numbers, protocol IDs
- **DNS root zone management** — top-level domains

**Website:** https://www.iana.org

## Regional Internet Registries (RIRs)

Five RIRs manage IP address allocation for different global regions:

### 1. ARIN (American Registry for Internet Numbers)
- **Region:** United States, Canada, Caribbean, North Atlantic islands
- **Website:** https://www.arin.net
- **Established:** 1997

### 2. RIPE NCC (Réseaux IP Européens Network Coordination Centre)
- **Region:** Europe, Middle East, parts of Central Asia
- **Website:** https://www.ripe.net
- **Established:** 1992

### 3. APNIC (Asia-Pacific Network Information Centre)
- **Region:** Asia-Pacific region
- **Website:** https://www.apnic.net
- **Established:** 1993

### 4. LACNIC (Latin America and Caribbean Network Information Centre)
- **Region:** Latin America and parts of the Caribbean
- **Website:** https://www.lacnic.net
- **Established:** 2002

### 5. AFRINIC (African Network Information Centre)
- **Region:** Africa
- **Website:** https://www.afrinic.net
- **Established:** 2005

## Address Allocation Hierarchy

```
IANA (Global)
    |
    ├── ARIN ──> ISPs/Large Organizations ──> End Users
    ├── RIPE NCC ──> ISPs/Large Organizations ──> End Users
    ├── APNIC ──> ISPs/Large Organizations ──> End Users
    ├── LACNIC ──> ISPs/Large Organizations ──> End Users
    └── AFRINIC ──> ISPs/Large Organizations ──> End Users
```

## How Address Allocation Works

### Step 1: IANA to RIRs
IANA allocates large blocks (typically /8 for IPv4, /12 for IPv6) to RIRs based on:
- Regional demand
- Population
- Internet growth projections
- Existing infrastructure

### Step 2: RIRs to ISPs/Organizations
RIRs allocate smaller blocks to:
- **ISPs** — Internet Service Providers
- **Large enterprises** — companies with justified need
- **National registries** — some countries have NIRs (National Internet Registries)

### Step 3: ISPs to End Users
ISPs further subdivide and assign addresses to:
- Residential customers (often dynamic)
- Business customers (static or dynamic)
- Hosting providers

## IPv4 vs IPv6 Allocation

### IPv4
- **Exhausted at IANA level** — last blocks allocated to RIRs in 2011
- **Limited availability** — RIRs managing remaining fragments
- **Strict justification** — must prove need for addresses
- **Transfer markets** — buying/selling unused IPv4 blocks

### IPv6
- **Abundant supply** — 128-bit address space (340 undecillion addresses)
- **Larger allocations** — /32 or /29 typical for ISPs
- **Encouraging adoption** — RIRs promote IPv6 deployment

## Address Policy

Each RIR has policies for:
- **Allocation size** — minimum/maximum blocks
- **Justification requirements** — documentation of need
- **Utilization rates** — must efficiently use allocated space
- **Sub-allocation rules** — how organizations can redistribute
- **Transfer policies** — selling/buying address blocks

## Whois Database

RIRs maintain public Whois databases showing:
- IP address block assignments
- Autonomous System (AS) numbers
- Contact information
- Organization details

**Example lookup:**
```bash
whois 8.8.8.8    # Google's DNS
whois AS15169    # Google's AS number
```

## IPv4 Exhaustion Timeline

| Date | Event |
|------|-------|
| Feb 2011 | IANA allocated last /8 blocks to RIRs |
| Apr 2011 | APNIC exhausted (entered final /8 policy) |
| Sep 2012 | RIPE NCC exhausted |
| Jun 2014 | LACNIC exhausted |
| Sep 2015 | ARIN exhausted (entered waiting list) |
| 2017-2018 | AFRINIC approaching exhaustion |

## See Also

- [ISP Roles](isp-roles.md)
- [NAT](nat.md)
- [Classless Addressing](classless-addressing.md)

## External Resources

- [IANA](https://www.iana.org)
- [Number Resource Organization](https://www.nro.net) — coordination body for RIRs

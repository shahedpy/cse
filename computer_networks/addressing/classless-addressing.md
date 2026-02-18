# Classless Inter-Domain Routing (CIDR)

## Overview

CIDR (Classless Inter-Domain Routing) was introduced to replace the rigid classful addressing system (Class A, B, C). It allows flexible allocation of IP address blocks using variable-length prefixes.

## Key Concepts

### CIDR Notation

CIDR notation: `A.B.C.D/N` where:
- `A.B.C.D` is the IP address
- `/N` is the prefix length (number of network bits)

**Example:** `192.168.10.0/24`
- Network: first 24 bits
- Host: last 8 bits (256 addresses)

### Prefix Length vs Subnet Mask

| CIDR | Subnet Mask | Usable Hosts | Network Size |
|------|-------------|--------------|--------------|
| `/8` | 255.0.0.0 | 16,777,214 | Class A equivalent |
| `/16` | 255.255.0.0 | 65,534 | Class B equivalent |
| `/24` | 255.255.255.0 | 254 | Class C equivalent |
| `/25` | 255.255.255.128 | 126 | Half of /24 |
| `/26` | 255.255.255.192 | 62 | Quarter of /24 |
| `/27` | 255.255.255.224 | 30 | |
| `/28` | 255.255.255.240 | 14 | |
| `/29` | 255.255.255.248 | 6 | |
| `/30` | 255.255.255.252 | 2 | Point-to-point links |
| `/31` | 255.255.255.254 | 2 | RFC 3021 p2p |
| `/32` | 255.255.255.255 | 1 | Single host |

## Benefits of CIDR

1. **Efficient address allocation** — allocate exactly the size needed
2. **Route aggregation** — combine multiple routes into one summary route
3. **Reduced routing table size** — fewer entries in global routing tables
4. **Flexibility** — not limited to /8, /16, /24 boundaries

## CIDR Supernetting

Supernetting (route aggregation) combines multiple smaller networks into a larger block:

**Example:**
- `192.168.0.0/24`
- `192.168.1.0/24`
- `192.168.2.0/24`
- `192.168.3.0/24`

Can be aggregated to: `192.168.0.0/22` (1024 addresses)

## Calculation Examples

### Example 1: Find network range for 192.168.50.10/26

1. `/26` = 255.255.255.192 (26 network bits, 6 host bits)
2. Block size = 2^6 = 64 addresses
3. Network ranges: .0-.63, .64-.127, .128-.191, .192-.255
4. 192.168.50.10 falls in `.0-.63` range
5. **Network:** 192.168.50.0/26
6. **Broadcast:** 192.168.50.63
7. **Usable:** 192.168.50.1 - 192.168.50.62

### Example 2: How many /27 networks fit in a /24?

- `/24` has 2^8 = 256 addresses
- `/27` has 2^5 = 32 addresses
- Number of /27 subnets = 256 / 32 = **8 subnets**

## See Also

- [Subnet Mask](subnet-mask.md)
- [Subnetting Basics](subnetting-basics.md)
- [VLSM](vlsm.md)
- [IANA & RIRs](iana-rir.md)

## Course Materials

- [Subnetting and VLSM.pdf](../Subnetting and VLSM.pdf)

# Network Protocols (ARP, RARP, DHCP)

This folder covers key network protocols for address resolution and configuration.

## Table of Contents

- [Address Resolution Protocol (ARP)](arp.md)
- [Reverse ARP (RARP)](rarp.md)
- [Dynamic Host Configuration Protocol (DHCP)](dhcp.md)
- [RTS/CTS Protocol](rts-cts.md)

## Overview

These protocols operate at the network and data link layers to enable:

1. **ARP** — maps IP addresses to MAC addresses (Layer 2 ↔ Layer 3)
2. **RARP** — maps MAC addresses to IP addresses (historical, replaced by DHCP)
3. **DHCP** — automatically assigns IP addresses and network configuration
4. **RTS/CTS** — wireless collision avoidance mechanism

## Protocol Comparison

| Protocol | Purpose | Layer | Direction |
|----------|---------|-------|-----------|
| ARP | Find MAC from IP | Layer 2/3 | IP → MAC |
| RARP | Find IP from MAC | Layer 2/3 | MAC → IP |
| DHCP | Auto-assign IP config | Application | Full config |
| RTS/CTS | Avoid wireless collisions | MAC/Layer 2 | Control |

## When to Use

- **ARP** — Always used in IPv4 networks (automatic)
- **RARP** — Obsolete (use DHCP instead)
- **DHCP** — Dynamic IP assignment (most networks)
- **RTS/CTS** — Wireless networks with hidden node problem

## Related Topics

- [IP Addressing](../addressing/README.md)
- [Wireless Networking](../wireless/README.md)
- [Routing Protocols](../routing/README.md)

## Course Materials

- [ARP,RARP,DHCP.pdf](../ARP,RARP,DHCP.pdf)
- [Lecture on MAC protocol1.pdf](../Lecture on MAC protocol1.pdf)

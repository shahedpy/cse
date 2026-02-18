# Wireless Networking

This folder covers wireless networking technologies and protocols.

## Table of Contents

- [Wireless Networking Basics](basics.md)
- [RTS/CTS Protocols](rts-cts.md)
- [Wi-Fi Architecture](wifi.md)
- [WiMAX Architecture](wimax.md)
- [Mobile Networks](mobile-networks.md)

## Overview

Wireless networking enables devices to communicate without physical cables. This section covers:

1. **Wireless basics** — radio frequency, modulation, standards
2. **RTS/CTS** — collision avoidance for hidden node problem
3. **Wi-Fi** — 802.11 standards and architecture
4. **WiMAX** — broadband wireless access
5. **Mobile networks** — cellular technologies

## Key Wireless Standards

### Wi-Fi (IEEE 802.11)

| Standard | Year | Frequency | Max Speed | Range |
|----------|------|-----------|-----------|-------|
| 802.11b | 1999 | 2.4 GHz | 11 Mbps | ~100m |
| 802.11a | 1999 | 5 GHz | 54 Mbps | ~50m |
| 802.11g | 2003 | 2.4 GHz | 54 Mbps | ~100m |
| 802.11n | 2009 | 2.4/5 GHz | 600 Mbps | ~200m |
| 802.11ac | 2013 | 5 GHz | 6.9 Gbps | ~100m |
| 802.11ax (Wi-Fi 6) | 2019 | 2.4/5 GHz | 9.6 Gbps | ~100m |

### WiMAX (IEEE 802.16)
- **Range** — up to 50 km
- **Speed** — up to 1 Gbps (fixed), 100 Mbps (mobile)
- **Use case** — broadband wireless alternative to cable/DSL

## Wireless Challenges

1. **Interference** — radio signals can overlap
2. **Hidden node problem** — nodes can't hear each other
3. **Signal attenuation** — walls, distance reduce signal
4. **Security** — wireless is inherently broadcast medium
5. **Bandwidth** — shared among all users

## MAC Protocols for Wireless

### CSMA/CA (Collision Avoidance)
- Listen before transmit
- Wait random backoff time
- Used in Wi-Fi (802.11)

### RTS/CTS
- Request to Send / Clear to Send
- Solves hidden node problem
- Optional in 802.11

## Related Topics

- [Network Protocols (ARP, DHCP)](../protocols/README.md)
- [Routing Protocols](../routing/README.md)

## Course Materials

- [Lecture on wireless.pdf](../Lecture on wireless.pdf)
- [Lecture on MAC protocol1.pdf](../Lecture on MAC protocol1.pdf)

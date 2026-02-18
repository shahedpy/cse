# Address Resolution Protocol (ARP)

## Overview

ARP maps IP addresses (Layer 3) to MAC addresses (Layer 2) on local networks. When a device needs to send data to an IP address on the same network, it must first discover the destination's MAC address.

## Why ARP?

- **IP addresses** are logical (can change, assigned by software)
- **MAC addresses** are physical (burned into network card)
- Ethernet frames require destination MAC address
- ARP bridges this gap

## How ARP Works

### Step 1: Check ARP Cache
Device checks its ARP table for IP → MAC mapping.

### Step 2: ARP Request (Broadcast)
If not in cache:
```
Who has 192.168.1.5? Tell 192.168.1.2
```
- Sent as broadcast (FF:FF:FF:FF:FF:FF)
- All devices on network receive it

### Step 3: ARP Reply (Unicast)
Device with matching IP responds:
```
192.168.1.5 is at AA:BB:CC:DD:EE:FF
```
- Sent directly to requester

### Step 4: Cache Entry
Requester stores mapping in ARP cache (typically 2-20 minutes).

## ARP Message Format

| Field | Size | Description |
|-------|------|-------------|
| Hardware Type | 2 bytes | Ethernet = 1 |
| Protocol Type | 2 bytes | IPv4 = 0x0800 |
| Hardware Addr Length | 1 byte | MAC = 6 bytes |
| Protocol Addr Length | 1 byte | IPv4 = 4 bytes |
| Operation | 2 bytes | Request = 1, Reply = 2 |
| Sender MAC | 6 bytes | Source MAC |
| Sender IP | 4 bytes | Source IP |
| Target MAC | 6 bytes | Destination MAC (0 in request) |
| Target IP | 4 bytes | Destination IP |

## ARP Cache

View ARP cache:

```bash
# Linux/macOS
arp -a
ip neigh show

# Windows
arp -a
```

Clear ARP cache:
```bash
# Linux
sudo ip neigh flush all

# macOS
sudo arp -d -a

# Windows (admin)
arp -d *
```

## Types of ARP

### 1. Gratuitous ARP
- Device announces its own IP → MAC mapping
- Used for:
  - Duplicate IP detection
  - Updating other hosts' caches
  - VRRP/HSRP failover

### 2. Proxy ARP
- Router answers ARP on behalf of another device
- Allows communication across subnets without routing table

### 3. Reverse ARP (RARP)
- MAC → IP (opposite of ARP)
- Obsolete (replaced by DHCP)
- See [RARP](rarp.md)

## Security Issues

### ARP Spoofing/Poisoning
Attacker sends fake ARP replies:
```
192.168.1.1 is at ATTACKER_MAC
```

**Result:**
- Traffic intended for gateway goes to attacker
- Man-in-the-Middle (MITM) attack

### Mitigation
1. **Static ARP entries** (manual, not scalable)
2. **Dynamic ARP Inspection (DAI)** on switches
3. **ARP monitoring tools** (arpwatch)
4. **Network segmentation**

## Troubleshooting

### Problem: No ARP reply
```bash
ping 192.168.1.5
# Destination Host Unreachable
```

**Possible causes:**
- Device is down
- Firewall blocking
- Wrong subnet (need routing)
- Network cable issue

### Problem: Wrong MAC in ARP cache
```bash
arp -d 192.168.1.5  # Delete entry
ping 192.168.1.5    # Force new ARP
```

## ARP vs NDP (IPv6)

IPv6 uses **Neighbor Discovery Protocol (NDP)** instead of ARP:
- More efficient
- Built-in security (IPsec)
- Uses ICMPv6 messages

## See Also

- [RARP](rarp.md)
- [DHCP](dhcp.md)
- [IP Addressing](../addressing/README.md)

## Course Materials

- [ARP,RARP,DHCP.pdf](../ARP,RARP,DHCP.pdf)

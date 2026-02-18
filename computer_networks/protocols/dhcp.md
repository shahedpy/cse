# Dynamic Host Configuration Protocol (DHCP)

## Overview

DHCP automatically assigns IP addresses and network configuration to devices, eliminating manual configuration.

## What DHCP Provides

- IP address
- Subnet mask
- Default gateway
- DNS servers
- Domain name
- Lease time
- Other options (NTP, TFTP, etc.)

## DHCP Process: DORA

### 1. Discover (D)
Client broadcasts:
```
"I need an IP address!"
Source: 0.0.0.0:68
Destination: 255.255.255.255:67
```

### 2. Offer (O)
Server(s) respond:
```
"Here's 192.168.1.100 for you"
+ subnet mask, gateway, DNS
```

### 3. Request (R)
Client accepts offer:
```
"I accept 192.168.1.100 from Server X"
Broadcast (other servers withdraw offers)
```

### 4. Acknowledge (A)
Server confirms:
```
"Confirmed! Lease for 24 hours"
```

## DHCP Components

### DHCP Server
- Stores IP pools and configuration
- Tracks leases
- Can reserve IPs for specific MACs

### DHCP Client
- Built into OS
- Requests IP on boot/network connect

### DHCP Relay
- Forwards DHCP requests between subnets
- Allows centralized DHCP server

## Lease Management

### Lease Timeline
```
T0: Lease begins (24 hours example)
T1 (50%): Try renew with same server (12 hours)
T2 (87.5%): Try renew with any server (21 hours)
Expiry: Release IP, restart DORA
```

### Renewal (Unicast)
```
Client → Server: DHCPREQUEST
Server → Client: DHCPACK (extend lease)
```

### Release (Optional)
```
Client → Server: DHCPRELEASE
"I'm done with this IP"
```

## DHCP Messages

| Message | Description |
|---------|-------------|
| DHCPDISCOVER | Client looking for server |
| DHCPOFFER | Server offers IP |
| DHCPREQUEST | Client requests IP |
| DHCPACK | Server confirms |
| DHCPNAK | Server denies request |
| DHCPRELEASE | Client releases IP |
| DHCPINFORM | Request config (already has IP) |
| DHCPDECLINE | Client rejects IP (conflict) |

## DHCP Options

Common options:

| Option | Description |
|--------|-------------|
| 1 | Subnet mask |
| 3 | Default gateway |
| 6 | DNS servers |
| 15 | Domain name |
| 42 | NTP servers |
| 51 | Lease time |
| 54 | Server identifier |
| 66 | TFTP server (for PXE boot) |

## IP Reservation

Assign specific IP to MAC address:
```
MAC: AA:BB:CC:DD:EE:FF → 192.168.1.50
```

**Use cases:**
- Servers
- Printers
- Network equipment

## DHCP vs Static IP

| Feature | DHCP | Static |
|---------|------|--------|
| Configuration | Automatic | Manual |
| Scalability | Excellent | Poor |
| Maintenance | Low | High |
| Control | Server-side | Device-side |
| Best for | Clients, BYOD | Servers, network gear |

## Troubleshooting

### Problem: No IP assigned

```bash
# Linux/macOS
ifconfig  # or ip addr
# Look for 169.254.x.x (APIPA)

# Windows
ipconfig
```

**Causes:**
- DHCP server down
- No available IPs in pool
- Network cable issue
- Firewall blocking ports 67/68

### Fix: Renew lease

```bash
# Linux
sudo dhclient -r  # release
sudo dhclient     # renew

# macOS
sudo ipconfig set en0 DHCP

# Windows
ipconfig /release
ipconfig /renew
```

## DHCP Relay

When DHCP server is on different subnet:

```
Client (VLAN 10) → Router (DHCP Relay) → Server (VLAN 1)
```

Router config (example):
```
interface vlan 10
 ip helper-address 192.168.1.10
```

## Security Considerations

### DHCP Snooping
- Switch feature
- Prevents rogue DHCP servers
- Validates DHCP messages

### DHCP Starvation Attack
- Attacker requests all IPs
- Legitimate clients can't get IP
- Mitigation: rate limiting, DHCP snooping

## See Also

- [ARP](arp.md)
- [RARP](rarp.md)
- [IP Addressing](../addressing/README.md)

## Course Materials

- [ARP,RARP,DHCP.pdf](../ARP,RARP,DHCP.pdf)

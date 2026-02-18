# Reverse Address Resolution Protocol (RARP)

## Overview

RARP is the reverse of ARP: it maps **MAC addresses** (Layer 2) to **IP addresses** (Layer 3). Used by diskless workstations to discover their IP address on boot.

## Historical Context

### The Problem (1980s)
- Diskless workstations had no storage
- Knew their MAC (burned into ROM)
- Needed IP address to communicate
- No DHCP yet (invented 1993)

### RARP Solution
```
I have MAC AA:BB:CC:DD:EE:FF
What is my IP address?
```

## How RARP Works

### Step 1: RARP Request (Broadcast)
```
Source MAC: AA:BB:CC:DD:EE:FF
Destination MAC: FF:FF:FF:FF:FF:FF (broadcast)

"Who knows the IP for AA:BB:CC:DD:EE:FF?"
```

### Step 2: RARP Reply (Unicast)
RARP server responds:
```
"AA:BB:CC:DD:EE:FF has IP 192.168.1.100"
```

### Step 3: Client Configuration
Client configures interface with assigned IP.

## RARP vs ARP

| Feature | ARP | RARP |
|---------|-----|------|
| **Direction** | IP → MAC | MAC → IP |
| **Used by** | All devices | Diskless workstations |
| **Server needed** | No | Yes |
| **Broadcast** | Request only | Request only |
| **Obsolete** | No (still used) | Yes |

## RARP Message Format

Same structure as ARP, different operation code:

| Field | Value |
|-------|-------|
| Hardware Type | 1 (Ethernet) |
| Protocol Type | 0x0800 (IPv4) |
| Hardware Addr Length | 6 (MAC) |
| Protocol Addr Length | 4 (IPv4) |
| **Operation** | **3** (RARP Request) or **4** (RARP Reply) |
| Sender MAC | Client MAC |
| Sender IP | 0.0.0.0 (unknown) |
| Target MAC | Client MAC |
| Target IP | Filled by server in reply |

Compare to ARP operations: 1 = Request, 2 = Reply

## RARP Server Requirements

1. **Server on each subnet**
   - RARP uses broadcast (doesn't cross routers)
   - Each network segment needs RARP server

2. **MAC-to-IP database**
   ```
   AA:BB:CC:DD:EE:FF → 192.168.1.100
   11:22:33:44:55:66 → 192.168.1.101
   ```

3. **Always on**
   - Must respond when clients boot

## Limitations of RARP

### 1. Only Provides IP Address
- No subnet mask
- No gateway
- No DNS servers
- Client must manually configure these

### 2. Not Scalable
- Manual MAC-to-IP mapping
- Server required per subnet

### 3. No Lease Management
- No IP reclamation
- Permanent assignment

### 4. Broadcast Limitations
- Cannot cross routers
- Increases network traffic

## RARP Successors

### BOOTP (1985)
**Improvements over RARP:**
- Provides gateway, DNS, etc.
- Can cross routers (uses UDP)
- Still requires manual configuration

### DHCP (1993)
**Modern solution:**
- Dynamic IP assignment
- Full network configuration
- Lease management
- No per-client configuration
- Scalable

**Migration path:**
```
RARP (1984) → BOOTP (1985) → DHCP (1993)
```

## When RARP Was Used

### Typical scenario:
```
1. Diskless workstation powers on
2. ROM bootloader broadcasts RARP request
3. RARP server responds with IP
4. Workstation uses TFTP to download OS image
5. Boot completes
```

### Examples:
- Sun workstations (1980s-1990s)
- Thin clients
- Network boot systems (before PXE)

## Modern Equivalents

Today, diskless boot uses:

1. **PXE (Preboot Execution Environment)**
   - Uses DHCP for IP assignment
   - TFTP for boot image

2. **iPXE**
   - HTTP-based boot
   - More features than PXE

3. **Network boot** still common for:
   - Imaging systems
   - Terminal servers
   - Embedded devices

## Packet Capture Example

### RARP Request:
```
Ethernet II
  Source: Dell_11:22:33 (AA:BB:CC:DD:EE:FF)
  Destination: Broadcast (FF:FF:FF:FF:FF:FF)
  Type: RARP (0x8035)

RARP Request
  Operation: Request (3)
  Sender MAC: AA:BB:CC:DD:EE:FF
  Sender IP: 0.0.0.0
  Target MAC: AA:BB:CC:DD:EE:FF
  Target IP: 0.0.0.0
```

### RARP Reply:
```
Ethernet II
  Source: Server_AA:BB:CC (00:11:22:33:44:55)
  Destination: Dell_11:22:33 (AA:BB:CC:DD:EE:FF)
  Type: RARP (0x8035)

RARP Reply
  Operation: Reply (4)
  Sender MAC: 00:11:22:33:44:55
  Sender IP: 192.168.1.1
  Target MAC: AA:BB:CC:DD:EE:FF
  Target IP: 192.168.1.100
```

## Why RARP is Obsolete

1. **DHCP does everything RARP did, plus more**
2. **No RARP in IPv6** (uses NDP + DHCPv6)
3. **Modern NICs support PXE boot**
4. **Diskless workstations rare today**

## See Also

- [ARP](arp.md)
- [DHCP](dhcp.md)
- [IP Addressing](../addressing/README.md)

## Course Materials

- [ARP,RARP,DHCP.pdf](../ARP,RARP,DHCP.pdf)

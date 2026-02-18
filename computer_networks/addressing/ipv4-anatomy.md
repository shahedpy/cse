# IPv4 Address Anatomy

## Overview

An IPv4 address is a 32-bit number that uniquely identifies a network interface. Understanding its structure is fundamental to networking.

## Structure

### Binary Representation

```
11000000.10101000.00000001.00000001
```

### Decimal (Dotted-Quad) Notation

```
192.168.1.1
```

- 4 octets (bytes) separated by dots
- Each octet: 0-255 (8 bits)
- Total: 32 bits

## Two-Part Address

Every IPv4 address consists of:

1. **Network portion** — identifies the network
2. **Host portion** — identifies the device on that network

### Example: 192.168.10.5/24

```
Network:  192.168.10    (first 24 bits)
Host:     5              (last 8 bits)
```

## Conversion: Binary ↔ Decimal

### Decimal to Binary

```
192 = 128 + 64 = 11000000
168 = 128 + 32 + 8 = 10101000
1 = 00000001
1 = 00000001

Result: 11000000.10101000.00000001.00000001
```

### Binary Powers of 2

| 128 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
|-----|----|----|----|----|----|----|----|
| 2^7 | 2^6 | 2^5 | 2^4 | 2^3 | 2^2 | 2^1 | 2^0 |

## Address Classes (Historical)

Classful addressing divided IPs into fixed classes:

| Class | First Octet | Default Mask | Networks | Hosts/Network |
|-------|-------------|--------------|----------|---------------|
| A | 1-126 | /8 (255.0.0.0) | 126 | 16,777,214 |
| B | 128-191 | /16 (255.255.0.0) | 16,384 | 65,534 |
| C | 192-223 | /24 (255.255.255.0) | 2,097,152 | 254 |
| D | 224-239 | Multicast | N/A | N/A |
| E | 240-255 | Reserved | N/A | N/A |

**Note:** Classful addressing is obsolete; CIDR is used today.

## Special Addresses

### Network Address
- All host bits = 0
- Example: 192.168.1.0/24
- Cannot be assigned to a device

### Broadcast Address
- All host bits = 1
- Example: 192.168.1.255/24
- Sent to all devices on the network

### Loopback
- 127.0.0.0/8 (typically 127.0.0.1)
- Refers to "this computer"
- Used for testing

### Private Addresses (RFC 1918)
- 10.0.0.0/8
- 172.16.0.0/12
- 192.168.0.0/16
- Not routable on Internet

### Link-Local (APIPA)
- 169.254.0.0/16
- Auto-assigned when DHCP fails

## See Also

- [Subnet Mask](subnet-mask.md)
- [Classless Addressing](classless-addressing.md)
- [Subnetting Basics](subnetting-basics.md)

## Course Materials

- [Subnetting and VLSM.pdf](../Subnetting and VLSM.pdf)

# Network Address Translation (NAT)

## Overview

Network Address Translation (NAT) allows multiple devices on a private network to share a single public IP address (or a small pool of public IPs) for Internet access. NAT is a key technology for IPv4 address conservation.

## Why NAT?

1. **Address conservation** — thousands of private IPs map to one/few public IPs
2. **Security** — hides internal network structure
3. **Flexibility** — change internal addressing without affecting external connectivity

## Private Address Ranges (RFC 1918)

These addresses are reserved for private networks and not routable on the Internet:

| Range | CIDR | Classful Equivalent | Total Addresses |
|-------|------|---------------------|-----------------|
| 10.0.0.0 - 10.255.255.255 | 10.0.0.0/8 | 1 Class A | 16,777,216 |
| 172.16.0.0 - 172.31.255.255 | 172.16.0.0/12 | 16 Class B | 1,048,576 |
| 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 | 256 Class C | 65,536 |

## Types of NAT

### 1. Static NAT (One-to-One)

Maps one private IP to one public IP permanently.

```
Private IP         Public IP
10.0.0.5    <-->   203.0.113.5
10.0.0.6    <-->   203.0.113.6
```

**Use case:** Servers that need consistent public IP

### 2. Dynamic NAT (Pool)

Maps private IPs to a pool of public IPs on a first-come basis.

```
Private IP Pool    Public IP Pool
10.0.0.0/24  <-->  203.0.113.10-203.0.113.20
```

**Limitation:** Number of simultaneous connections = pool size

### 3. PAT (Port Address Translation) / NAT Overload

Maps multiple private IPs to ONE public IP using different ports. This is the most common NAT type (used in home routers).

```
Internal              External (Internet)
10.0.0.5:52000  <-->  203.0.113.1:52000
10.0.0.6:52001  <-->  203.0.113.1:52001
10.0.0.7:52002  <-->  203.0.113.1:52002
```

## How NAT Works

### Outbound Traffic
1. Internal host (10.0.0.5:3000) sends packet to external server (198.51.100.10:80)
2. NAT device replaces source IP:port with public IP:translated-port (203.0.113.1:52000)
3. NAT maintains translation table entry
4. Packet forwarded to Internet

### Inbound (Return) Traffic
1. Server responds to 203.0.113.1:52000
2. NAT checks translation table
3. NAT translates destination to 10.0.0.5:3000
4. Packet forwarded to internal host

## NAT Translation Table Example

| Inside Local | Inside Global | Outside Global | Outside Local |
|--------------|---------------|----------------|---------------|
| 10.0.0.5:3000 | 203.0.113.1:52000 | 198.51.100.10:80 | 198.51.100.10:80 |
| 10.0.0.6:3001 | 203.0.113.1:52001 | 203.0.113.50:443 | 203.0.113.50:443 |

## Advantages

- **IPv4 conservation** — critical for delaying IPv4 exhaustion
- **Security layer** — internal IPs hidden from outside
- **Flexibility** — change internal addressing scheme without reconfiguring Internet connection

## Disadvantages

- **Breaks end-to-end connectivity** — some protocols/apps have issues
- **Performance overhead** — translation processing
- **Complicates troubleshooting** — harder to trace connections
- **Port forwarding needed** — for incoming connections to internal servers

## NAT and IPv6

IPv6 has such a large address space that NAT is generally unnecessary. IPv6 promotes end-to-end connectivity without translation.

## See Also

- [ISP Roles](isp-roles.md)
- [Classless Addressing](classless-addressing.md)
- [IPv4 Address Anatomy](ipv4-anatomy.md)

## Course Materials

- Reference main [Course PDFs](../docs/pdfs/index.md)

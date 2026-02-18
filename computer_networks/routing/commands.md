# Routing: Commands & CLI Cheatsheet

This page lists common troubleshooting and verification commands; exact syntax differs by vendor (Cisco, Juniper, Linux).

## General
- `ping <destination>` — test reachability
- `traceroute <destination>` — path & hop test (Linux `traceroute`, Windows `tracert`)
- `show ip route` — view routing table (RIB)

## OSPF
- `show ip ospf neighbor` — OSPF neighbor relationships
- `show ip ospf interface` — OSPF interface information
- `show ip ospf database` — LSDB contents

## RIP
- `show ip rip database` — RIP database
- `debug ip rip` — debug updates (use carefully)

## BGP
- `show ip bgp summary` — show BGP session state
- `show ip bgp` — BGP table and attributes
- `show ip bgp <network> vrf <vrf>` (platform-specific) — BGP route detail

## EIGRP
- `show ip eigrp neighbors` — view EIGRP neighbors
- `show ip eigrp topology` — EIGRP topology information

## Helpful Linux commands
- `ip route show` or `route -n` — linux route table
- `ip neigh` — neighbor/arp table on linux

**Tip:** Always use vendor docs to confirm exact command parameters; the above are representative examples across platforms.

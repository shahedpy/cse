# BGP (Border Gateway Protocol)

## Summary

BGP is a path-vector protocol used to exchange reachability information between Autonomous Systems (AS). It is the protocol that makes Internet inter-domain routing work.

## Key Characteristics

- Path-vector protocol (AS path, route attributes).
- Operates between ASes (exterior gateway protocol, EGP) and sometimes internally (iBGP within the same AS).
- Policy-driven: BGP uses route attributes and local policies for path selection and export decisions.
- Scalability: Designed to handle very large numbers of prefixes across the Internet.

## Common attributes

- **AS-PATH:** Sequence of ASes a route has traversed.
- **NEXT_HOP / NEXT_HOP attribute:** IP to next hop.
- **LOCAL_PREF:** Local preference used to prefer one eBGP route over another inside an AS.
- **MED (Multi-Exit Discriminator):** Suggests preferred entry point to neighboring AS (lower preferred).
- **COMMUNITY:** Tagging mechanism used for policy.

## Operational Notes

- BGP sessions are typically established over TCP port 179.
- iBGP requires either full mesh or route reflection to avoid loops (or use confederations).
- Route filtering and prefix-lists are essential to avoid accidental route leaks.

## Commands / examples

- `show ip bgp summary` — BGP peering status
- `show ip bgp` — BGP table
- `show ip bgp <prefix>` — details about prefix and attributes

## See also
- `routing/concepts.md`
- Course PDFs under `docs/pdfs/` for more details and slides
## Further reading
- [PDFs & slides](../docs/pdfs/index.md)

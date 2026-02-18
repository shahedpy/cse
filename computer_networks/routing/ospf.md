# OSPF (Open Shortest Path First)

## Summary

OSPF is a link-state interior gateway protocol (IGP) that uses Dijkstra’s algorithm to compute shortest paths. It offers fast convergence and support for hierarchical design (areas), including backbone area (area 0).

## Key Characteristics

- Link-state protocol with LSAs (Link State Advertisements).
- Metric: cost (typically derived from bandwidth; administrative policies may adjust it).
- Supports areas (backbone area 0) for hierarchical design and scaling.
- Fast convergence due to event-driven LSA flooding and local recomputation.

## OSPF Components

- **Router Types:** Internal Router, Area Border Router (ABR), Autonomous System Boundary Router (ASBR).
- **LSAs/LSDB:** Routers flood LSAs to share topology; each router maintains a Link-State Database (LSDB).
- **DR/BDR:** On broadcast multi-access segments (Ethernet) OSPF elects a Designated Router to reduce flooding.

## Commands / examples

- `show ip ospf neighbor` — display OSPF neighbors and state.
- `show ip ospf database` — examine LSDB content.
- `show ip route ospf` — display routes learned via OSPF.

## See also
- `routing/concepts.md`
- `routing/rip.md` (for comparison)
- Course PDFs under `docs/pdfs/` for deeper reading
## Further reading
- [PDFs & slides](../docs/pdfs/index.md)

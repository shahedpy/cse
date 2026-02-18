# Routing Concepts

This document summarizes the routing primitives and operational concepts.

## Routing families

- **Distance-vector:** Routers keep a table of destinations and next hops with a metric for cost (e.g., RIP uses hop count). Routers periodically share their routing tables with neighbors.
- **Link-state:** Routers flood topology information (LSAs) and compute shortest paths using Dijkstra’s algorithm.
- **Path-vector:** Used primarily by BGP to maintain AS-level paths and to allow policy decisions.
- **Hybrid:** Combine advantages of distance-vector and link-state (e.g., EIGRP uses DUAL algorithm).

## Metrics and path selection

- Metrics may be based on hop count, bandwidth, delay, reliability, or composite costs.
- Administrative distance is a local preference factor (lower values preferred) for route selection between multiple sources.

## Operational concepts

- **RIB (Routing Information Base):** All routes learned by control plane.
- **FIB (Forwarding Information Base):** Forwarding table used by data plane (may be derived from RIB).
- **Convergence:** The time it takes for network topology changes to be propagated and for routers to compute new paths.
- **Route summarization:** Aggregating smaller prefixes into a larger one to reduce the number of routes.
- **Route redistribution:** Sharing routes between routing protocols and the complexities involved (metric translation, filtering).
- **Split horizon and poison reverse:** Techniques to reduce count-to-infinity on distance-vector protocols.

## Monitoring & Troubleshooting

- Verify routing tables: `show ip route` (platform-specific)
- Check routing protocol neighbors: `show ip ospf neighbor`, `show ip bgp summary`, `show ip eigrp neighbors` etc.
- Check interface states and reachability with `ping` and `traceroute`.

## References
- Course materials (see `docs/pdfs`)

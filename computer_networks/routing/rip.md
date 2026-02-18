# RIP (Routing Information Protocol)

## Summary

RIP is a simple distance-vector protocol that uses hop count as a metric. It has a maximum hop count (typically 15) which makes it suitable for small, simple networks.

## Key Characteristics

- Distance-vector algorithm (Bellman-Ford based).
- Metric: hop count (max 15).
- Periodic updates (default 30 seconds).
- Convergence time can be slow; vulnerable to the "count-to-infinity" problem.

## Mechanisms for loop prevention

- **Split horizon:** Do not send route back to the neighbor you learned it from.
- **Split horizon with poison reverse:** Advertise invalid route with infinite metric to the neighbor.
- **Triggered updates:** Immediately send updates on a topological change (instead of waiting for periodic timer) to speed up convergence.

## Known drawbacks

- Poor scalability due to hop-count limits and frequent updates.
- Slow convergence and susceptibility to routing loops without correct implementations of split-horizon or poison-reverse.

## Commands / examples

- `show ip route` — view route entries (platform-dependent)
- `show ip rip database` or `show ip protocols | include rip` — many platforms have RIP-specific debug/monitor commands.

## See also
- `routing/concepts.md`
- `routing/ospf.md` (for comparison)
- Course PDFs under `docs/pdfs/`
## Further reading
- [PDFs & slides](../docs/pdfs/index.md)

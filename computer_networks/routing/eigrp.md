# EIGRP (Enhanced Interior Gateway Routing Protocol)

## Summary

EIGRP is a Cisco-developed hybrid routing protocol that uses features of both distance-vector and link-state algorithms, with its own DUAL algorithm for loop-free and fast convergence.

## Key Characteristics

- Uses a composite metric (bandwidth, delay, reliability) to compute path costs.
- Supports unequal-cost load balancing with the `variance` parameter.
- DUAL (Diffusing Update Algorithm) allows fast reconvergence and loop-free operation.
- Cisco proprietary (historically); some variants implemented as open standard (EIGRP for IPv6, etc.).

## Commands / notes

- `show ip eigrp neighbors` — neighbors and topology info
- `show ip eigrp topology` — EIGRP topology table

## See also
- `routing/concepts.md` for operational concepts
- `routing/ospf.md` and `routing/rip.md` for comparison
## Further reading
- [PDFs & slides](../docs/pdfs/index.md)

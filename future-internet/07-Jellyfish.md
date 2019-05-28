# Paper summary <br> [Jellyfish: Networking Data Centers Randomly](https://www.usenix.org/conference/nsdi12/technical-sessions/presentation/singla)

### Summary

Jellyfish is a high-capacity network interconnect which, by adopting a random graph topology, yields itself naturally to incremental expansion.

### Goals

- allow incremental network expansion
   - structured networks constrain expansion
   - leaving free ports wastes investment until usage
   - oversubscribing switches makes distribution uneven
- providing high per-server bandwidth

### Intuition: bounding throughput

```
#flows * cap_per_flow <= total_cap (1)
cap_per_flow = thp_per_flow * mean_path_len (2)

#flows * thp_per_flow * mean_path_len <= total_cap (3) (by (1) and (2))
thp_per_flow <= total_cap / (#flows * mean_path_len) (by (3))
```

Thus, the throughput per flow is bounded by the inverse of mean path length. Hence, decreasing the path length might result in bigger throughput.

**Degree diameter problem:** What is the maximum number of nodes in any graph with degree ∂ and diameter d?

**Objective:** get mean path length down given the constraints on (d,  ∂) graph parameters.

### Topology construction

- **Main idea:** Build a random graph at the ToR switch layer.
  - each ToR switch with k<sub>i</sub> ports uses r<sub>i</sub> for connecting with other ToR switches
  - with N racks, network supports *N(k - r)* servers
- **Topology building/extension:**
  - pick a random pair of switches with free ports and add connection
  - for adding a new switch *u* a random link *(x, y)* can be cut, adding links *(u, x)* and *(u, y)*

### Topology properties

- lower mean path length than fat-tree
- higher bisection bandwidth than fat-tree
   - **bisection bandwidth:** the worst-case bandwidth between any 2 equal-sized partitions of a network
   - a common measure of network capacity since the links passing through the bisection would become the bottleneck
- better failure resilience than fat-tree: intuition is that after cutting a server or edge, graph is still random enough
- less cost of expansion

### Routing and Congestion Control

- ECMP performs poorly on Jellyfish as it does not provide enough path diversity
- **k-shortest paths**:
   - intuition: we want to also use longer paths
   - works good with either TCP or Multi-path TCP
   - possible implementation: OpenFlow switches randomly distributing load over allowed paths

### Cabling

- group racks into clusters:
  - each cluster connects to some central racks with switches
  - cabling between clusters is done with aggregate cable bundles running between them

# [LLPD](https://dl.acm.org/authorize.cfm?key=N666831)

### Paper summary
LLPD is a metric which quantifies a WAN routing algorithms degree of capability of routing around congestion hotspots. It is agnostic of traffic matrices and routing algorithms by summarizing the APA metric curve into a single metric. The paper shows that in practice classical shortest path algorithms don't work well on high-LLPD topologies and designs the LDR algorithm for this purpose. The LDR algorithm minimizes propagation delay under the primary objective of avoiding congestion. It dynamically changes a link headroom by predicting when link capacity will be exceeded.

### Key insight(s)
- APA represents the fraction of links on a shortest for which the routing on alternative paths does not exceed a given path stretch. The LLPD summarizes the APA distribution for a given topology.
- A close to 0 LLPD means no path choice(i.e. trees), while a LLPD close to 1 means lots of choices when shortest path links are available.
- Classical routing algorithms don't work on real topolgies with big LLPDs.
- A MinMax approach that minimizes the maximum traffic utilization results in higher latencies, while shortest path algorithms result in congested links.
- LDR minimizes propagation delay while avoiding congestion. Since is designed for ISPs, capping the maximum capacity of links is necessary. (the so-called, allocation headroom)
- LDR changes the path allocation for links by using linear programming.
- The headroom is changed when congestion is predicted. We can predict congestion from the temporal correlation of traffic allocations and from uncorrelated multiplexing of different aggregation links.

### What could be improved?
I find the paper very interesting, but not very well structured. The discussion on LLPD could have been shorter while insisting more on MinMax and LDR.

The paper specifies that uses the gravity model for matrix generation in order for the traffic matrix to fit the topology. Is there any reason why we cannot use real traffic patterns on topologies, but we rather work with traffic matrices?

If parts of the network are congested, wouldn't that change the traffic pattern, resulting in a different traffic matrix? If so, aren't they a bit harsh on the performance of shortest path routing since they keep a static traffic matrix?

They mention that using a low-pass filter for latencies has been used before to improve MinMax. Couldn't we use a dynamic filter for MinMax in a similar fashion to the congestion prediction they use for LDR?

It was not very clear to me how they deal with temporal correlation for evaluating multiplexing.

Finally, I like the insight of fitting the routing algorithm to the topology. It raises the question of what kind of network topologies would one be able to design if he knows that the routing will "fit" the topology.

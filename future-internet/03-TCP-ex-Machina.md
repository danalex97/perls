# [TCP ex Machina: Computer-Generated Congestion Control](http://nms.csail.mit.edu/papers/sigcomm13.pdf)

### Paper summary

The paper describes a program that generates congestion-control algorithms. The input of Remy is prior assumptions of the network and the optimization objective. The prior assumptions refer to the traffic patter, link speed range, RTT range, etc. The traffic used for training is modeled as a stochastic process that switches unicast flows between sender-receivers pairs on or off. This prior assumptions are used directly in simulations when solving the optimization problem formulated by the Remy algorithm. The optimization problem assumes that everybody runs the Remy algorithm. Remy generates an algorithm that maps a limited state of past events to actions to take in congestion changes. The contestion algorithm will use these mapping to adjust the congestion window.

### Key insight(s)

- The prior assumptions refer to the traffic patter, link speed range, RTT range, etc. The traffic used for training is modeled as a stochastic process that switches unicast flows between sender-receivers pairs on or off. We note these are not directly relevant, but are rather used when doing simulation for optimizing Remy.

- The congestion algorithm keeps a limited state. Remy defines a set of automatic rules that map the state to a congestion window change:

```
On ACK:
  <m, b, t> = RULE(state)
  cwnd = m * cwnd + b

Send packet if:
  cwnd > FlightSize AND
  last_packet_sent > time_now - t
```

- The default objective function describes trade-off between throughput and delay on multiple connections, which is used by the optimizer that runs the simulations.

- The optimizer splits the state input at median of each measurement value. The most used rule in an epoch is optimized by varying the output, that is the <m, b, t> value is varied and the optimization objective is measured. This will alternate by modifying the divisions of the states, until we can't obtain further improvements. At this point, the most used rule is divided across median measurements. In a way, this works like a Divide et Impera algorithm.

### Reflection

The paper approached congestion control in an original way, trying to optimize for a particular model, rather than trying to explicitly formulate observations. Exactly by this argument, I think that this approach is hard to be deployed since it wouldn't fit well with variable network conditions.

Conversely, in a limited setup such as connections in the same autonomous systems or data centers, this can work better. However, this suggests breaking the end-to-end principle. This can be overcome if the topology we are optimizing for is using an overlay. For example, an application such as multi-hop overlays could use this congestion algorithm on individual segments.

A sight criticism regards the evaluation on cellular networks. The experiments should have been placed in a similar setting to Sprout(since both are from MIT), to make the comparisons more credible.

Finally, I think the problem of this algorithm is that it should firstly detect the type of network it is running on, based on some empirical measurements, and then select the rules for that setting.

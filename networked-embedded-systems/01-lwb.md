# [Low-Power Wireless Bus](https://homepages.dcc.ufmg.br/~mmvieira/cc/papers/ferrari12lowpower.pdf)

### Summary

LWB is a communication protocol that supports several traffic patterns and mobile nodes immersed in static infrastructures. It turns a multi-hop low-power wireless network into an infrastructure similar to a shared bus, where all nodes are potential receivers of all data.  

### Paper strengths

The general design argument of the paper is compelling: protocols designed in isolation are often combined, which incurs more overhead rather than designing the whole stack.

The shared bus abstraction is appropriate since we want to model 1-to-M, M-to-1 and M-to-M communication. Probably the most important takeaway of this abstraction is that it enables topology independence, which makes state management much easier. Moreover, topology independence helps mitigate node failures and allows node mobility.

Different traffic demands are supported via the scheduler and variable round periods. This is well addressed in the evaluation section by the light, heavy and fluctuating traffic experiments.

The bootstrapping mechanism was easy to follow and effective. The example in the paper helps a lot in understanding the mechanism.

The protocol does not need much tuning, which makes it easy to reason about and compare with. In contrast, in each experiment, one has to think about what kind of LPL thresholds to use.

I think piggybacking is leveraged quite good, dealing with new requests in an effective way.

Finally, I like the general paper style and I think the examples make it easy to follow.

### Paper weaknesses

In some setting, there might more classes of nodes with different power needs. Therefore, the optimization objective of energy might not be homogeneous across all nodes. In my opinion, this makes the protocol hard to adapt to a heterogeneous energy objective since every node contributes equally to each flooding.

Another point that is barely touched upon is network partitioning. For example, what happens with synchronization when a partition happens and then the parts are joined back together?

Glossy is mentioned a few times, but its description is not very broad. To make the paper more self-contained, a short explanation of it would have been useful.

Giving example after each section sometimes makes the paper harder to follow. Maybe some sections didn't need examples at all. I did not find the steady-state example very useful; maybe a more complicated example would have helped to get the point across well.

### Open questions and improvement

I wonder whether flooding makes sense all the time. For example, push-based gossip might actually give the same results on some topologies and it reduces the number of transmissions. Fewer transmissions can be useful if someone wants to transmit multiple messages at the same time. This might apply to power consumption improvements as well, but I am not very convinced since the radio would still be on.

Simultaneous bus writes would have been very interesting to consider. However, this might have hurt the simplicity of the protocol since multiple writes probably need some topology knowledge and we have to somehow deal with self-interference.

Another mention in the paper was that when traffic is saturated, we could use external storage. If the traffic is very bursty, the scheduler might want to take into consideration that some nodes need to use the storage, while others could wait. Maybe we should formulate fairness differently in this case.

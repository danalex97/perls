# [pFabric](https://web.stanford.edu/~skatti/pubs/sigcomm13-pfabric.pdf)

### Paper summary
pFabric is data center transport design which decouples rate control and flow scheduling. The system uses an approximation of SRPT, ordering the packets based on a packet priority which is ideally set as the remaining flow size. The highest priority packet is scheduled when a port is idle, while the lowest priority packet is dropped if the queue overflows. Rate control does additive increase and resets the window at timeouts. The algorithm achieves low average flow completion times for simulations of spine-leaf topologies. Finally, the paper offers a flow priority assignment methodology for current routers to approximate pFabric.

### Key insight(s)
-SRPT is a 2-approximation of the optimal flow allocation that minimizes the FCT in the big switch model.

-pFabric offers similar guarantees to SRPT as long as at each switch port one of the highest priority packets is always available. A packet can be dropped as long as the queue takes more than an RTT to drain, supposing the host retransmits the packet.

-pFabric allows scheduling based on deadlines and flow sizes.

-Starvation can be used by up-capping the usage of the algorithm for big size flows.

-The algorithm can be approximated without changing the hardware by setting good thresholds for priorities based on flow sizes.

### What could be improved?
One of my concerns about this paper is about the deployment feasibility since it requires a completely new hardware for switches. Moreover, the incremental deployment optimizes the thresholds using the given workload, making the approach less generalizable. More research can be done on changing the thresholds dynamically, not based on a single workload distribution.

Another missed point from my point of view is not discussing the size of the packets in the algorithm for dropping packets. Dropping a packet of 1500bytes is not same as dropping a 20bytes packet.

pFabric also does not support streams and the paper suggests using a hierarchical approach to solve this problem: split the traffic then apply pFabric approach only on some of the traffic. How does this work in terms of hardware? How much of the data center has to get pFabric switches as opposed to usual ones?

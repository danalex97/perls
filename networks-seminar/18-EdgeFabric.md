# [EdgeFabric](https://research.fb.com/wp-content/uploads/2017/08/sigcomm17-final177-2billion.pdf)

### Paper summary
Edge Fabric is Facebook's SDN-based system for establishing peer and transit connections at egress traffic. Edge Fabric overcomes the problems of BGP by reacting to additional information such as current traffic rates and by using alternating paths for avoiding congestion. Aiming for ease of deployment, EdgeFabric injects selected routes via BGP by using a controller which overrides either the destination or traffic class for a packet. The decisions are made separately for each PoP and the solution achieves good results since it experiences under 0.1% packet drops during traffic redirection and manages to keep the desired link utilization within a margin of 2% error for more than 70% of the traffic.

### Key insight(s)
- The traffic demand cannot be served completely by private peers and the capacity of a link is variable due to the different traffic pattern.

- The paper points out the problems of BGP: lack of capacity and performance awareness.  

- Edge Fabric operates at PoP level, Facebook having a global algorithm used for load balancing operating independently of Edge Fabric.

- A PoP's central controller is used to override the BGP decisions by using the local_pref BGP parameter for assigning individual links and the DSCP IP6 field for providing alternating paths for different classes of traffic.

- Edge Fabric can be easily deployed due to running only using BGP at the router level, while the controller practically creates a software-defined network.

### What could be improved?
I like the fact that the paper treats in details the infrastructure and that most of the evaluation is easy to follow. Moreover, the design principles behind the implementation are clearly stated. However, I did not particularly enjoy reading the paper probably due to the overall structure: I felt that the paper would go into details very often, making it harder to follow.

The part that I do not like about the evaluation is the fact that the paper only compares the solution with BGP and not, for example, Expresso. I suspect that beating BGP is not very hard in this setting. Related to this topic, are there any limitations in Edge Fabric's granularity? (i.e. destination and priority class)

Some things that might have been interesting for me would have been some evaluation on how the global load balancer affects Edge Fabric and some cost evaluations: maybe is more cost-effective to just add more capacity/more private peers.

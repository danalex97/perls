# [Why the Internet only just works](http://www0.cs.ucl.ac.uk/staff/m.handley/papers/only-just-works.pdf)

### Paper summary

The paper describes the state of the internet in 2006, showing that the Internet protocols have not changed for the past decades even though the infrastructure and number of users has been growing fast. Past scaling challenges such as moving away from `hosts.txt` to DNS or moving from link-state routing to multi-level routing put in evidence the fact that the Internet ecosystem was rather reactive than proactive. Finally, the author looks into future challenges(e.g. spam and security short-term, congestion control in mid-term) and shows examples of temporary solutions that stuck around(e.g. BGP, NATs).

### Key insight(s)

- The paper shows past examples of scale problems and their solutions: for example ARPANET's `hosts.txt` was replaced with DNS, distance-vector routing was replaced with link-state routing, policy state routing was introduces to cope with larger number of service providers and CIDR classes appeared to handle the increasing number of hosts.

- The 'ossification' of some parts of the Internet is highlighted. Since '93, the network layer did no change much with the exception of adoption of MLPS(label-based packet forwarding) and VPNs, but many initiatives such as adoption of IPv4 QoS extensions failed.

- This problems are argued to come partly from the stakeholders not being open to new protocols: an examples is the vicious cycles in stakeholders' behavior - developers don't what to use a non-end-to-end solution, then vendors don't implement it as a consequence, so NATs and Firewalls don't support the new protocol since it's not common enough, making it not usable for developers.

- Short-term concerns of the author are spam, security, DoS, deployments(due to NATs and FWs), while longer term concerns are address space depletion, congestion control and inter-domain routing.

### Reflection

The paper presents problems of the Internet which are still current today: we don't have a better congestion control than TCP, spam, security, DoS remain pressing concerns, while there have been taken steps in improvement of inter-WAN algorithms(for example software-defined networks) and address space depletion(adoption of IPv6).

BGP remains still hard to replace today, being the only algorithm that enable policy routing, even though it has a series of problems:
 - does not take into account demand, capacity, performance of the links
 - slow convergence after failures(no AS knows which routes will be filtered by other ASes since no policy information is propagated to other ASes)
 - simple to infer customer-provider relations information from BGP path information
However, many inter-WAN and edge routing workarounds are employed today, such as Facebook's EdgeFabric(edge routers on top of BGP that override its decision) or Google's Expresso(label-based forwarding and SDNs) and B4.

Today's applications grow on top of the Internet stack, making the old infrastructure hard to change, making the vicious cycle described in the paper still relevant. Finally, I think the TCP criticism remain current: fairness problems, slow flow convergence and rather poor utilization due to use of a reactive state machine.

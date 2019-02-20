# [ShareBackup](https://www.cs.rice.edu/~eugeneng/papers/SIGCOMM18.pdf)

### Paper summary
ShareBackup shows how a data center can support fast and transparent failure recovery using backup switches and circuit switches. The main idea of the paper is repairing link failures instantly instead of making do with a crippled network. The paper shows how to effectively adapt a fat-tree topology by adding backup switches, circuit switches and a low-cost out-of-band control plane for controlling them. Moreover, the system allows offline diagnosis and incremental deployment, proving a cost-efficient solution for increasing data center availability.

### Key insight(s)
- When a switch failure happens, the control plane replaces the switch by modifying the connections in the circuit switch. When a link failure happens, the switches at both ends are replaced directly.

- A backup switch is added in each failure group at core, aggregation and edge layers. At the core layer, the core switches are split into multiple strips for creating a failure group.

- The control plane detects failures via heartbeat messages. The network controllers are deployed per failure group with out-of-band and low-cost hardware.

- Offline auto-diagnosis is performed by using backup switches to diagnose links. The switches that are still functional will become new backup switches.

- The system uses live impersonation by modifying the VLAN ID in packets when the backup switch takes over. Each switch preloads the routing table in order for each switch to be able to take over when needed.

- Some of the control plane failures are treated via shadow controllers(controller hard failures), fallback to traditional rerouting(link soft failures) and human intervention(controller link hard failures). The rest of failures are handled implicitly.

### What could be improved?
I feel like the paper is thoroughly motivated and detailed, but it lacks focus on the cost-effectiveness of the solution. When the 6.7% cost estimation is made, there are no clear explanations of the number of backup routers, the control plane hardware, and control plane backup hardware.

The paper is also valuable from the perspective of diagnosis: the solution actually notifies humans when intervention is needed and is able to differentiate between the types of failures. However, I would have linked a section on evaluation of auto-diagnosis. For example, to auto-diagnose a link we need at least 2 backup switches on both parts of the connection. A theoretical analysis of how the number of backup switches affects the auto-diagnosis accuracy would have been interesting.

Another part of the evaluation that I feel it was missing is the analysis of failures in the control plane and circuit switches. On some level, this is understandable since most of the control plane failures are handled directly and the rest are improbable(e.g. hard failure of a circuit switch).

I am not sure how impactful are failures on the application level. (4.2x seems a bit far-fetched) Aggregation-level failures are not so impactful. Edge-level failures are not so expensive when we use data flows with fewer dependencies(e.g. TPC-H benchmark). I assume that the data flows with heavier dependencies are not time-sensitive, they would probably analytics jobs.

In my opinion, deployments should probably be made only at edge switches and should require a thorough cost analysis. Moreover, I think that for applications with deadlines the solution makes a lot of sense and should be cheap. A hybrid deployment could group the deadline applications in a part of the DC topology and backup switches could be used only there.

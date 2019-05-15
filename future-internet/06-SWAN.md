# Paper summary <br> [SWAN](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/swan-sigcomm13.pdf)

#### Summary

SWAN is a system that boosts utilization of inter-DC networks by centrally controlled traffic and frequent traffic re-configurations.

#### Traffic patterns and Motivation

We have 3 service types:
  - interactive: in user's critical path
  - elastic: within seconds/minutes(e.g. replicating data updates)
  - background: maintenance and provisioning activities

MPLS TE show problems in terms of efficiency:
  - services can send however much traffic they want
  - resource allocation is inefficient(typically 30-40% utilization)

#### Architecture

- SWAN Controller: aggregates traffic demands from hosts and network configurations from routers
- Hosts: receive rate allocations from the Controller
- Switches: receive new network configurations from the Controller

### Service allocations

SWAN allocates the one class of traffic after the other from the more sensitive to the less sensitive traffic. The algorithm maximizes utilization by keeping a α-approximation of max-min fairness(maximize the minimum share of which the demand is not met).

Inputs:
```
	d[i] = demand of flow i
	w[j] = weight of tunnel j(e.g. latency)
	c[l] = capacity of link l
	s[P] = scratch capacity([0, 50%]) for traffic class P
	I[j,l] = 1 if tunnel j uses link l and 0 otherwise
```

Outputs:
```
	b[i] = allocation to flow i
	b[i, j] = allocation of flow i over tunnel j
```

Algorithm:

```python
for k := 1, 2, 3,...
	lb := 2 ** (k-1) * U
	ub := 2 ** k * U
	for b[i] in MFC(P, rem_c lb, ub, F):
		if i not in F and b[i] < min(d[i], ub):
			F = F + {i}
			f[i] = b[i] # flow saturated
```

```python
def MFC(P, c_rem, lb, ub, F):
	# maximize overall throughput, prefer short paths
	max sum(b[i]) - Ɛ * sum(w[j] * b[i][j])
	s.t.
		# bound the capacities allocated at this step
		lb <= b[i] <= min(d[i], ub)
			for i not in F
		# keep the already allocated flows
		b[i] = f[i]
			for i in F
		# don't use the scratch capacity
		sum(b[i][j] * I[j][l]) <= min(c_rem[l], (1 - s[P]) * c[l])
			for all l
		b[i][j] >= 0
			for all (i, j)
```

The proof for α-approximation of max-min fairness is based on the intuition that maximal unfairness for flows frozen in each epoch is bounded. This is intuitive since we bound the flows frozen in each epoch by the lower and upper bounds -- check [this](https://www.microsoft.com/en-us/research/uploads/prod/2013/08/Achieving-High-Utilization-with-Software-Driven-WAN.pdf).

### Congestion-free updates

We devise a multi-stage congestion-free transmission plan made of independent changes per stage. We leave headroom between s [0, 0.5] and we can finish the upates in `ceil(1/s) - 1` steps.

Moreover, the background traffic will have bounded congestion, while the non-background traffic will have no congestion.

### Limited switch rules

- Calculate initial allocation
- Select tunnels by smallest latency
- Rerun LP with chosen tunnels

#### Failure resilience

- Each component has standby replicas.
- If a router fails, the topology around the router will be expanded.

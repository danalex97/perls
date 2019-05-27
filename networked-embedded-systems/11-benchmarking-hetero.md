# [Network Dynamics Analysis and Benchmarking on an Outdoor Heterogeneous Wireless Sensor Network](https://www.researchgate.net/publication/328548795_Network_Dynamics_Analysis_and_Benchmarking_on_an_Outdoor_Heterogeneous_Wireless_Sensor_Network)

#### Summary

The paper presents an empirical study on network dynamics in an outdoor heterogeneous multi-hop WSN deployment for long-term environmental monitoring.

#### Paper strengths

Composing benchmark profiles for real-world deployment of a heterogeneous network is a nice deliverable.

Routing topology dynamics in long-term operation in real-world environments seems hard to study, hence I agree that studying this on CTP and RPL(and in general for routing protocols) is a nice addition to have and provides more applicable results.

The dataset is publicly available.

They do data cleaning and fill the missing paths at each collection cycle due to packet loss. The method of adding missing links by maximizing link entropy per cycle makes sense in this scenario.

Nice insight that we can tune the link PRR estimation for CTP.

#### Paper weaknesses
The paper seems to point out a lot of times things that one would expect, even without the empirical data they collected: e.g. link characteristics in heterogeneous environments differ from homogeneous environments, more powerful nodes have least link symmetry, etc.

Similarly, the main insights do not surprise me much. But I would say that the formulation is a bit unfortunate: "asymmetric links are the majority in heterogeneous networks" -- this really depends on the deployment and environment.

CTP+ERR is not really introduced. I was familiar with CTP, but I would have liked a short introduction.

One result that surprised me a bit was that 68% percent of the links are used for less than 100 times. I would have liked more details on why this happens and what is the spatial distribution of these links.

I would have liked to see insight from both spatial and temporal characteristics. If the number of link decreases, do all decrease in the same place? Does the network get partitioned? etc.

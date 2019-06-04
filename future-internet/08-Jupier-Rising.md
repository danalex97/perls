# Paper summary <br> [Jupiter Rising](https://conferences.sigcomm.org/sigcomm/2015/pdf/papers/p183.pdf)

### Design principles

- clos topologies
- merchant silicon
- centralized control protocols

### Network Evolution

Initially, Google DC was made of 4 routers connecting all ToRs in a cluster.

All the topologies we discuss are clos with:
  - different aggregation and spine blocks
  - different physical layouts

The paper presents the following deployments:

- Firehose 1.0
  - minuses:
    - switching fabric integrated with servers → servers fail too often
	- low radix of ToR switch
- Firehose 1.1
  - plus:
    - dedicated hardware to house switch chips
	- separate chassis to keep the switches
  - minus:
    - copper cabling expensive and hard to manage
- Watchtower
  - plus:
	 - less cabling by **chassis with backplane** and **cable bundles** between clusters
	 - reduce cost by **depopulating the optical fabric** where clusters have smaller demands
- Saturn - add more ports
- Jupiter
  - **middle blocks** - collocate multiple chassis on the same rack and fully connect them
  - multiple middle blocks make an aggregation block
  - spine blocks designed in a rack made of multiple chassis

### External connectivity

- Firehose 1.1 was initially deployed as a bag-on-the-side cluster(i.e. each ToR connected to both cluster routers and Firehose fabric)
- the cluster routers were decommissioned by connecting the fabric directly to external services via an aggregation block connected to external services
- inter-cluster networking via a hierarchy of iBGP routers(clusters in same facility) and eBGP routers(with both BGP protocols to connect the facilities and peer to external ASes)

### Software control

- Routing via Firepath for Firebase and Saturn:
   - each ToR is a layer 2 subnet
   - centralized state topology distribution: link state database distributed by a master out-of-band
   - distributed forwarding table computation: shortest path via ECMP
   - border routers use BGP

- for configuration of the switches, a single monolithic configuration is sent and all switches select their relevant part

# [Web Tracking](http://laoutaris.info/wp-content/uploads/2018/09/imc18.pdf)

### Paper summary
The paper shows a novel measurement methodology for mapping the geographic characteristics of tracking flows at scale. Real tracking flows are identified via a browser extension. The extension classifies the traffic, collects IPs for the tracker and DNS services and uses RIPE Atlas infrastructure to detect geolocation information. The measurement methodology is used to quantifying the percentage of tracking flows that terminate within national or regional borders. The paper also discusses the effects of DNS redirection and PoP mirroring on traffic locality by using a series of what-if experiments on the collected traces.

### Key insight(s)
- Tracking flows cross data protection borders.

- A browser extension deployed on volunteers' browsers is used to collect real tracking flows, as opposed to using crawlers.

- Trackers can be identified using lists used by ad-blockers and classifying non-tracking flows using heuristics(e.g. check referrer, URL, etc.)

- IPs are identified via passive DNS replication.

- Geolocation is done efficiently using the RIPE Atlas infrastructure. The accuracy in Europe is higher due to the big number of probe boxes in RIPE Atlas.

- The traffic confinement is significantly improved via DNS redirection at both country and continent level. This is a viable solution due to the small costs.

- The study on PoP mirroring shows a correlation between
the density level of IT infrastructure of a country and the level of traffic confinement.

###What could be improved?
The paper is quite dry in my opinion. I would have liked more emphasis on how RIPE is used for geolocation and a broad comparison between it and commercial geolocation databases. Does it make sense to extend current geolocation databases using the RIPE infrastructure?

Why do we use a passive extension rather than an active one? In my opinion, the extension could have also acted as a crawler to generate different data traces for comparison with the user-based ones.

Can we make the system more scalable by deploying crawlers similarly to how Akamai deploys CDNs? Moreover, we could try to make the crawler traffic more natural by using some page ranking algorithms or by generating synthetic data using the traces collected by the extension.

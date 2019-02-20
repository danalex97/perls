# [LLPD](https://dl.acm.org/authorize.cfm?key=N666831)

### Paper summary
The paper presents a traffic analysis attack against encrypted streaming traffic over HTTPS with MPEG-DASH. The attack is based on the fact that the content of a video generates variable bit rate patterns, patterns that can be observed from burst sizes.

The traffic can be classified by using DDNs due to their robustness against noise and different network characteristics. Practical on-path and off-path attacks are presented. The off-path attacks can be performed due to the correlation between artificially induced delays and traffic burst sizes. The attack is efficient since direct mitigation of the problem results in poor streaming quality.

### Key insight(s)
- MPEG-DASH traffic causes traffic bursts due to the transmission of the videos in segments of variable sizes.

- DNNs can be used to classify traffic due to their robustness against noise and different network characteristics. Moreover, the DNNs can make abstraction of protocol-specific attributes(e.g. TCP, QUIC).

- Accurate results can be produces using only the burst sizes.

- The attack can be performed off-path by making use of the fact that we can induce artificial delays in the streaming traffic by congesting the network. Therefore, the attack can be performed both cross-channel and cross-site.

- Direct mitigation by adjusting streaming parameters results in poor QoE. Detecting the off-path attack is possible by a MitM(e.g. router, ISP, proxy, etc.). The on-path attack is virtually undetectable since it is passive.

### What could be improved?
The paper a very exciting area and contains a large number of details and clear evaluation. It shows practical on-path and off-path attacks and presents the CNN section at a high level. The mitigation discussion, on the other hand, is too succinct.

The mitigation of noise for the cross-channel attack is not ideal in the case of multiple people sharing the connection. It is not clear if the attack can distinguish between two streams running at the same time. Moreover, filtering other busty traffic seems very hard for me(e.g. what if the person is downloading a torrent at the same time).

Another issue not in the scope of the paper is how to scale the approach on classifying a large number of videos. For example, Youtube has a tremendous amount of videos, compared to Netflix. Therefore, is really hard to guess what kind of traffic is out there. Maybe a dummy solution is classifying the most popular content, e.g. the trending videos. Moreover, the fingerprint of the device might be used to get information on age and gender, reducing the search space.

As further work, the idea of analyzing traffic bursts can be probably applied to IoT and Wireless traffic as well. As an example for IoT, a cross-channel attacker could classify events detected in a camera surveillance system. For the wireless domain, the same idea can be probably applied to traffic that is easy to observe. LoRa provides easy to observe traffic since the number of towers used for this specific spectrum is quite small and the range of devices is large. By observing the traffic bursts, if the attacker has some knowledge on the deployed application, the types of events could be classified from the encrypted traffic. A practical example is an attacker that could find information about the events happening in a deposit monitored wirelessly by a company such as Ocado or Amazon.

One of the applications of this paper can also be detecting pirate traffic by the ISPs. A middlebox can perform this kind of attack against encrypted traffic originating from different domains than the original host of the content. The attack will be undetectable since the middlebox is on-path.

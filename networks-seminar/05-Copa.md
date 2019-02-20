# [Copa](https://www.usenix.org/system/files/conference/nsdi18/nsdi18-arun.pdf)

### Paper summary
Copa is a congestion control algorithm that uses queueing delay estimations to adjust the congestion window size. Furthermore, it detects buffer filling by other protocols, becoming more aggressive to achieve more bandwidth.

The transmission rate adjustment is done by defining a throughput-delay utility function and looking for the Nash equilibrium point. The window size is modified towards the desired size using a velocity parameter for speedup. The algorithm works particularly well in sharing the connection fairly and obtains a good report between throughput and queueing delay in wired, cellular and satellite links.

### Key insight(s)
- The main assumption for calculating the Nash equilibrium point is that the packet arrival at the bottleneck link follows a Poisson process.

- Queueing delay is calculated using RTT measurements. The smallest RTT over the current window size is used to reduce the noise in measurements, while the minimum RTT over a longer period of time is a good estimation for the propagation delay.

- The window size is modified based on a velocity which increases exponentially as the size adjustment is done in the right direction.

- The steady state is characterized by the queue delay getting close to 0 periodically. This allows for exact propagation delay measurements and detection of loss-based competitors on the network.

### What could be improved?
In my opinion, the paper is valuable from multiple perspectives: the theoretical model is plausible and well explained, the queueing delay computation is exact(hence the good performance in cellular and satellite networks) and the detection of other types of congestion control algorithms is an original idea.

In the evaluation section, I would have also liked to see a deployment of PCC and BBR together with Copa. The way in which the delta parameter has to be changed in order to fit a certain type of congestion algorithm is unclear to me. Is there a way to do this automatically?

The algorithm is evaluated only in default mode(delta = 0.5). A discussion on the delta factor would have also been interesting.

Performance of Copa is also affected if the queue is not empty for a few RTTs. What is the effect of allowing a bigger error margin when switching to competitive mode?(at the moment this is 0.1 * (rtt_max - rtt_min)) What is the effect of waiting before switching? (e.g. wait for 5 more RTTs before switching to competitive mode)

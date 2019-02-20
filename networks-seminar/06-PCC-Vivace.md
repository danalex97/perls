# [PCC Vivace](https://www.usenix.org/system/files/conference/nsdi18/nsdi18-dong.pdf)

### Paper summary
PCC Vivace is an improvement on top of the PCC framework of congestion control schemes. PCC treats the network as a black box, making decisions about the sending rate based on utility function associated with the metrics measured in the network. The novelty which comes together with PCC Vivace mainly in the special properties of the chosen utility function and the control algorithm.

The chosen utility function guarantees convergence and is latency aware. The rate control uses gradient ascent in order to achieve faster conversion than PCC. Moreover, the utility function allows the protocol to adapt in presence of competition; Vivace looks at loss in case the latency variation is constant. The evaluation results are impressive: better median throughput in the wild, sensitivity to latency, good on satellite links, better than TCP on congested networks.

### Key insight(s)
- PCC Vivace is based on a black box model and the utility function plays a central role.

- The utility function rewards throughput and penalizes loss and latency.

- The utility function can be tuned to achieve several properties: strict concavity(guaranteed convergence point), no latency inflation, bounded ratio loss tolerance.

- Rate control is done using gradient ascent. The steps are increased when guesses are correct.

- In a heterogeneous setting, the loss function parameter can be used to handle resource allocation.


### What could be improved?
The study focuses only on deployments over the internet. A discussion on data center applicability and evaluation would be interesting. In the same direction, looking at high bandwidth links would be also interesting.

Regarding the friendliness of the protocol, deployments together with BBR would be useful since QUIC already uses BBR. The algorithm seems also fit for background transport scenarios, for example, further research can try to improve Apple's LEDBAT or BitTorrent's uTP.

The only part of the paper that left me unconvinced is the interaction with other protocols. The competitiveness with TCP is treated shallowly in the paper, even though it should be one of the main points since the network settings presented are not focused on data center traffic.

# [RADWAN](https://www.microsoft.com/en-us/research/uploads/prod/2018/06/sigcomm18-final223.pdf)

### Paper summary

REDWAN is a WAN routing algorithm which takes into consideration the physical capabilities of optical fiber to transmit at higher SNR. The link capacities can be increased dynamically by using QPSK, 8-QAM or 16-QAM. The currently available hardware devices have a 1-minute downtime when changing the modulation scheme, so the algorithm for changing the modulation should be aware of the churn caused in the system by these changes. RADWAN uses a controller at the networking layer, also taking into consideration the current SNR levels in the optical topology and current flow allocations for the devices, producing flow allocations and hardware links reconfigurations.

### Key insight(s)
- The main idea of the paper is adapting link capacities in response to changes in signal to noise ratio.

- The gain in capacity and availability from dynamically changing the modulation scheme are significant.

- The network layer has to play along with the layer-1 devices since the time taken to reconfigure a link is significantly high. Moreover, changes in capacity would cause traffic reconfigurations(churn).

- The traffic engineering optimization problem becomes both maximizing throughputs, but also minimizing churn. In order to account for the aggressiveness of the algorithm, we can tune how important is minimizing churn.

- Even better results could be obtained by modifying the existing hardware.

### What could be improved?
The paper was well-structured and easy to follow in my opinion. The idea is quite intuitive and the solution is easy to implement(in theory). I am quite curious why the idea has emerged only now since wireless has been using adaptive rates for years?

From what I understood, changing the rate faster than in 1 minute is a limitation of the hardware. Why don't we use, for example, a circuit switch and multiple BVT modules which transmit with different modulation schemes?

Another interesting thing is that forward error connection is mentioned only once. However, even if this is less efficient in wired environment, it might be useful to consider if the SNR doesn't decrease significantly.

Finally, I would have liked a discussion on how conservative the report between churn and bandwidth should be. Maybe some evaluation in this direction would be interesting as well.

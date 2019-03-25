# [Passive-ZigBee: Enabling ZigBee Communication in IoT Networks with 1000X+ Less Power Consumption](https://www.csee.umbc.edu/~zicheng1/publication/li-2018-pez-3274783-3274846/li-2018-pez-3274783-3274846.pdf)

### Summary

The paper presents a backscatter no-battery device that can transmit sensor data and replay WiFi data to ZigBee consumers, when combined with a special WiFi gateway.

### Paper strengths

The thing that I liked the most about this paper is the thorough background explanations. The paper showed very clearly how WiFi and ZigBee transmitters and receivers look like and the basic principles of backscattering.

The good high-level descriptions make the paper easy to follow. For example, take section 5.1 states we need to embed in subcarriers combination of ZigBee symbol states; similarly, section 6.2 states we need to combine the carrier signal with a signal that corresponds with the data we need to send.

The paper also goes into details in multiple points, which makes reading for an inexperienced person much easier: for example, the paper clearly shows how to perform dynamic frequency scaling.

The reasoning behind following a particular solution is motivated by some basic observations. For example, the design of a hybrid WiFi and ZigBee signal is possible due to symbol rates operating on different frequencies and 7 WiFi subcarriers overlapping over a ZigBee signal.

Motivation and applications for using backscattering are present in the introduction. Graphs in the evolution section are easy to interpret. Therefore, the overall structure and flow of the paper are quite good if you read it in multiple passes - especially if you don't have much background in the area.

### Paper weaknesses

The algorithm on the backscatter is not clearly explained. I think this would have been much more clear if the authors added some comments or reference lines of code in their explanation.

From what I understood the synchronization is done on the preamble at each received packet. The tag must have the knowledge from the hybrid packets symbol period. I do not understand why do we need any information in the preamble: isn't the symbol rate of the hybrid signal always the same?

When describing emulation of the ZigBee signal, I would have liked to have WeeBee introduced in few sentences.

When mapping subcarrier groups to symbols, we optimize the subcarrier weights by minimizing an error defined as the geometric mean of error vector magnitudes of WiFi and ZigBee. The choice of this function is somewhat intuitive, but I am not sure whether this choice can actually have an impact on performance. I would have liked some reasoning behind it.

The abstract is not very specific in my opinion. For example, the authors could have just stated they did a gateway and a backscatter that can transmit sensor data and replay WiFi data to ZigBee consumers.

Even though the evaluation graphs are clear and easy to interpret, the explanations are not very useful and sometimes do not match what happens on the graphs. Moreover, it is not linked with the applications described in the introduction. The paper would have been much more persuasive if they did an example application like an implanted sensor.

The paper seems somehow rushed, unfinished. I think it has potential, but there are explanations lacking in some parts, some words are misspelled, there is a typo in the algorithm listing, etc. I suspect the authors submitted quite late to the conference.

### Open questions and improvement

I am not sure how generalizable the approach is.  With what kind of modulations will this approach work? Can we do the exact same thing with BLE?

Adding a no-battery receiver also gives more capabilities. Does this allow for more complex applications?

From my understanding, the gateway created via the backscatter tag is one-way. Can we somehow get bidirectional communication? I think that one has to also consider CSMA/CA on ZigBee and WiFi when trying to approach this problem.

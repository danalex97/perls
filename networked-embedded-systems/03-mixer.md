# [Mixer: Efficient Many-to-All Broadcast in Dynamic Wireless Mesh Networks](https://nes-lab.org/pubs/2018-Herrmann-Mixer.pdf)

### Summary

This paper presents Mixer, a many-to-all broadcast primitive for dynamic wireless mesh networks. Mixer integrates random linear network coding(RLNC) with synchronous transmissions. It approaches the order-optimal scaling in the number of messages to be exchanged.

### Paper strengths

The main contribution of the paper is improving the time constant in many-to-all broadcast primitives by combining random linear network coding with synchronous slotted transmissions. The overall approach is interesting and the results provide big improvements over the state of the art.

The paper highlights the importance of topology in the performance of RLNC. They provide several improvements based on this, such as changing the probability of transmission based on local density and making the algorithm more deterministic in high-density regions. The intuition behind this improvement is clearly explained and the proposed solution is easy to implement.

Looking at where RLNC is slow in practice is a good approach to find places to improve the protocol. The paper, then, provides concrete improvements that can be done during startup and termination.

The protocol is generalizable to all physical layers where the capture effect is present. I think this is a big plus, along with the fact that the initial distribution of messages does not greatly affect the protocol's performance.

The paper is well-structured and its flow is natural. The examples given in the introduction are also fairly good. In particular, the trace of Mixer with 5 nodes exchanging 5 messages is useful to understand the general workflow of the protocol and the general goals of the paper.

The evaluation is clear and the metrics and test-bed configurations are clearly defined at the beginning of the section. The interpretation of the results is detailed and the graphics get the point across effectively.

### Paper weaknesses

One thing that bothered me is the fact that the paper presents 4 heuristic approaches to improve RLNC, but they are not evaluated separately. I think it is relevant/insightful to know how the distribution of the average rank increase looks after applying only some of the heuristics.

Another point that wasn't clear to me from the first readings is what the initial setting is. Of course, the paper mentions at the beginning that we leave to the other layers to make the distribution of the message known, but I would have liked to have everything clearly stated: e.g. we know N, M, what messages are at each node and in what order, etc.

I find the slot assignment for Adapted Coordination to be explained and argumented poorly in comparison with the other improvements. In particular, some statements like "it stimulates a fast wake-up" are left to the reader to interpret and some statements lack details: e.g. "assigning the owner role of slot k to the originator of message k during the first M slots".

I think that is also relevant for most of the improvements discussed to mention intuitively why the approach improves the status-quo. For example, the Improving Startup algorithm makes sense, but a clear example would have gotten the point across much more easily.

Finally, the paper does not rely on mathematical analysis too much. However, I would have liked to have such a discussion on some parts of the paper, even though I understand that this might just have been a biproduct of the space limitation.

### Open questions and improvement

The open question mentioned by the paper, namely determining distributions that encourage propagation based on the topology seems a good starting point for further research. One can, for example, discuss what distribution should be assigned based on how sparse a network is.

Another interesting point would be how to allow the number of messages transmitted in a round to be unknown. This might impact slot allocation as well.

Something also interesting to consider is asynchronous rounds or actually eliminating the round concept. This would imply that we still need to somehow bound the capacity of the number of equations that we process and we need to decide when to deliver a message. That is, if all my neighbors have a message, I don't really need it anymore.

Finally, making certain probabilistic guarantees would be very interesting and central for the application of Mixer.

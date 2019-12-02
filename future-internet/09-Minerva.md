# Paper Summary <br> [End-to-End Transport for Video QoE Fairness](https://mit.edu/papers/sigcomm13.pdf)

### Paper summary

Minerva aims to optimize video for QoE for multiple users in a fair way. It uses information about the player state and video characteristics to adjust its congestion control behavior to optimize for QoE fairness. Furthremore, Minerva tries to occupy only the fair share of the bottleneck link bandwidth, competing fairly with existing TCP traffic.

### Motivation

The main motivation of the work is that most ABR algorithms focus on optimizing video QoE for a single user. The problems of these approaches is that they are blind to QoE and to the dynamic state of the video client.

### Objective

QoE for a single chunk:
```
QoE(chunk, rebuf_time, prev_chunk) = P(chunk) - β * rebuf_time - γ * |P(chunk) - P(prev_chunk)|
```

where `P(e) = quality gained from watching a chunk at bitrate e`.

We optimize for `max min[ sum(QoE) / chunks]`, that is we want to maximize the minimum of the average per-chunk quality.

### Workflow

1. Client sends information regarding the video player state
2. Formulate local optimization problem server-side
3. Solve optimization problem server-side
4. Adjust the underlying trasport according to weights computed by optimization

Note Minerva only modifies the number of allocated flows, hence using any ABR and CC implementations. It uses QUIC with a persistent connection for each client.

### Utilitiy function

The utility function is formulated such that the original optimization problem reduces to `max min(U(rate))`. The update rule used for weights is `w = r / U(r)`. This gives the followins properties:
1. Fixed points keep the weights(i.e. optimums are fixed points)
2. Each iteration moves towards optimal values

The paper presents multiple utilty functions that get updated with similar rules as above. The utility function used in the evaluation takes into consideration the state of the DASH video client.

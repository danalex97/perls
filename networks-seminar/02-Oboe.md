# [Oboe](https://engineering.purdue.edu/~isl/papers/sigcomm18-final128.pdf)

### Paper summary
Oboe presents auto-tune techniques applicable to ABR algorithms, used to reduce algorithms' sensitivity to changing network conditions. Oboe focuses on throughput variability, basing its main idea on the assumption that the network connections are piecewise stationary.

Oboe has 2 phases: finds offline the best choice for parameters in the underlying ABR algorithm for a space of discrete stationary network states and detects online the current network state and fine-tunes the parameters of the ABR algorithm. The paper shows how to apply the algorithm to existing state-of-the-art models, evaluating the performance change on a testbed using existing network trace.


### Key insight(s)

Oboe works on top of ABR algorithms, dynamically adapting parameters at run-time for the current network conditions. The separation between online and offline work allows fine-grained quantization of the throughput variability space. The algorithm is stable during the online phase due to point detection and searching for the most cautious configuration around a particular mean and std. Oboe is applicable to a large range of state-of-the-art ABR algorithms, such as BOLA and MPC, but the application is different from model to model. Its architecture allows the reuse of most of its components(e.g. change detector, reconfiguration engine, player simulator).


### What could be improved?

The paper compares thoroughly the algorithm with other approaches, but it does not evaluate its own fine-tuning. For example, there is no evaluation for the effect of the granularity in the mean-std throughput space. Moreover, the discussion is limited to the throughput-based fine-tuning; we could fine-tune the ABR algorithms based on previous download times and sizes of the next chunks.

On the same note, the reasoning behind the online heuristic of choosing the most stable parameters from the r-radius range is not fully explained. Who do we choose linear spaces for both mean and std dimensions? Why do we search in a circle and not use any other distance metric?

In the evaluation, the reduced number of rebuffers seems the most important result. In my opinion, the paper offers no insight on where this result emerges from.

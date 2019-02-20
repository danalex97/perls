# [AWStream](https://ptolemy.berkeley.edu/publications/papers/18/ZhangEtAl_AWStream_SIGCOMM_18.pdf)


### Paper summary
AWStream is a stream processing system for analytics in WAN. It addresses the problem of scarce and variable bandwidth, offering the developer an intuitive API. AWStream models the fidelity-freshness report by allowing the user to define an accuracy function to describe the fidelity. Once the user provides in code knobs for possible quality degradation, offline profiling is employed to find all Pareto-optimal (accuracy, bandwidth) pairs.

At runtime, the traffic rates are decreased on congestion and smoothly increased via probing and monitoring of queue messages. The probes are made of raw stream data which is used to online improvements of the application profiles. The system works well under changing network conditions, proving small latencies at significant accuracy rates.


### Key insight(s)
- The developer primitives do not require domain-specific knowledge for usage since the given knobs are only suggestions rather than policies.

- The programming framework is generalizable as data, knobs and accuracy metrics are all provided by the user.

- Profiling offline is done at deployment based on user-provided traces.

- The paper shows a way to usefully combine smooth traffic increase via probing with online profiling.

- The online profile is improved by sampling only the Pareto-optimal profiles until the difference between models is significant. (case in which a full space search is done)

- The paper introduces the notion of accuracy-based fairness, as opposed to utility-based schemes.

### What could be improved?
There is not much discussion on the user-provided data. The user supplies the training data traces. What impact does the trace size have on offline profiling? How much training data do we need? On the same topic, the user-supplied knobs can produce differently shaped profile spaces. Does the system benefit from a larger number of knobs or does it just cause unneeded computation?

Another interesting problem is how much additional bandwidth is needed to run the online algorithm. I would have also liked to see the comparison with other systems ran on a more bursty bandwidth traffic since the paper notes that WAN bandwidth shows high variability.

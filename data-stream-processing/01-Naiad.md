# [Naiad: A Timely Dataflow System](http://sigops.org/s/conferences/sosp/2013/papers/p439-murray.pdf)

### Paper summary

Naiad is a distributed system for executing data parallel,cyclic dataflow programs. It aims to provide iterative processing on real-time data streams, support for iterative queries and a fresh, consistent view of the results.

The computation model is described by stateful vertices connected in a DAG of feedback loops that receive notification for changing the epoch of computation. External sources timestamp messages with an epoch and notify the vertices when the computation is done in a pull-based manner. Each vertex sets up callbacks on message receipt and subscribes to notification that [roughly](https://github.com/danalex97/rust-examples/tree/master/timely_tutorial) fix the end of an epoch.

The control plane propagates capabilities established through notification and information regarding the graph structure. Using this information it is able to establish safety properties together with computation progress. The system achieves low latency by using the mechanism aforementioned and by grouping multiple handlers onto the same worker.

### Key insight(s)

- To ensure the safety of computation in the control plane capabilities are used as follows: once a notification with timestamp t is received, a node has the guarantee that its neighbor will not produce more data with the associated time smaller than t. Each timestamp is defined by an epoch number and counters associated with each feedback loop.

- Since each timestamp defines a partial ordering, we need to track the composition of the workflows(graph) since we don't what a node to be able to arrive from a time-location pair (t, l) to a pair (t2, l2) s.t. (t2, l2) < (t, l).

- To make the control plane protocol more efficient each node keeps a partial view of the graph and capabilities rather than a full view. The state is shared via broadcasts to FIFO delivery queues. This means that an arbitrary point in time, each worker has seen an arbitrary prefix of the sequence of progress made in the system by each worker, thus keeping a more "conservative" view of the progress made so far. The paper describes also how to add a central component to the control plane.

- The data plane partitions the logic vertices onto more workers. The data can travel either on local or HTTP channels(in case of a shuffle). Locality is maintained by keeping state on each vertex and by placing multiple vertices onto the same worker.

- Limited fault tolerance is achieved by periodic checkpoints. The system chooses to gain performance by doing less state saves during the computation and losing availability in events of a failure.

- To gain performance Naiad modifies TCP standard parameters and uses single-threaded nodes with concurrent queues and lightweight spinlocks with small granularity.

### What could be improved?

The paper results are fairly convincing and the general framework of computation is well argumented and explained. However, the failure discussion is short and provides no practical experiments. Some mentions of fail-over plans would have been welcome: for example, if a worker fails, what happens with a loop? Similarly, if a worker handling a part of a stream fails, what happens with the new incoming requests?

Separately, only micro-stragglers are mentioned, whereas the problem of straggler vertices is not mentioned at all. Even though this can be solved at higher levels, by speculative executing, for example, the problem could have been at least addressed. On the same line of taught rate limitation is not mentioned at all. Within a loop at each epoch a larger neighborhood of a vertex may be affected by an 'avalanche' of messages; is this left to the developer?  

Finally, I am not sure about the argument that speculative work is too expensive. What about providing each piece of data with an unique ID and just discarding duplicated messages with the same timestamp at the next node? This basically would allow 2 vertices on 2 workers to act exactly as the same virtual vertex if they are identified in a similar way. If the computation carried out by the vertex is deterministic, then we only need to solve the problem of double messages at the receiver.

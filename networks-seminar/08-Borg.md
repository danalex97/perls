# [Borg](https://pdos.csail.mit.edu/6.824/papers/borg.pdf)

### Paper summary
Borg system is a cluster manager designed for large-scale(100,000s of jobs, 1,000s of apps, 10,000s of machines). From the user perspective, Borg splits the workloads in prod and non-prod jobs, favoring the prod. It operates on large groups of nodes(cells), allowing large computation clients. Architecturally, it is based on a master-slave architecture. It emphasizes reliability over efficiency via master replication, overallocation for prod tasks and failure containment via limiting cell sizes. For efficiency, the overallocated capacity of prod jobs is reclaimed by non-prod jobs, saving up to 20% computational power.

### Key insight(s)
- Borg has a master-slave architecture with Borgmasters handling allocation and pooling clients for their state.

- Scheduling is done at Borgmasters via building a "large enough" set of feasible machines and allocating them via a scoring mechanism.

- The cell compaction metric measures how small a cell can be horizontally in order to satisfy the same resource needs. It is used for scoring and resource reclaiming.

- The Borgmaster achieves availability via multiple replicas and consistency via persisted Paxos-backed transactions.

- Borglets react to overuse of uncompressible resources by killing low priority jobs and reclaiming their resources.

- Cell sharing proves to provide less CPU overhead than the gains resulted from better resource allocation.

- Fine-grained resource allocation reduces resource fragmentation.

- Resource reclamation for non-prod tasks is done via the Borglet predicting usage and the scheduler reclaiming the remaining resources non-aggressively.

### What could be improved?
The paper feels less systematic in the discussion of design issues compared to the usual systems paper. It describes how Borg arrived at the current state, more as a reaction to initial design flaws, corrections being made in an informed way from experiments.

The authors should focus more on the utilization section since is the most original part. The problems on scalability and availability are interesting, but nevertheless, do no bring something new.

The resource request granularity is discussed independently of resource reclamation. The resource reclamation algorithm used has some impact on request granularity, so further discussions could be interesting. Could we apply the same strategy when providing fixed-size resources to cloud clients?

In comparison with Microsoft's Apollo, Borg uses simulations for scheduling. This results in large overheads while having smaller cells. How would using simpler scheduling on more fine-grained cells work?

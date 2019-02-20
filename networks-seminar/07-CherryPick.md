# [CherryPick](http://shivaram.org/publications/cherrypick-nsdi17.pdf)

### Paper summary
CherryPick is an automatic cloud configuration picker for recurring big data analytics jobs. In large lines, CherryPick chooses from a configuration represented by machine types and their number a configuration that offers good performance under cost constraints. CherryPick achieves low overhead and maintains accuracy by establishing configuration using Bayesian optimization techniques.

The model aims to be generalizable by adopting a black-box approach when looking at the data analytics application. The solution provides opportunities for user customization(by the choice of search stopping conditions) and takes into consideration data-center execution noise. CherryPick can find near-optimal configurations at the median and optimal configurations with a probability between 45-90\%.

###Key insight(s)
- The key idea behind CherryPick is searching for a suboptimal configuration where the best configurations are likely to be found.

- The workflow of CherryPick is: running a configuration, modeling cost and performance via the prior function, ranking the choice via the acquisition function, repeat.

- The Bayesian Optimization model is appropriate for the problem due to the small number of samples needed, the uncertainty model of the cloud and the modeling of the config space as a Gaussian process

- Noise in the cloud is treated as multiplicative due to the "domino effect" of bottlenecks in typical pipelines and accounted for appropriately.

- Starting points are chosen quasi-randomly in order to keep the algorithm from converging on local minimums.

### What could be improved?
Even though the solution is appropriate under the paper assumptions(Gaussian process configuration model, the noise multiplicative model, recurring jobs, etc.), it is not very clear for me who the actual end user is and what data does he look at. Is the data workflow constrained by deadlines? Can the workload be variable(and how variable)? Does the end-user have the capability to control the supplied workload?

Another concern of mine is that the whole experimental setup assumes homogeneous machines. A simple counterexample from practice is having an HDFS setup with different capability machines for NameNodes and DataNodes. Having different types of machines might make sense for the first point in the analytics pipeline.

The variable workload is mentioned, but not really taken into consideration at evaluation and the solution is briefly mentioned. This is controversial since not taking it into consideration assumes the capability of controlling the workflow. The workflow then can be regulated for a particular cluster setup.

Finally, the paper mentions that application-specific knowledge can be better used for establishing the prior function. This knowledge can, moreover, be used for establishing a better noise reduction strategy: e.g. a slow machine might affect differently a MapReduce job than a different type of job, potentially changing the noise distribution.

Application-specific knowledge can be assumed in multiple user setups as well: e.g. small companies probably have only a few types of data, whereas in a big company using different configurations for each type of data can result in big cost reduction.

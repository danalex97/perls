# [Chameleon](http://people.cs.uchicago.edu/~junchenj/docs/Chameleon_SIGCOMM_CameraReady.pdf)

### Paper summary
Chameleon is a system that picks suitable configurations for NN-based analytic pipelines. The problem addressed is the tradeoff between accuracy and computational resources. The key challenge in this regard is the large space of configurations and the insight behind Chameleon are temporal and spatial correlations.

The system reduces computational power by using cross-camera correlation, infrequent full-space profiling and reducing the search space via decomposing accuracy measurements for different knob components. The benefits of the system are found in both reducing the resource consumption and keeping accuracy high.

### Key insight(s)
- Chameleon has based the observations of characteristic persistence(good configurations tend to remain good), cross-camera correlation(for saving computational power) and configuration knobs independence on accuracy.

- The observations of monotonicity and independence of accuracy measurements for the space dimensions allow usage of techniques such as hill climbing.

- Full space searches frequency is reduced by choosing only the current best configurations in the time interval between full space searches.

- Using cross-camera correlation effectively distributes the resource consumption of comparing a configuration to the "golden" configuration.

### What could be improved?
The groups of cameras are established based on the correlation of data. What happens if the correlation breaks? (e.g. a traffic accident on a single road for traffic control, bad weather conditions)

An interesting research topic would be if the independence of search space dimensions can reduce the resource usage even more by only modifying the search space at the profiling window a single(or several) dimension at a time. For example, in the first window we would only recalibrate frame resolution, in the second one the framing sample rate, in the third one the detector model and so on.

Going in the same direction, further research can be done to find out if we can create a group of correlated cameras based on single knob dimensions. For example, two surveillance cameras might produce similar frame sample rate accuracy distributions, but their detection model has to be different due to the surrounding environment.

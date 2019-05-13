# [SnailTrail](https://www.usenix.org/node/211258)

### Paper Summary
After a thorough introduction to CPA and the PAG, the paper proposes a new model for critical path
analysis.  The authors consider only the events captured in a tumbling window at a time, defining the PAG
snapshot − the activities entirely within the time window are kept, while the boundaries are truncated − and transient critical path −
a path with the biggest length in the snapshot.

Once  these  new  metrics  are  defined,  one  of  the  main  insights  of  the  paper  is  that  an  activity  that
appears on many transient paths is more likely to appear onto a critical path, fact captured by the Critical Participation metric.

To prove the applicability of these notions, the paper presents the SnailTrail system which takes incoming streams of events from diverse systems(coming from custom instrumentation) and produces real-time
performance summaries.  SnailTrail computes the graph snapshot associated with a tumbling window and calculates the CP metric without the need of materialization.

Finally, the paper shows how to use the CP metric for discovering overheads, finding stragglers, tuning
operator parallelism and communication skew.  The overall conclusion from the experiments is that the CP
metric provides better insight into this problems compared to classical profiling, insight which comes at a
minimal cost of instrumentation.

### Comments and Criticism

The most interesting part of the paper for me was the definition and usage of the CP metric.  The idea
is original and intuitive and the comparison with existing methods puts that into light.  In particular, the
given examples in the sections get the idea across in an easy-to-understand way.

The  applicability  of  the  system  is  quite  large  and  the  classification  in  activity  types  is  broad.   The
summaries(activity, straggler,  operator, communication) are general and easy to understand. The system can identify different operator contributions clearly − this is shown well in the TensorFlow example.  This
makes the system practical and appropriate for profiling.

The  evaluation  is  generally  satisfactory:   the  instrumentation  overhead  is  acceptable  and  is  the  only
overhead due to the streaming approach, the performance keeps up with the stream speed, and the system
provides more insight compared to classical methods.  However, I was not sure how close the system is to the
optimal:  how many activities that have a big CP metric are actually on the critical path for a long-running
computation.

Regarding the evaluation, I have also missed the impact of different parameters on the accuracy of the
CP metric.  Does the length of a snapshot directly impact the accuracy of the metric?  Which window size
should a user choose?  Moreover, I would also like to know how good are the metrics that I can get with
smaller instrumentation overhead.  As a general observation, I think the paper does not look much into how
its own parameters affect the system overall −which is not necessarily a problem if this makes the paper more succinct/clear.

The  only  criticism  regarding  the  writing  style  is  the  over-mathematical  description  of  uncomplicated
notions.  These break the flow in the first read and I would personally move them to their separate section.
Moreover,  some  do  not  provide  any  additional  insight  and  are  easier  to  understand  phrased  directly  in
English.

The paper lacks a future work section as well.  I find the general idea of creating snapshots interesting and
I would like to think about how to solve the problem using different windowing mechanism.  Other interesting topics could be:  black-box instrumentation,  online operator parallelism modification and migration given
maximum resource allocations, and combining this system with elastic provisioning.

### Conclusion
Overall,  the  paper  shows  convincing  results  and  the  general  motivation,  trade-offs  and  contributions  are
well-defined.  It presents both theoretical and practical contributions and improves on the state-of-the art.
The only criticism is related minor aspects of the writing style and evaluation.  All in all, a nice paper.

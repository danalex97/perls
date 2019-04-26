# [InK: Reactive Kernel for Tiny Batteryless Sensors](http://josiahhester.com/cv/files/inksensys2018.pdf)

### Summary

The paper propses InK: a reactive kernel that provides a novel way to program energy-harvesting devices that operate intermittently. InK brings an event-driven paradigm shift for battery-less applications, introducing abstractions that enable reacting to changes in available energy and variations in sensing data, alongside task scheduling, while maintaining a consistent memory and sense of time.

### Paper strengths
The paper states clearly even from the abstract what are its goals and contributions. The introduction makes a clear problem statement, together with useful background information.

The subsection in challenges captures clearly what are the current problems with other systems, namely: the problems related to polling, the need for a resilient timing subsystem, risk of starvation and memory model limitations.

The execution model and task threads explanations are clear and well-motivated. I find the approach reasonable and the complementing memory model compelling. Task threads and double buffering make up a model easy to reason about.

The reactive execution discusses explains well why progress is enabled and how Ink manages to avoid data races between ISRs and task threads.

The experiments and performance are quite encouraging. The system manages to achieve proper reactive responses and misses the execution of a small number of priority threads. The authors also manage to explain why Mayfly dies fewer times than Ink.

The authors provide real-world event-driven applications and test usability with some developer. This shows nice proof-of-concept work and provides proof for the claim that Ink is easy to use.

### Paper weaknesses
The background and related work section reiterates a lot of the ideas in the introduction. I also feel that some explanations make the reader lose track of what we are interested in.

The introduction to section 3 creates some confusion since it enumerates some points that are addressed in the section in a different order. I think the authors should probably focus shortly summarizing what the reader should look for.

Different types of intermittent computing events are enumerated, but not put in context in section 3.1. For example, they mention an external device powered by a capacitor can keep track of time while MCU is down. They don't come back on this later at any point(or is hard to find where they come back on this).

Section 3.2 presents programming approaches for intermittent computing, scheduling policies, and preemption. I am not convinced by the argument they make against checkpointing. I imagine that division in tasks of their "task thread" could be done automatically, making the system even easier to program. The only problem would be too much granularity, but I am not entirely convinced by their argument.

The sections on reactive execution and timers could have given more details. In particular, the starvation reduction part was not very clear to me. Moreover, there are not many details on the external persistent timekeeper.


### Open questions and improvement
Firstly, regarding the paper, I would focus more on reducing out the redundant parts in the introduction and creating a section which shows a clear overview of the system.

Regarding the programming model, I wonder if it's possible to automatically divide code into tasks, keeping the same double buffer semantics. This would allow the user to reason without having to keep in mind tasks.

Their model seems to reduce race conditions and, at first sight, seems to be respecting borrow semantics outside the tasks. I wonder if this model is applicable in a more general setting in IoT since is not as restrictive as raw borrow rules and offers some nice guarantees about data races and allows checkpointing.

Another interesting idea about dynamic scheduling would be the usage of an external control plane(some IoT devices that have a battery) that can predict the power usage of the battery-less devices and change the priorities of the device threads dynamically.

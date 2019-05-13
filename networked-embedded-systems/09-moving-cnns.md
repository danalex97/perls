# [Moving Convolutional Neural Networks to Embedded Systems: the AlexNet and VGG-16 Case](https://dl.acm.org/citation.cfm?id=3207995)

### Summary

The paper moves AlexNet to embedded devices by using approximate computing techniques to reduce the computational load and memory occupation of the deep learning architecture by compromising accuracy with memory and computation.

### Paper strengths

The paper states from the beginning what it tries to do, and how it tries to do it: a methodology for design and porting of CNNs to embedded systems by approximation methods. Moreover, the contributions and motivation are clearly stated as well.

The methods described in section 3 are intuitive and easy to understand: via task dropping, we keep only a part of the CNN and by precision scaling, we reduce both the memory and computation footprint. The filter-selection mechanism in section 4 is also intuitive. These sections make the paper easy to follow.

The authors manage to move the approximations of AlexNet even on an embedded platform with 512 KB memory and a 167 MHz processor, which is fairly impressive.

The experimental results in section 5.1 seem reasonable and the results are explained by the authors as well.

Through the paper, the authors make nice observations while designing the approximation mechanisms: the hierarchy of features in the CNN may be sufficient enough for classification, searching for the optimal configurations on the Pareto boundary, etc. The paper is well-written in this aspect as the whole flow feels story-like.

In my opinion, the benchmark and data split they selected are good ones.

### Paper weaknesses

The part that I did not like about the paper was mostly bits of the evaluation section. Firstly, they only port AlexNet after in 5.1 we see that VGG does a bit worse when their approximations are applied.

They don't compare their solution with the literature mentioned in the survey or architectures designed for scaling(e.g. MxNet). Since they mention significant reductions in memory size for papers referenced in the survey, without comparison is hard to see how much they improve on the state of the art.

From what I understood, the improvement of cutting the last layers was ~10% when deploying, but what is the improvement if we also consider approximating the numbers to fewer decimals in their representation.

Another point that I missed was how much each mechanism for reducing energy influences the final results(in section 5.2). What would I get with only filter-selection, task dropping and precision scaling separately? How close are these configurations to the Pareto boundary?

The mention that the smaller computation footprint reduces energy: how much energy is reduced? How big is the execution time for the unaltered AlexNet in section 5.2.

Finally, I feel that the contributions they made are not necessarily novel, in the sense that their techniques have already been applied in the literature, but not having their application in mind(i.e. embedded systems). I would say though, their contribution is still significant.

### Open questions and improvement

Besides the criticism in evaluation, the work is interesting, nevertheless. I would also like to know how these approximations would affect RNNs and if that is viable.

Furthermore, rather than discarding a whole filter, I was wondering if we can prune all the connections that contribute to the next layer with near-zero values when computing the output of layer in the CNN. This "fast-kill" mechanism might reduce computation significantly depending on the picture that is given as a query.

The further work they mention in distributing the computation and/or offloading part of it is also a nice topic.

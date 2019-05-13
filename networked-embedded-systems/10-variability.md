# [Taming Performance Variability](https://www.usenix.org/system/files/osdi18-maricq.pdf)

### Summary

The paper looks at hardware variability in a dataset of more than 800 severs over a period of 9 months. The authors draw a number of lessons about the types and magnitudes of performance variability and the effects on confidence in experiment results. They create a statistical model that can be used to understand how representative an individual server is of the general population.

### Paper strengths

The first sections are informative and the authors describe well the prior work in parametric and nonparametric statistical methods for estimating variance.

The graphs provided in the analysis of the dataset helped a lot my understanding of the sources of variability. Furthermore, the dataset is substantially big and I would image a lot of people can use it for different purposes.

The tools and data are open-source.

They provide methods to detect unrepresentative servers. These could be used before doing the actual experiments, to give better results.

The paper provides actionable output for experimenting with individual hardware and experimenting on testbeds: randomize experiment ordering, perform sensitivity analysis w.r.t. hardware configurations, don't assume experiment independence, etc. I think this can be used a small checklist when doing an experiment even if readers don't adopt using their framework.

The paper was quite heavy to read for me since it required a lot of attention, but I think the authors did a very good job of walking the reader through their experiments.

### Paper weaknesses

CONFIRM is a very nice deliverable, but of course, is limited to the hardware and locations that the experiments took place and the specific benchmarks. Besides the benchmarks, this is quite narrow.

The methodology of experimentation should be clearly stated somewhere in the paper,i.e. actually enumerate the steps someone should take when experimenting with these benchmarks. I find this is a bit dispersed through the paper as actionable advice, rather than a checklist.

The MMD test was not clearly explained. I would have liked more details.

Maybe the structure could have been separated to show the problems that appear only on the same machine when experimenting vs. the problems that appear on multiple machines.

I think the paper should have focused on mapping the advice to scenarios: what should I do if I run my benchmarking on the cloud, what about my own machine, etc.

In the end, I do not know what are the final takeaways and conclusions of the paper.

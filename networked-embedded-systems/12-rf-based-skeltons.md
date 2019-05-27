# [RF-Based 3D Skeletons](http://people.ee.ethz.ch/~nescrp/hotcrp/doc.php/nescrp-paper121.pdf)

#### Paper summary

This paper introduces a system that infers 3D human skeletons from RF signals. It requires no sensors on the body, and works with multiple people and across walls and occlusions.

#### Paper strengths
They achieve impressive accuracy(under 5cm) and the paper has many applications.

The idea of moving the 4D to 2 3D spaces is quite natural and well executed; moreover, the explanation on model decomposition and the appendix make the methodology very clear.

They explain keypoint localization as a classification problem. The loss function used makes sense since it requires fitting all the keypoints at once.

The idea of detecting objects in the intermediate layer is fairly used in computer visions. Proposing it for multi-person estimation also accounts for the limitation in close frames that come from the multipath effect.

The paper has a good flow; it basically makes the reader understand their methodology at all steps.

The evaluation seems quite impressive: works through walls, good accuracy, multiple people, robust to environmental change.

I like the structure of the paper in general and the fact that the details and background are clearly separated in their sections. It makes the paper so much easier to read since you can just skip some parts.

#### Paper weaknesses
The Primer section may even be a bit over-detailed. Similarly, section 4 and 1 seem to have lots of overlapping content.

The camera system becomes unstable to occlusions by their saying for multiple people. I don't see a clear reason for this if you can correlate the data over time.

I don't see why the algorithm wouldn't be able to generalize to more than 4 people since the separation is still based on higher level features. Maybe I missed something.

I would have liked for the errors to be put in perspective. Is the 4-5 cm error relevant to some particular algorithms that would be applied after the position detection?

I am also curious if adding or cutting observed points of interest(head, neck, wrist, etc.) in the training process has any effect in reducing accuracy.

The distance is not taken too much into account in the evaluation section. How far can people be? Does distance affect accuracy?

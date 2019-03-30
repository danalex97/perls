# [Enabling Deep-Tissue Networking for Miniature Medical Devices](http://www.mit.edu/~fadel/papers/IVN-paper.pdf)

### Summary

The paper presents a beamfolding algorithm that can focus its energy towards an implantable device. This allows communication with millimeter-sized sensors at over 10cm depth in fluids, as well as battery-free tags in a central organ.

### Paper strengths

The motivation of the paper is clearly stated. Implantable medical devices can be used for decoding brain circuits, delivering drugs or monitoring vital signs. Enabling networking in in-vivo devices can bring advancements in optogenetics and removing the need for battery incorporation.

The background on RF power harvesting is very helpful in understanding the improvements brought by the paper. The paper explains clearly how a basic circuit that converts RF signals into DC voltage works and explains what typical beamfolding approaches are taken for powering the battery-free device.

The main idea is elegant. It starts from the observation that phase synchronization is hard to achieve using traditional beamfolding as waves travel through irregular environments such as tissues. Therefore, the paper can achieve the same effect by using different frequencies. The phase shift of the waves with respect to each other would determine constructive(and destructive) interference at certain points in time, effectively allowing the battery-free device to harvest energy when constructive interference happens.

The direct advantages of the main idea are that the process can be done under blind channel conditions, the power maximum power gain is of order O(N^2) and the power gains are achieved for any point in 3D space close enough to the beamfolding antennas.

The formulation of selecting the center frequency as an optimization problem on random variables of phase shifts seems to fit reality as the wave are traveling on different paths hard to estimate, hence independence is reasonable to assume. Moreover, the constraints on the cyclic operation and amplitude flatness make the device to provide greater reliability. Thus, the device could actually be used for the proposed applications in the introductory section.

The approach for the optimization problem is also generalizable since additional constraints can be added based on depth knowledge and different expectation probabilities added based on different materials. Furthermore, the paper mentions that the power transfer can also be optimized with depth knowledge.

The range for powering off-the-shelf passive RFIDs is 7x better than previous solutions.

The evaluation section treats both in-vivo and ex-vivo cases. For ex-vivo, the gain increases fast with the number of antennas and the approach shows robustness against depth, orientation, and medium changes. Moreover, the prototype is shown to work for in-vivo devices, showing that the proof-of-concept implementation is applicable.

### Paper weaknesses

The test of the device in the gastric placement only succeeded in half the cases, even if the authors explain the failures. However, the in-vivo tests don't show a mature research product, but rather a proof-of-concept since the number of trails is small. Also, the duration of the trails is not very clear from the experiment description.

The explanation of why the experiment in the stomach did not work seems quite succinct. If the antenna did not have enough energy to start up, does this mean that there is too much attenuation for the energy produced to pass the minimum threshold? Wouldn't this be solved by adding more antennas?

For evaluation, it would have been interesting to see how the solution behaves with multiple devices.

It was mentioned that array beamfolding supports higher SNR. It was not clear to me why that's the case.

### Open questions and improvement

Can the RFID tag collect energy from different sources as well(e.g. thermal energy), in addition to the energy collected from incoming beams?

What applications could this beamfolding technique have outside medicine? From what I see, it can be used as an increased range multicast mechanism. This can also increase communication range in general when location of nearby devices is not known.

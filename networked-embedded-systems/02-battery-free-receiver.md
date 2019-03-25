# [Battery-free 802.15.4 Receiver](http://ambuj.se/IPSNZigBee.pdf)

### Summary

The paper presents the architecture of an 802.15.4 receiver that operates at a few hundred microwatts, enabling new battery-free applications. It does this by offloading the power-hungry local oscillator to an external device and by treating a phase-modulated 802.15.4 signal as a frequency-modulated one.

### Paper strengths

Offloading the power-hungry local oscillator to an external device by using an unmodulated carrier of frequency can significantly reduce the power consumption of the RF front-end.

Phase demodulation at the receiver can be done by using a passive slope detector, which has less power consumption. The is possible since OQSPK modulation can be formulated as Minimum Shift Keying modulation.

The paper provides evaluation for a prototype that consumes at least 5 times less power and has similar sensitivity as the receiver.

Using an IF amplifier, the receiver has more use cases since the communication range can be increased to up to 7 meters.

The component can be grouped with a backscatter transmitter to obtain battery-free transceiver capabilities.

### Paper weaknesses

A fundamental characteristic of the receiver architecture is the need for an external carrier generator.

Since the communication range is small, the device can be used only for short-range sensor networks with high node density.

The paper mentions that we can pair the device with a backscatter transmitter, allowing bidirectional battery-free communication given a provided carrier. However, it would have been nice to give a few background information on the backscatter transmitter and maybe mention the performance of a prototype with both pieces of hardware in the evaluation section.

I like that the paper provides the architecture of a classical receiver in contrast with the prototype, but having a short summary describing, in contrast, the 2 architectures before diving into details would have been much more clear.

I think another important point is that the device is less resilient to interference compared to commercial alternatives. However, this is mentioned only in the evaluation section towards the end and I haven't noticed an experimental comparison with commercial alternatives.

### Open questions and improvement

Since we are looking for a component that is used for a battery-free device, I wonder if the deployment should have also been tested in adversarial deployment conditions(e.g. high humidity, etc).

Another interesting point for me would be if the device should be able to use different amplifiers for providing smaller or bigger ranges of communication, based on its location in the topology(i.e. distance to the carrier)

# [MUTE: Bringing IoT to Noise Cancellation](https://synrg.csl.illinois.edu/papers/mute-sigcomm18.pdf)

### Summary

This paper exploits velocity gap between RF and sound to improve active noise cancellation. By placing an IoT device that listens to ambient sounds and forward the sound over a wireless radio, we can improve the performance of a noise cancellation device by gaining time to peropare the noise cancellation signal.

### Paper strengths

The background on noise cancellation is quite detailed and easy to follow. The components of the error signal measured at the error mic are clearly detailed, the paper showing where the limitations in current ANC methods appear: e.g. the tight timing bound doesn't allow classical ANC to cancel high-frequency sounds.

The advantages of the lookahead-aware noise cancellation algorithm over classical active noise cancellation are clearly stated: namely the timing advantage of having future samples and the opportunity for sound profiling.  

The use of sound profiling to seems appropriate since filtering sound sources individually should provide better performance: for example, in the presence of an intermittent source and a continuous one this would allow the algorithm to filter the continuous source all the time. The example given in figure 8 captures the idea very well.

The relay has a clean design: the audio quality is kept by frequency modulation and positive lookahead is detected by cross-correlating the forwarded signal with error microphone.

The relay comes is multiple architectural variants: a personal table-top, a public edge service or smart noise devices attached to sources.

Even though it's left for future work, the concern of privacy awareness is brought into discussion and possible solutions such as beamfolding and sound scrambling are proposed.

The paper generally has a good flow, clear examples and detailed design details.

The performance improvement is fairly good and the claim that high-frequency noise filtering is possible with this approach is confirmed by the experiments.

### Paper weaknesses

The LANC design section is fairly hard to follow when talking about non-causality. In particular, the emergence of negative values for the inverse of the noise signal captured by the reference microphone is not explained, thus making the rest of the section harder to follow. Moreover, the use of steepest gradient descent is not motivated in comparison with other possible variants.

The human experience experiment is quite unreliable. That is, the group control is made only of 5 users, which does not provide much usefulness. Moreover, the headphone tests were made for only one ear.

The wireless relay selection experiment that shows the correlation technique only shows an example with 2 spikes, which can hardly show that the technique works in a general setting.

The usability may be a problem since the user needs to carry the relay with him. However, MUTE is still applicable in a large number of cases.

There is not much evaluation when overlapping multiple sound sources. This would be useful to prove that that sound profiling works as expected.

### Open questions and improvement

I think that it would be useful to relate the objectives of optimization to the user experience. For example, it might be that for the user the convergence time would be more important than the strength of the cancellation.

In related work distributed DSP processing is mentioned. This could be useful for this device since the user has to carry the relays. If multiple relays are present in the same place, it would be useful for them to collaborate.

Another interesting idea would be making the relay battery-free. Having a battery-free relay could the whole solution cheaper and more portable. As far as I know there is some work related to this, such as battery-free cellphone.

Moving the relay to a smartphone and/or laptop would also make the solution more practical and cheaper.

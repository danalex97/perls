# [System Architecture Directions for Post-SoC/32-bit Networked Sensors](https://rise.cs.berkeley.edu/blog/publication/system-architecture-directions-for-post-soc-32-bit-networked-sensors/)

### Summary

The paper presents major trends in networked sensors: more powerful MCUs with more radio consumption, less power-intensive and more efficient radio, and cheaper production of SoC motes. They present both customisable hardware(Hamilton) and OS modifications to account for these changes.

### Paper strengths
The paper presents quite substantial work, from developing the Hamilton mote to porting and improving multiple operating systems.

The related work section provides a broad overview of different motes and OS paradigms. The section is easy to read due to the story-like layout and putting the mote generations in context.

The Hamilton design provides cost reduction from both integrating processing, storage and communication and producing a fully-integrated mote. The authors also present how the cost depends on different production contexts.

The power consumption analysis in section 4 is clear: the lower MCU idle consumption and the comparable MCU and radio power capture well a significant trend in hardware modern components. This results in the need for tickless OSes.

The cooperative and adaptive clocking ideas are elegant and simple to follow. This can be probably used even in other contexts. Caching sensor data by the driver is also very good for efficiency.

The networking implementation saves memory space and context switches.

The evaluation is nicely complemented with the findings mentioned earlier in the paper, making it easier to read.

The style of writing is generally clear and through. The introduction and summary for each section make the paper easy to follow.

### Paper weaknesses
Even though the argument for full thread-based concurrency is compelling, I do not think that event-based concurrency is presented in the best light. For example, from the usability perspective, I could argue that Tock is more usable than RIOT. Taking into discussion new developments in the field together with Contiki would have been nicer.

Caching sensor data could have been more detailed: how much space do I have for the readings, we buffer the reading or just overwrite them. This is not a big problem, as these details may not be essential.

Networking in one thread has a tradeoff that they did not mention: if the mote tries to use multiple stacks at the same time(e.g. UDP and BLE) one type of packet may be delayed. This may be more complicated to handle in case of real-time events.

They mentioned that each thread has a packet queue, but they don't mention its data overhead. Again, since the mote has more memory this may not be a problem.

When evaluation energy consumption, showing an evaluation without AES encrypted payloads would have been interesting since encryption gives an advantage in terms of energy consumption to Hamilton.

### Open questions and improvement
I am quite positive about the paper and I think most of my negative comments are not very significant. I think they give a good research direction and that the work put into designing the mote and porting and analyzing the OSes is substantial.

What I think that could have been improved is mentioning the significance of the event-driven direction as well. Maybe on the long term, event-driven driven OSes allow for more opportunities to reduce power and the programming model can be fairly nicely hidden under higher level abstractions. For example, I imagine that cooperative threading could be nicely stacked upon an event-driven OS and a fair amount of people are familiar with it.

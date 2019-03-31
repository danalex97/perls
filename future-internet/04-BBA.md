# Paper summary <br> [A Buffer-Based Approach to Rate Adaptation](http://yuba.stanford.edu/~nickm/papers/sigcomm2014-video.pdf)

### Motivation

ABR algorithms try to:
  - maximize video quality
  - minimize rebuffering events

One approach is to pick a video rate by estimating future capacity from past observations. However, in environments with highly variable throughput this approach does not work.

These algorithms augment capacity estimation with adjustment based on buffer occupancy: more conservative when buffer is almost empty, more aggressive when buffer is almost full.

#### Current approaches


The buffer:
  - fills with rate C(t)/R(t)
  - buffer occupancy is B(t)
  - output rate is 1


Approach:
  - measures chunks downloads to estimate capacity Ĉ(t)
  - adjustment factor F(B(t)) based on buffer occupancy
  - video rate: R(t) = F(B(t)) * Ĉ(t)

### Main idea

Use buffer-based ABR algorithm. We say that an ABR algorithm is buffer-based if it picks the video rate as a function of the current buffer occupancy, B(t).

### Basic approach

Simplifying assumptions:
  - chunk size is small enough
  - any video rate between Rmin, Rmax is available
  - videos are encoded at constant bit rate
  - infinitely long videos

Any rate map f that is **continuous**, **strictly increasing** and have **ends pinned** at Rmin and Rmax, don't generate any rebuffering and maximize average video rate:
  - no rebuffering: f(B) tends to Rmin when B tends to 0
  - average video rate maximized: for a fixed capacity level, we get a "sawtooth" behavior

To adapt this for real-world, we keep a **reservoir** of r seconds, so that any longer download of a segment(which have a discrete size in reality) will have segments to consume. We keep a **cushion** space in which we ramp up the rate. It has to be as spread out as possible to account for the fact that we have only a few fixed rates.

Algorithm:
```python
Input:
  - R_prev
  - B_now
  - r: reservoir size
  - cu: cushion size
Output:
  - R_next

# get next and previous rate levels
R_up   = min(R_i s.t. R_i > Rate_prev)
R_down = max(R_i s.t. R_i < Rate_prev)

# default keep same value
R_next = R_prev

if B_now <= r: # handle reservoir
	R_next = R_min
elif B_now >= r + cu: # handle upper reservoir
	R_next = R_max
else:
	if f(B_now) >= R_up: # move up on f
		R_next = max(R_i s.t. R_i < f(B_now))
	if f(B_now) <= R_up: # move down on f
		R_next = min(R_i s.t. R_i > f(B_now))
```

### Other challenges

#### VBR

We reformulate the problem in terms of the chunk sizes. To solve the problem of VBR, we will vary the size of the reservoir by the amount of data we will resupply/consume during a particular interval.

Of course, now instead of having the mapping from buffer occupancy to rates, we will have a mapping to chunk sizes.

#### Startup

During the startup we can ramp-up the download speed based on the previous capacity estimation. This acts as a "slow-start" mechanism: we ramp up until buffer is decreasing or the f mapping suggests higher rate.

#### Switch rate

We can reduce the chance of switching by looking ahead at future chunks, and, in case we see bigger variance, we can probably keep the same rate.(i.e. video quality)

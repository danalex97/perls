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

**BBA-0:**
```python
Input:
  - R_prev: previous rate
  - B_now: buffer size 
  
  - r: reservoir size
  - cu: cushion size
Output:
  - R_next: next rate

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
	if f(B_now) <= R_down: # move down on f
		R_next = min(R_i s.t. R_i > f(B_now))
```

### VBR

For different segment sizes, let us think of the effect on a buffer during a single segment download. The download of the segment takes `segment_size/avg_network_capacity` seconds, which will be consumed, since the user watches already downloaded material during the time. The seconds added to the buffer are equal to the time that the video segment has, which is a constant `V`. Note this is used to update the buffer size after a new segment is downloaded.

Therefore, we reformulate the problem in terms of the chunk sizes. To avoid buffering, we will vary the size of the reservoir by the amount of data we will resupply/consume during a particular interval. Furthermore, since we look at chunk sizes now we need to compare the current segment size suggested by the mapping with the chunk size of the next segment associated with rate `R_up`, etc.

**BBA-1:**
```python
Input:
  - k: previous segment number
  - R_prev: previous rate
  - c_prev: average network capacity during last download
  - B_now: buffer size now
  
  - chunk: chunk size mapping
  - r: reservoir size
  - cu: cushion size
  - X: time horizon
Output:
  - R_next: next rate

# get next and previous rate levels
R_up   = min(R_i s.t. R_i > R_prev)
R_down = max(R_i s.t. R_i < R_prev)

# default keep same value
R_next = R_prev

# calculate projected reservoir(using chunk mapping would be more exact)
r_future = r + X * c_prev / R_min

if B_now <= r_future: # handle reservoir
	R_next = R_min
elif B_now >= r + cu: # handle upper reservoir - not specified how
	R_next = R_max
else:
	if f(B_now) >= chunk[k + 1][R_up]: # move up on f
		R_next = max(R_i s.t. chunk[k + 1][R_i] < f(B_now))
	if f(B_now) <= chunk[k + 1][R_down]: # move down on f
		R_next = min(R_i s.t. chunk[k + 1][R_i] > f(B_now))
```

### Other challenges

#### Startup

During the startup we can ramp-up the download speed based on the previous capacity estimation. This acts as a "slow-start" mechanism: we ramp up until buffer is decreasing or the f mapping suggests higher rate.

#### Switch rate

We can reduce the chance of switching by looking ahead at future chunks, and, in case we see bigger variance, we can probably keep the same rate.(i.e. video quality)

# [Vesper](https://www.usenix.org/system/files/conference/nsdi18/nsdi18-netravali-vesper.pdf)

### Paper summary
Vesper raises the issue of capturing page interactivity when defining metrics for page load time. The paper defines the ready index which captures both an element's functionality and visibility features. Vesper is the framework used to measure the RI metric by looking for the last changes applied to the relevant elements of the DOM, the pain tree and the JS heap.

The authors show how to provide a schedule for fetching and evaluating elements of the page in order to optimize the RI metric. In contrast to other metrics, RI proves to capture page interactivity. Furthermore, user studies show that
pages which optimize for Ready Index support more immediate user interactions with less user frustration.

### Key insight(s)
- The ready index captures both an element's functionality and visibility features. The index takes into account the size the elements above-the-fold and rewards loading elements faster.

- The original Page Load Time metric is too conservative, while Google's Speed Index only looks at the time taken to render elements.

- Vesper measures the RI metric in two stages: identifying the page's interactive state(visibility, event handlers, handler state) offline and then capturing the times of the last element, handler and pain tree modifications.

- Optimizing for RI is done via rewriting the page for evaluating and fetching objects based on weights assigned to the dependency graph.

- User studies show that optimizing for RI shows comparable results in terms of rendering while improving user interactivity.

### What could be improved?
I like the fact that the framework is extensible to defining whatever ratio between a page's visibility and functionality. However, it would have been interesting to see how this ratio(currently 1/2-1/2) does affect users.

I think another important part of interactivity is related to the actual functionality of the page. Typically companies use frameworks that track user interaction for testing UIs; I am sure that this should be taken into account when assigning weights in Polaris' dependency graph.

Finally, using the pixel area as the main deciding factor for the order of loading DOM elements makes sense. However, using this for JS functionality might not: e.g. an autocompletion library for a search bar may be more important than a lens effect library.

# [Prophecy](https://www.usenix.org/system/files/conference/nsdi18/nsdi18-netravali-prophecy.pdf)

### Paper summary
Prophecy is an acceleration system for mobile page loads. The main idea around Prophecy is making the browser skipping intermediate rendering stages. To accomplish this, it uses a server hosting a headless browser to process the pages and generates DOM and JS write logs. The write logs are compressed by capturing only the last state of all objects. Finally, the system allows caching by using a table of versions and differences. Prophecy yields improvements for mobile devices' page load time, bandwidth consumption and energy consumption.

### Key insight(s)
- Prophecy allows skipping intermediate rendering stages in a browser by capturing the state of a web page after loading has finished.

- Running the loading stages is done via a headless browser and the logs are generating by modifying the original client-side code.

- The system captures the page state via writing a single JS script that builds the DOM state, the JS heap state, dispatches all image requests and fixes all DOM-to-JS references.

- The CSS style attributes are directly embedded in the HTML elements in order to optimize the painting stage of browser rendering.

- Caching and incremental updates are supported by a server-side in-memory table of versions and differences.

- The system allows optimizations for loading faster above-the-fold content by separating the rendering in two phases: above-the-fold and below-the-fold.

### What could be improved?
The only tested browser was Chrome, but Safari has a big share of the mobile market. I suspect the results won't be extremely different, but nevertheless, browsers do painting differently. For example, in Firefox graphics pipeline JS has priority over other components. Embedding everything in JS code might not be a good idea since the GPU will do nothing until the JS script was executed.

Another interesting point is that the DOM tree is built from top to bottom. Wouldn't it make sense to prioritize elements that occupy a larger area, for example?

There seems to be no major difference between online and offline Prophecy. This means that the whole framework could be pushed to front-end.

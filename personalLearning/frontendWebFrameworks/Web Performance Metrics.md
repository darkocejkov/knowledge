Based on [this web.dev](https://web.dev/user-centric-performance-metrics/) article.
___
Measuring web application performance is much trickier than just timing how long it takes to load - because we need to concretely define the *what*, in what we are actually loading. 
- previously done with the `load` event
	- however, it only cared about the initial load - it wouldn't actually care about deferred fetched content
- Metrics are meant to be answering the following questions:
	1. Is it *happening*?
	2. Is it *useful*? 
	3. Is it *usable*?
	4. Is it *delightful*?

- There are two main environments to measure:
	- Lab
	- Field
- Neither way is *better*, because the lab is biased heavily and done on powerful, or simulation machines. Field testing is the most *practical*, but hardest, because you have to subject users to it before you really know.
	- We can use **Real User Monitoring**, which is a method in collecting performance data from users while they use the app

# Types of Metrics
- Perceived load speed
	- how *quickly* can a page load/render all elements
- Load responsiveness
	- how quicky can page load and execute JavaScript to make it interative?
- Runtime responsiveness
	- after load, how quickly can the user interact?
- Visual stability
	- do elements shift in potentially interfering ways?
- Smoothness
	- consistent frame rates on animates, how smooth/fluid do transitions from one state to another happen?

# Metrics
## [First Contentful Paint (FCP)](https://web.dev/fcp/)
- time between page *starts* loading, to when *ANY* content is rendered
![[Pasted image 20230412200107.png]]

## Largest Contentful Paint (LCP)
- time from page *starts* loading, to when the *largest text block/image* is rendered
![[Pasted image 20230412200318.png]]

## First Input Delay (FID)
- time from the first *user interaction*, to the the time when brower begins processing event handlers
	- the *delay* of when the browser actually starts processing an input request
![[Pasted image 20230412200542.png]]
- Happens because JavaScript is a single-threaded runtime, so it *can be blocked* from doing work, typically when it's parsing a large JS file.

## Interaction to Next Paint (INP) (experimental)
- pretty simply, the delay between the start of an interaction, and when the *next* paint occurs
![[Pasted image 20230412201054.png]]
- users *expect* the UI to change almost instantly, so bad/slow responsiveness means that users become *unsure* of the interaction they made, and try and re-do it.

## Time To Interactive (TTI)
- time from page *starts* loading, to when it is capable of *responding* to user input.
- A good UX should look for a TTI < 5 seconds on *average* mobile hardware.
- should be minimizing the time between FCP and TTI
	- server-side rendering can lead to low FCP, but a big difference in TTI

## Total Blocking Time (TBT)
- the time between FCP and TTI, where the *main thread* was *blocked* for long enough to prevent input responsiveness
	- being "blocked" means that a Long Task (>= 50 ms) is blocking the main thread, because the browser cannot interrupt it
	- if a user interacts during this time, it must queue up this interaction and respond to it when the long task finishes
	- the blocking time describes the time that a task is blocked by another

## Cumulative Layout Shift (CLS)
- a measure of the *largest burst* of layout shift scores, for all *unexpected* shifts during the whole lifespan of the page.
	- a "layout shift" is when a visibile element changes position from one frame to the next.
	- a "burst" of these shifts is called a "session window", with less than 1 second intervals between each shift, and a max. of 5 seconds of the total window duration

- typically due to asynchronous resources, DOM elements removed/inserted that shift the layout, an image with dynamic dimensions, a font that is slightly larger or smaller than you thought, an ad or width that changes size.
![[Pasted image 20230412202831.png]]
- What matters most is that these elements must change their *start* position

## Time To First Byte (TTFB)
- time between *request* for a resource, and the time the *first byte* of the response
![[Pasted image 20230412203023.png]]
- It's a sum of:
	- redirect
	- service worker startup (if applicable)
	- DNS lookup
	- connection/TLS startup
	- request
- up until the time of the first byte of the response

![[Pasted image 20230412203154.png]]
___

# NPM
Stands for "Node Package Manager", bundled with NodeJS installations. It allows us to control the way we use external packages. Also a public repository of many, many, many different packages for NodeJS.

## Dependency?
Whenever we want to use an "external" package in our project, there are a few ways we can actually include it:
1. Find a version online that includes the source code and manually import into the project
2. use a package manager to download and source the documents of the package into the project

This also avoids talking about updating packages, conflicts between versions of packages, and endless more complexities. The package manager is obviously the way to go to. Whenever you add a package to your project, you create what's called a **dependency**, because your project *depends* on this package.
- A *dev* dependency is a development workflow package, a tool that makes it possible/easier to develop the project, that the end product will depend on
	- JSON server for example, allows us to create a simple JSON server to host data for accurate data fetching simulation.

# JSON Server
- A basic data server that serves pre-defined JSON content, through endpoint routes based on the JSON structure

# Fetching & Promises
- Simple data fetching uses either the `fetch` function built into JS, and is well supported
	- or, we can use external packages like `axios` to make it even simpler
- XHR data fetching was based on the *event* loop, in which we create an XHR object and define its behaviours, fetch some resource, to which *events* fire based on the status and progress of the data fetch.
- More modern practices have shifted to using JS `promises`, which are very much exactly what they sound like, a promise of resolving data, an asynchronous function that handles data once the promise either *resolves* (success) or *rejects* (failure)

## JavaScript Runtimes and Asynchronicity
- JS engines are single-threaded, unable to parallel execute
- When asynchronous code runs, the execution therefore continues outside of the asynchronous callback
	- The async. callback function runs when the async. IO operation's promise is fulfilled.

## Promises
Promises are ways to deal with "producing code" that does some process that can take an indeterminate amount of time, like fetching data over networks, and how the "consuming code" is notified about when the producing code is finished.
A promise is basically a very clean way to conditionally branch logic based on the success (resolve - value) or rejection (failure - error) of asynchronous code.

Axios & fetch *return* promise objects, which allow us to use asynchronous chaining syntax to determine what to do with the data that comes back from those promises, and importantly, how errors are handled if any occur.

# Effects
Effects in React are concepts based on changes in state. Whenever a change in state occurs, it triggers a re-render. We might  want to be able to handle additional synchronization and logic whenever a change occurs, which we call a "side-effect".

Effects are meant to be ways to hook into changes in state to trigger additional "side-effects" to mainly synchronize APIs for non-React interfaces. The keyword here is *synchronize*, because we should NOT use effect hooks to "chain logic" or react to changes in React's state to trigger other state changes.
- We should therefore only create side-effects to create synchronization between non-react variables, APIs, interfaces, etc.

Golden rules of affecting React's state:
1. Any changes to React state should always be through the state interface, and not directly mutating state variables
2. React state updates should only be done in response to some event as part of an event handler.
> An exception to 2. is usually in terms of data fetching with effects, because it's necessary to hold the fetched data in a state, and there's really no other place to trigger a data fetch. 

What is really meant by these rules, is that we adhere to them because they create more efficient and predictable applications. Effects and any resulting side-effects run after a re-render cycle, so when a state changes, React renders (by invoking and constructing all JSX), then schedules commits to the DOM tree, then any defined effects fire.
> So, if we have some bad logic, and create a chain of state updates in a side-effect, any state changes cause cascading state changes.

Effects are created using the `useEffect` hook, in which we define a function to run, our side-effect, and a "dependency array" that indicates *what states to invoke the side-effect on re-renders*
- No dependency arrays means on *every* render
- `[]` means only the *first* render, and none after
- `[stateA, stateB]` means only on render in which stateA OR stateB have been changed

```jsx

	useEffect(() => {
		axios
			.get('http://localhost:3001/notes')
			.then(resp => {
				setNotes(resp)
			})

	}, [])

```
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

# Altering Server Data
In typical HTTP servers, the method we use to send requests decides what the server does to the stored data.
- HTTP GET reads data
- HTTP POST inserts new data
- HTTP PUT replaces data
- HTTP PATCH updates parts of data

It's a little more nuanced when you get into the differences between these, because there are configurations of payload data that can make some of these redundant.
- For example, we could alter the client-side data before a PUT request to be the entirety of the existing object with some fields changed, which would make it very similar to a PATCH request.

## Dynamic Event Handling
```jsx
{notes.map(note => {
	<Note toggle={() => toggleImportance(note.id)}/>
})}
```
We can create "dynamic" event handlers when we map elements from a collection this way.

## Shallow Copy
A "Shallow copy" is a way to describe how copy objects are created. If we remember, in JS, references (pointers) are heavily used to optimize space.
In a shallow copy, only properties that are primitives are created as NEW properties, and are not references to the original property, thus, the shallow copy only copies properties on the "first depth" of the object we are copying.
Any properties which are themselves objects are created as references to the *original* object property.
> `...object` is a "spread" of the object that creates a shallow copy

Knowing this is important for React because we treat state as immutable, so we always avoid manipulating the original directly - which is possible even when we create shallow copies because sub-objects are references to the original, and manipulations in the "copy" actually manipulate the original.

# Creating a Module for backend communication
It's very much worth it to seperate the communication functions into their own files / module so that each piece of our UI follows the *single responsibility principle* of OOP design.
- `App.js` handles rendering and events of the UI
- `/service/notes.js` handles communication between the UI and Backend, given that the functions depend on UI events, like which specific data element is being manipulated.

We can take this a step further, and create a module with export that allows us to create UI-specific functionality through chaining.

```js

// ./service/notes.js
const get = () => { return axios.get(url) }
const create = (object) => { return axios.post(url, object) }
const update = (id, object) => { reqturn axios.put(`${url}/${id}`, object) }

export default {
	get,
	create,
	update
}

// ./App.js
import noteService from './service/notes'
// ...
useEffect(() => {
	noteService
	.get()
	.then(resp => {
		setNotes(resp.data)
	})
}, [])

```
> This part is a little more JS heavy but we export an object from the service module, which we can call anything in the import. When we call any of the functions defined in the module, like `.get()` or `.update()`, it returns a *promise* (axios returns a promise, which we return), so that way, we can create UI-module-specific promise handling

Since the `.then` needs to parse the `.data` part from the HTTP response, we could seperate that into the service module:
```js
	const get = () => {
		const req = axios.get(url)
		return req.then(response => response.data)
	}

	...
	noteService
		.get()
		.then(data => {
			setNotes(data)
		})
```

## Simple Object Literals (ES6)
When creating object literals, if the property we want to store is in some variable, we do not need to define `x: x` in the literal, we can simplify that entry.
```
	{
		get: get,
		set: set,
		x: x
		y: 'ABC'
	}

	// ... becomes

	{
		get,
		set,
		x,
		y: 'ABC'
	}

```

## Promise Chaining and Errors
Promises and handling their fulfillment depends on either:
1. using async/await to force synchronicity
2. handling asynchronous tasks gracefully through chaining operations

Chaining operations are among the simplest because it's a very declarative process, you just describe what should happen when a promise is fulfilled or a value is returned
- I say "a value is returned" because we don't *need* the function to be asynchronous, it's just a chain of functions that runs.

```js

new Promise((res, rej) => {
	//...
	resolve(1)
})
.then(result => {
	return result * 2
	// 1 x 2 = 2
})
.then(result => {
	return result * 3
	// 2 x 3 = 6
})
.then(result => {
	return result * 4
	// 6 x 4 = 24
})

```
> It's quite similar to the `reduce` idea, in which we *chain* returns. It's not exactly clear what we would use this for in terms of real promises and data fetching, so here's a full example:

```js

	axios.get(url)
	.then(response => response.json())
	.then(data => {
		return data.data
	})
	.then(data => {
		setData(data)
	})
	.catch(err => {
		alert(`${err}`)
	})

```
This is a more practical example of fetching data using axios and handling the asynchronous data using the `.then` callback syntax. the `.json()` method returns a promise, which we can continue chaining on to seperate the `.data` field which actually contains the payload data into another chain to then finally set states.
> An important distinction here is that we included a `.catch` to the end of the chain to handle errors. If errors occur ANYWHERE in the process of the chain like the initial promise, or in any of the `.then` callbacks, then the exception gets *caught* by the `.catch`.

## Data Fetching in Effects
Data Fetching is among one of the most complex things to optimize, because introducing that connection between the front and backend introduces a million different questions and concepts. Data caching, authentication, cookies, storage, ..., the list goes on. In order to make an application that fetches a LOT of data work well when more than just YOU use it, there has to be considerations about how and when data is fetched, and if it's even necessary, or allowed to do so.

One of the more simple ways to control data is by paying attention to when the fetches occur (through what effects they trigger on), and utilizing local flags to affect whether or not state gets changed.

Imagine you have more than just 1 render effect, based on pages or states. If you trigger a view with a render side-effect that fetches data, then quickly change views to another - the asynchronous callback will continue regardless of the view and sets state when it finishes even though the component may not be rendering.

All side effects we create through the `useEffect` hook allow us to define a *cleanup* function, which runs *before* any  of the actual side-effect code on any subsequent  renders, see: ([[React#Effect Cleanup]]). Cleanup functions execute on "unmount" of the component as well, so we can use these cleanups to change a local flag that indicates to the asynchronous code to NOT manipulate state if the flag is not true.


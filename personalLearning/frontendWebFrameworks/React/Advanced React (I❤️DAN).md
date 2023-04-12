A love letter to Dan's incredible thinking. It's pretty obvious that one of the people that created React would have such a fundamentally clear description of React. This is more than just the syntax and construction of React *code*, but rather the advanced principles and designs that make it easier to write *good* code. In previous experience, it seems pretty simple and obvious that *effects* are basically just reactions to changes in state, and we can "*make effects go brrrrr*" when a state changes and we want to impose logic on that state. that is effectively, just wrong. I used to approach thinking of React in this weird, akward area where it's both class-based runtime, while also functional. As if hooks *mimick* classes - which is absolutely not true, even though they may accomplish some of the same functionality, the *mental model* that goes into thinking about React is pretty advanced and high-level.
___
# [React as a UI runtime](https://overreacted.io/react-as-a-ui-runtime/)
- When introduced to React, it's almost certainly the case that you are using it for the web
	- However, React is more than just a "web" framework - the concepts of React are much bigger than that
	- This breakdown explores the idea about how React works as a UI runtime, and not just a JS-based web framework to build web pages

## Host Tree
- Programs and frameworks output *something*
	- React outputs a *tree* that *may* change over time
		- DOM tree
		- iOS hierarchy
		- PDF primitives
		- JSON objects
- A "host tree" is the environment outside React, it's the *other side* that React interfaces with
	- Host trees have their own *imperative API* that allow anything to imperatively interact with its elements
		- React is meant to live above those APIs
- Really, all React does is provide a way to manipulate complex host trees responding to external events
- React is based on 2 principles:
	1. Stability
		- Host trees are stable, and updates don't radically change structure. Elements are not meant to change all at once every microsecond
	2. Regularity
		- Host tree can be broken into UI patterns that look and behave consistently.

## Host Instances
- These are *instances* of elements within the host tree. Nodes, elements, whatever they are - they are what the host tree is made of.
	- For example, within the DOM environment, the instances are *DOM nodes*. on iOS, they are native elements to the system itself.

- Instances have *properties*, and may have other instances as children.
- Like previously mentioned, Hosts usually have APIs, which allow you to manipulate instances
	- `appendChild`, `removeChild`, ...
		- If you've created a React application - you don't call any of these, rather, React's runtime calls these API methods to change the UI based on what you *declared* it to be.

## Renderers
- The *renderer* is the specific API that teaches React how to talk to specific host environments and manage the instances.
	- React DOM (web, DOM)
	- React Native (mobile, iOS/Android)
	- Ink (terminal)
- Renderers are not magic, you can write your own renderer.
- Modes of rendering:
	- Mutating
		- create, set, add/remove. Instances are *mutable*
	- Persistent
		- *immutable* elements. parent trees are cloned to make a new tree. facilitates multi-threading.

## React Elements
- The atomic units that are created in React are React elements, which are basically just plain JS objects. 
	- they *describe* the host instance.
	- they *nest* to form hierarchies and trees
- React elements are not persistent - they are re-created and thrown away
	- However, they are *immutable*. In order to change the child or property, React creates a new element

#### React elements are *frames* in a movie. They describe the UI at a snapshot in time. You don't mutate a frame, you add a new one.

## Entry points
- The API that enables us to get React to render a particular element tree within an instance
	- `ReactDOM.render`
	- This API will trigger React to walk down our elements and components, and create a React tree using matching host instances

## Reconciliation
- Is the process of figuring out how to make the host tree match the React element tree
	- Given we have previously rendered host instances, and would like to re-render the tree, how we does React know which elements match, change, re-create?
		- It's possible that React can just re-create the *whole* tree, but that's really impractical with many elements, and also causes the loss of host API synchronization (element focus, selection, scroll, etc)
- Reconcilliation in React is based on the *position* of matching element types.
	- Given that we have some element, if it exists in the same place, we can consider it the *same element*
		- This happens on the local scope of a parent, for each parent element and its children.

## Conditionals
- React is really handy for the use of conditional rendering - rendering specific things based on the output of some expression.
- Conditionals make the concept of reconciliation a bit harder, but not if we understand that React only cares about the ordered position.

## Lists
- Lists challenge reconcilliation and element continuity even further
- Dynamic lists create this idea that the order of elements is actually ever the same
	- Especially if every rendered element is of the same type, how does React know which is which?
- For dynamic lists that are render-heavy, it's important to specify the `key` attribute, because this tells React to care only about the *key* of an element, rather than just the *prototype*.
	- When rendering dynamic lists, if you don't properly set keys, then any changes in the list itself may not create re-renders and thus no visual updates to your list happen
		- If order changes, if list member's content changes, etc...
	- Keys should be unique
		- This only matters per-parent, meaning that React will only "care" about uniqueness within a single parent

## Components
- Instead of always calling the entry point function to render a specific element, we can create a much more organized landscape of components.
- Components can be *classes* (as in class-based React), or *functions*, which are the newest and are the upcoming future of React development

### Purity
- Is an important concept in React, as it relates to JavaScript functions
	- [This article](https://www.educative.io/answers/whats-purity-in-react) explains that a function is *pure* if the return is determined by the input values ONLY, and will ALWAYS be the same mapping.
		- Think of a mathematical *function*. A bijection is a function which is both *one-to-one*  (every $x$ maps exactly to ONE $y$) and *onto* (all of the domain is mapped to the entirety of the range). 
- In the scope of React, purity means that a function/component does not **mutate** *state*, especially if it lives outside the component (without a setter!)
- *local* mutations are acceptable, which are mutations on objects that are not stateful, *within* the scope of the current function
- What's **most important** to React is that operations (functions) must be *idempotent*

## Recursive Calling
- Our "components" are functions, but we shouldn't be calling them directly
	- in the words of DAN - it's not *idiomatic*
- Instead of calling functions directly, we declare our functions as "components" through the use of JSX:
```jsx
const Form = () => {
	return ...
}
// NOT
return Form()

// BUT
return(
	<Form />
)
```
- This basically tells react that this function is a component, and allows React to *invoke* the function - not you.
	- When React is rendering, it invokes the functions and then *recurses* into the function that the first function invokes ... and so on and so forth.
	- This allows us to be more declarative about our UI, rather than describe exactly when and what functions are called - because React handles that for us.

```jsx
ReactDOM.render(<App />, domContainer)

<App>
	<Layout>
		<Content>
			<article>
				article text
			</article>
			<Footer>
				<footer>
					footer text
				</footer>
			</Footer>
		</Content>
	</Layout>
</App>
```
- React recurses the tree by invoking all child functions, which is done in the process of *reconcilliation* as well

## Inversion of Control
- The inversion of control is a general design pattern that passes the *control* from the invoker to the definition. Instead of embedding some resulting function - we pass the function like a callback.
- React displays the inversion of control pattern because we define components as functions - which are known by React - and React invokes them.
- Here are some prop
	- Components are more than functions, as they can have features like a *local state*, oriented around the position within the tree
	- It's easier to reconcile, as we can use the types - instead of strictly the returns - to determine what has changed and makes React's job easier
	- React can delay reconcillation, because it handles the invocation, and can let the browser work before re-rendering
	- Makes debugging richer

## Lazy Evaluation
- Is another side-effect of letting React control functions
- It's defined as the ability to have shortcuts on evaluating rendering information, through the use of conditionals
	- Why go through the work of invoking a function if it's result isn't rendered?
	- If we react functions to render, and invoke them not as components - then React cannot intercept its rendering, even when it's not necessary to render.

## State
- Host instances have innate local state: focus, selection, input value, etc ...
- The point of being able to use stateful variables, is that they *persist* between renders, so that we can perserve the state of the UI and react to changes in state
- State should also be seperate for components

## Consistency
- Is the necessity to always show a *consistent* UI, that is not "half-done" or so.
- Rendering can create intermediate rendering states based on style and layout calculations, and display them would not create a *consistent* UI.
- Thus, React deals with this by splitting work into a **render** phase, and a **commit** phase. 
	- Rendering is when React invokes components and reconciles. It can be interrupted, and *can* be async.
	- Commiting is when React actually makes those reconcilled nodes match the host tree and mutates it.

## Memoization
- when a parent issues a state update (using a state setter), React will reconcile the *whole child subtree*, because it cannot know if any changes in the parent cause changes in the child - so it re-renders all children by default.
- *Memoization* is when we tell React to reuse previous render results when props to the child are shallow-equal, meaning that it will then only update if there *are* changes.

```js
function Row({item}){
	//...
}

export default React.memo(Row)
```
> Row components only re-render when the `{item}` prop changes.

- Why aren't all components memoized by default? Because it's actually more efficient to *not* memoize most types of components, because they are so quick and easy to render. 
	- You only should be memoizing components that are large, expensive to render - or don't receive very many changes to props

- With *hooks*, we can use the `useMemo` hook to create memoized stateful variable within components.

## Raw Models
- Small updates are not really "reactive", and instead, top-level updates will react to updates to reconcile
	- This is by design, as the [[Web Performance Metrics#Time To Interactive (TTI)]] metric is important, and using critical timings for small updates is a waste
	- Also, updates are typically *either* small (hover updates) or large (page transitions)
	
## Batching
- React *batches* state updates, so that it doesn't prematurely re-render, and then waste renders on things that haven't actually changed
	- It does so my executing all relevant event handlers first, then triggering a single render to batch those updates

- Because of how state setting works, it can be unintuitive for "synchronous" state setting:
```js
function handleClick(){
	setCount(count + 1)
	setCount(count + 1)
	setCount(count + 1)
}
```
> Even though we call set could *three* times and expect the outcome to be `count + 3`, it really is only `count + 1` because React doesn't *re-call* the state update each time with the new value.
> Or, rather that at invocation time, `count` never increments synchronously, so it's always the *previous states* value.

- In order to work around this, we can pass the state updater a *function* that will use the newest value of the stateful variable:
```js
function handleClick(){
	setCount(c => c + 1)
	setCount(c => c + 1)
	setCount(c => c + 1)
}
```
> Fundamentally, this is similar to how *reducers* work, and puts reducer/dispatcher stateful interactions at an advantage. 
> Reducer & dispatch state manipulation also allows us to be more *semantic* about stateful changes. It gives meaning to arbitrary changes in state, and abstracts the code into the reducer function, where a single 'action' can have 0+ stateful updates associated with it.

## Call Tree
- The call **stack** is how language engines *keep track* of the currently executing functions. If `a()` calls `b()`, which calls `c()`, then the stack looks like: `[a, b, c]`, because it must go through the stack to evaluate the called functions before it finishes evaluating.
- React has its own *call stack* to evaluate rendering outcomes for reconcilliation.
	- Since these "components" form a hierarchy, it's effectively a "call tree" that is required to be kept in-tact because React is constantly referencing and interacting with it
	- Call tree frames are called "Fibers", which is where local state actually lives

## Context
- The React Context provider is a way to *dynamically scope* state for components, rather than having to "prop-drill" manually.
	- It's very, very effective for deeply-nested component trees, for which even the furthest components *may* need some contextual state information to perform its job.
- We wrap components using a context *provider*, that is bundled with the `createContext` call:
```jsx
const Theme = React.createContext('light')
//...
return(
	<Theme.Provider value="dark">
		<Component />
	</Theme.Provider>
)
```
- Children of Providers can 'hook' into the *nearest provider* through the `useContext` hook, to use the value passed down from the closest provider
	- No parent Provider means it uses the default context specified within the `createContext` call.

## Effects
- Components and event handlers *shouldn't* have side effects, meaning that when state changes, we don't want to use effects as a way to handle logic and rules
	- Changes in state sometimes *do* have side-effects, which we would want to "subscribe" to, and perform *synchronization* tasks on.
- Effects are executed *after* the commit phase, because the synchronization shouldn't have any *visual* updates  to block TTI, TTFP
	- There is a hook, `useLayoutEffect` that happens synchronously *during* the rendering phase - but comes at a big cost if you *don't know what you're doing*.
- Effects can *close over* state and props to utilize their values from the newest render
- Effects have *cleanup functions* that run *before* any non-cleanup code, and when the component will *unmount* from the tree
- Effects have *dependencies*, which tell React when to fire/skip the effect and its cleanup.
	- Effects with `[]` dependencies will run only on *component mount*.
	- Effects with `null` dependencies will run on *every* render.
	- Effects with `[a, b, c]` dependencies will run only any of `a`, `b`, `c`, have updated since the last render

- Something important to understand is that effects are functions, so [*closures*](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures) allow us to define *private* functions/variables
	- Any "global" functions that we *use* within effects means that we open ourselves up to a potential bug, if those functions use state or props, AND we don't take care to reference the appropriate depencies in the effect

## Custom Hooks
- Since `useState` and `useEffect` are hooks themselves, we can define *custom* hooks using any normal JS logic, and React hooks
- Hooks are meant to be abstractions of **logic**, so that we can easily bundle stateful logic into a "hook", and use it multiple times.
	- Think of the example of an "input" hook, that exposes a state, a state setter - but has a "blackbox" of validation-level logic that would be really annoying to copy+paste.

## Static Use Order
- Hooks have 2 very important rules about their use:
	1. Hooks can only be used within a React function
	2. Hooks can only be used at the *top-level*

- Hooks in non-React functions makes very little sense, as they cannot have state
- Hooks also must be in the top-level, almost like we are defining some property on the *class*, like this component *has* state, and is not contingent to conditional logic or looping.

# [Complete Guide to useEffect](https://overreacted.io/a-complete-guide-to-useeffect/)
- This piece comes with such a good insight into the effect mental model:
> **It’s only after I stopped looking at the `useEffect` Hook through the prism of the familiar class lifecycle methods that everything came together for me.**

## Each Render has its *own* props and state
- Stateful variables are not anything more than variables
- Any updates to stateful variables - through `NON-MUTATING` functions and the `setState` interface, React then takes those updates and re-renders the UI
	- It does so by *invoking your functions* with the *new* changes in stateful values.
> A render is a snapshot in time, with the new states

## Each Render has its own event handlers
- Since a render is a *snapshot* in time, any event handlers - regardless of their timing/synchronicity - are based on the render cycle
	- If we have an event handler that sets a `timeout` and uses a stateful value, the stateful value it uses is based on the render that it was created on
	- This is because within a render, the *value* of a state/prop is essentially *constant* for that render - meaning that any references to state within asynchronous/timed functions don't use the "latest" value of state, but rather the *constant* value of the state. The function is instantiated with *that* value, and does not re-evaluate the value of the state.

```js
function sayHi(person) {
  const name = person.name;  
  setTimeout(() => {
    alert('Hello, ' + name);
  }, 3000);
}

let someone = {name: 'Dan'};
sayHi(someone);

someone = {name: 'Yuzhi'};
sayHi(someone);

someone = {name: 'Dominic'};
sayHi(someone);
```
> This is an example of a *closure*, where the `name` variable *inside* (closed under) the `sayHi` function means that the closed name will be "remembered" across calls - it does not try and look outside for the *new* value of name. This is precisely why *state* within React works this way as well. The value is *captured* at the time of execution.

> [!note] This is also exactly why React functions should be *pure*, by avoiding ANY functions that mutate state/variables *directly* in-place. These direct mutations to state mean that the change is not done through React, and create unpredictable rendering outcomes.

## Each render has its own *effects*
- The stateful variables don't change within "static" effects - the effects are re-created, they are *new* every render, so the state  doesn't need to change for effects, as effects change for states.
- Effects run *after* re-paints (commits), in which it will be represented by a different function on every render, which then can "see" the new props/state from the render it "belongs to"
	- Meaning that the result of the function of the effects depends on the render - it is inherently attached.

## Each render has its own *everything*
- This is opposed to *class-based* components with `componentDidUpdate` lifecycle, in which `this.state.count` will always *point* to the *latest* value - which can be changed to mimick the behaviour of "captured/snapshot" values using *closures* (as the functional effects do)
	- Closures make it easier to "think" about (wrap your head around) the idea of changing values in the event loop - as they essentially make the global scope into a local, private one with a *constant* value.
- Therefore, all functions within a component's render (event handlers, effects, timeouts, API calls) *capture* the props/state of *that specific render*, as the component itself is a function, and thereforce, a closure.

- If we *do* want to read the *latest* value, we can use **refs** (direct references) to assign mutable variables that we can do *whatever* with.

## Cleanup, Cleanup
- Cleanup phases within effects are meant to *undo*.
	- Common for subscriptions (stores, APIs, eventListeners, etc...):
```js
useEffect(() => {
	ChatAPI.subscribe(props.id, handleChange)
	
	//cleanup
	return () => {
		ChatAPI.unsubscribe(props.id, handleChange)
	}
})
```
> Effects run *after re-paint*, and the cleanup always runs *before* the setup code (unless it's the first effect firing on mount, since there's nothing that's been done to *clean-up*).

> This cleanup may muddy the idea that the `props.id` value is the "latest" one - because the `props.id` within the cleanup is the *previous render's value*, which kind of goes against what goes mentioned before.
> However, it really still does use the constant value in both - it's just that the cleanup runs first, from the previous render - and a *new* effect function is "created" and the *new* functions setup is run.

> Update > Render > Commit > Effect A Setup > Update > Render > Commit > Effect A Cleanup > Effect B Setup > Update > Render > Commit > Effect B Cleanup > Effect C Setup

## Synchronization, NOT Lifecycle
- React is *declarative*, it's about the **destination**. Imperative APIs are about describing *how* we get to the destination (the journey). In jQuery and JS DOM APIs, we imperatively call `.appendChild` to add a child element to the DOM, while in React, we declaratively describe what we want the UI to look like, and React will handle the code to add, remove, and mutate the UI.
- React synchronizes the DOM (or the host tree) according to props and state, and in terms of rendering, there's no difference between a *mount* and an *update* for reconcilliation.

- Effects are *meant* to *synchronize* outside of the React tree, according to changes in state. 
	- If we try to achieve the `mount/update/unmount` lifecycle, we are starting to become *imperative*, relying on the "journey".

## "Diffing" effects
- We can specify *dependencies* of our effects, which allow us to tell React what state/props are used within the effect
	- This is because without invoking the effect itself and checking the difference between the last effect and current effect result - React cannot know if the outcome has changed.
	- Dependencies tell React (as if a pinky promise) that the effect depends on a specific state, and will only re-render when it knows that the state(s) have changed

## Dependency Fibbing
- When we don't specify the *correct* set of dependencies, it will often lead to big problems
	- It's not that we *lied*, but can also be due to using the incorrect mental model of effects
- This is further cemented by my own personal experience, but creating "global" functions to fetch data, and referencing them within an effect as a way to achieve `fetch-on-mount`, is not correct:

```js
async function fetchData(){}

useEffect(() => {
	fetchData();
}, [])
```
> This is bad, and the reasons why are a lot bigger than just this example. For now, it's because we *use* a "global" value from the component, so it needs to be specified in the deps (functions, states, variables, etc).
> - Essentially, anytime you define something *outside* an effect, and it's used *inside* the effect, we need to specify it as a dependency.

### Why Dependencies?
- It's more obvious when the outcome relies on visual updates, if we *don't* specify a state as a dependencies - any changes to it don't re-trigger the effect
- Again, thinking about effects is obscured by the perspective of class component lifecycles. You would only want to run something *on mount*, which might be functionally equivalent to `[]` deps, but if your effect relies on some states - then the state is not 

> The important thing to remember about `class` vs. `functions` in terms of components, is about objects. Classes and objects are related, we create "instances" of classes which are objects, and they exist in some runtime, constantly mutating, and they have a *lifecycle* associated with them (created, mounted, unmounted, destroyed, etc.). Functions are *not* instanced, but rather *invoked*. They tell React what to render based on functional logic within them. Hooks allows us to use the React Tree to maintain state (and various other things ...) outside of the scope of the function itself, but are NOT actually part of the "component" itself. TL;DR: Functions are invoked, Classes are instanced, which allows objects as instances to "persist", but functions are invoked to produce a result.

> This "mental hurdle" is what's been plaguing me as a React developer - because I started very briefly with components, but then moved into the idea of lifecycles. The React docs (legacy) made it quite unclear that hooks and lifecycle are not related. It has seriously been such a difficult journey, and I feel like an absolute moron to read through these well-written pieces about React architecture. It's humbling honestly.

```jsx
	function Counter() {
	  const [count, setCount] = useState(0);
	
	  useEffect(() => {
	    const id = setInterval(() => {
	      setCount(count + 1);
	    }, 1000);
	    return () => clearInterval(id);
	  }, []);
	  return <h1>{count}</h1>;
	}
```
- Here's an example of this, we want to initalize and use an interval to increment the *count* state once every second
	- However, since this effect never re-runs, the update is effectively doing `setCount(0 + 1)` every interval tick, because it does not use the new state.
	- Obviously, the solution to this is to include the state it depends on in the dependencies: `[count]`.
		- However, everytime the effect runs, the interval is cleared and reset with the *new* value of count, so count updates, but at the cost of clearing and setting a new interval. This might be fine in some cases, but in others, not acceptable.
	- Another solution is to not make the effect reliant on *any* variable - which is counter-intuitive, because we are setting a state.
		- This logic is the standard, but in the case of state setters - we can provide an updater *function*:
			- `setCount(c => c + 1)`, which now actually relies on no state, because it describes how to update the state, instead of imperatively setting the state to a literal using a "constant" state 
				- (*constant, within a render*)
			- This is not "lying" about dependencies, but rather is working to remove them, because the update no longer relies on the concrete value of the state. It just instructs React to update the state using this function and set the state to it's return.

## Functional Updates
- Synchronization is the correct mental model for utilizing effects well, not lifecycle changes - because functions don't persist like objects of classes do, and have no "lifecycle" other than it's invocation.
- When we synchronize between two (or more) things, we want to keep messages untangled from the "state".
	- In the example of Google Docs, whenever a user makes a change, it doesn't send the *whole* document to all other users to sync their view - but rather some "action".
		- It's very much like a game - every tick of a game server, the server does NOT pass ALL data back-and-forth, it sends back specific information about actions each player does, to keep their games in sync with each other, which each client is responsible for making sure that it "replays" those events
- Now, think about the difference between 
	a. `setCount(count + 1)` 
	b. `setCount(c => c + 1)`
	- example A is a concrete, imperative way to set the count equal to `<current count = 0> + 1`, while B describes the action itself, irregardless of the value of count. Essentially, it says "add 1", and is not attached to any particular render.
- The point being is that we send *minimal necessary information* from inside effects into components. Encoding the *intent* of the, rather than an imperative operation on state, is how we can very easily solve problems about collaborative synchronization (as in Google Docs).
	- This way, we don't have to worry about which states change, because we build an API *on-top* of the state, to create actions to impose, rather than focusing on granular state changes.
		- This is what the `useReducer` hook is based on.

## Decoupling Updates from Actions
- When setting a state depends on the value of *another state*, then it starts to more of an action rather than an update. We can do so with `useReducer`.
	- It decouples the "actions" from the state updates and makes a user's intent more semantic, especially when their action creates some "cascade" of updates with state.

- A *reducer* is a function that specifies how to deal with actions.
```js
const [state, dispatch] = useReducer(reducer, initialState)
```
> Through the `userReducer` hook, we provide a reducer *function*, and it passes us the state (similar to `useState`). However, instead of a direct setter to the state, it passes back a "dispatcher" function, which passes some "action" to the reducer, and the reducer then decides what to update based on the action's properties
> - an action is a simple JS object, commonly carrying a `type` property to differentiate actions, and can include any other type of property (information payload, etc)

```jsx
useEffect(() => {
  const id = setInterval(() => {
    dispatch({ type: 'tick' }); // Instead of setCount(c => c + step);  }, 1000);
  return () => clearInterval(id);
}, [dispatch]);
```
- It's important to note that in this example, we specify the dispatch function as a dependency because it's created outside of the effect.
	- However, it's not necessary to do so - **because React knows that `dispatch`, `setState`, `useRef` containers are STATIC**, so it's possible to omit them.
- So, instead of creating effect dependencies through states, we can now seperate the concerns of this interval, with the state - because the interval only dispatches actions irregardless of stateful values.

```jsx
const initialState = {
	count: 0,
	step: 1
}

function reducer(state, action) {
  const { count, step } = state;
  if (action.type === 'tick') {    
	  return { count: count + step, step };  
  } else if (action.type === 'step') {
    return { count, step: action.step };
  } else {
    throw new Error();
  }
}
```
- We can then "decouple" actions from state. 

### Why does this work?
- Because React then has a history of actions, and a function to handle actions.
- React can call reducers whenever it has time during the next render

## Functions within Effects
- It's definitely possibly to use functions within effects defined outside of the effect - the problem lies in whether or not that function depends on state
	- Functions *within* the scope of a component are *different every re-render*, and specifying them as deps can lead to effects too many times.
		- Likewise, not including them as effect deps means that effects don't re-run on changes, AND presents a hole in the logic if we ever add changes to the data flow (we must *remember* to change the deps to be correct, if not - a bug appears).
	- If a function does *not* rely on state, it means that it's kind of like an operator, it bundles some logic, calculation and output - we can *hoist it up*, outside of the component.
		- Think of a function that returns an RBG color when giving a HEX color.
		- This means that the function itself is *static*, and not "re-created" every render, so it's OK to use in effects (we *explicitly* define it as static)
	- OR, we can `useCallback` hook.
		- This hook is essentially a "memoization" of a function - the *identity* of the function is preserved based on dependencies.
			- If the dependencies of the callback change, then a *new* function is created with a different *identity*

RECAP:
```js

// STATIC function
// OK to use without specifying as a dep - it never changes identity
const getURL(query){}

function Search(){

	// 🔴 function depends on STATE (q), but effect deps cause no re-trigger 🔴
	const [q, setQ] = useState('')
	function getURL(q){}	
	useEffect(() => {
		async function fetch(){
			await axios(getURL())
		}
		fetch()
	}, [])

	//✅ OK, since effect is a closure and state changes re-trigger effect ✅
	const [q, setQ] = useState('')
	useEffect(() => {
		function getURL(){}	//depends on STATE (q)
		async function fetch(){ 
			await axios(getURL())
		}
		fetch()
	}, [q])

	// function is shared - too tedious to isolate individually
	// within the render scope - will change identities
	// 🔴 all effects are re-triggered every render 🔴
	function getURL(query) {}
	useEffect(() => {}, [getURL]) //a
	useEffect(() => {}, [getURL]) //b

	//✅ PERFECT, since function only changes identity when dependencies change (never) ✅
	// since the callback does NOT rely on state - it does not need to be re-created
	const getURL = useCallback((query) => {}, [])
	useEffect(() => {}, [getURL]) //a
	useEffect(() => {}, [getURL]) //b

	//✅ PERFECT, since function only changes identity when dependencies change✅
	// callback relies on STATE (query), changes to query re-create function, re-firing effects
	const [query, setQuery] = useState('')
	const getURL = useCallback((q) => {}, [query])
	useEffect(() => {}, [getURL]) //a
	useEffect(() => {}, [getURL]) //b
}

```

# [UI Engineering Principles](https://overreacted.io/the-elements-of-ui-engineering/)
## Consistency
- Local consitency of visual elements
- Persistent state between pages, transitions
- Consistency between the client and the server for events
- When do we opt in to checking the server to synchronize the client?
## Reponsiveness
- Continous actions (gestures/scroll), low limit on lack of visual feedback
- Discrete actions (click), higher limit, < 100ms delays are equally fast, any longer and there needs to be some visual indicator
	- layout jumps, several loading stages can make it feel longer
## Latency
## Navigation
## Staleness
## Entropy
## Priority

## Accessibility

## Internationalization (i18n)

## Delivery

## Resilience

## Abstraction


## [Data Fetching with Effects](https://www.robinwieruch.de/react-hooks-fetch-data/)



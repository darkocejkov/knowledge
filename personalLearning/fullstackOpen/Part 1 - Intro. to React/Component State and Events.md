## Helper Functions
There are many cases in which a component we create ingests some data and displays it. The really interesting part of JS is that we can define functions within our components (*almost* like methods) that can help us *calculate* something. It's more-or-less to support organization and re-usability. If the function had to be manually defined in *multiple* components, then it makes sense it would be best to globalize the function even further.

# Rendering
Given that React comes in-built with the following behaviour:
```jsx
ReactDOM.createRoot(document.getElementById('root')).render(
	<App counter={counter} />
)
```
It would make sense that if you want to "re-render" the page with new values, you could just call this function over and over, or perhaps on a timer?

That is one possible method, but is an *anti-pattern* and is not recommended by React on triggering re-renders. 
React is a UI engine that allows you to create *stateful* variables, and provides you (the programmer) a way to define how to programmatically manipulate stateful variables through the React API. 
From [[React]], the engine of React is a very special change tracker. You setup JSX elements that display, you set up event *handlers* on those elements that respond to change, and you set states. React listens to those changes, and triggers re-renders automatically and only does so on DOM elements that have been changed.

# States & Hooks
- We use functional **hooks** to create additional, reusable functionality. 
- React comes with certain hooks that are core to React principles, like **states** and **effects**.

## Complex States
- In general, avoid creating large objects to hold state in various properties.
	- This might seem simple and intuitive, and a lot easier than creating multiple `useState` hooks, but is a detriment.
		- Since objects can be nested, React's state-change comparison starts slowing down the deeper objects are nested. Use flat objects.
			- As mentioned in [[React]], we can use the library `Immer` to simplify how we manipulate state.
- Generally, only "group" states into (flat) objects if they ONLY change at the same time.
	- for example, an $x$ or $y$ coordinate. 
	- If your states are independent, keep them seperate. It's more code, but overall MUCH easier to manage.
- Again, only use object methods that return new objects - we treat React stateful variables as immutable and let React do the mutating.

## Asynchronous Updates
"Renders" are done in cycles. If you are attempting to set a state, then immediately read the new state right after you set it - you won't get what you expect.
- This is because when states are set, it triggers a re-render, and the stateful variables are *only* mutated on the *next* render, like a "snapshot" in time.
- There is no definite time that renders take, we do not know when (in time) renders happen, and even *how long after* we set states
	- React attempts to group or "batch" state updates into a single re-render, to limit the number of re-renders.

## Conditional Rendering
- Can use functional programming conditional logic to *return* a different result from functions
- Or, can "embed" the condition JavaScript *within* the JSX.

## Hooks?
Hooks are special functions that implement *logic*. They are *independent* of JSX, and should only implement the logic between stateful values and effects.

### Rules
- Must be called at the *top-level* of a function (component OR other hooks)
	- Not in any loops or conditionals
		- these are *not* top-level scopes because they define sub-level blocks with the function. Also, it doesn't make much sense to loop hook functionality.

Instead of thinking of hooks as "variables", think of them like "packages".

> Hooks are *not* implementations that are meant to *mirror* class-based behaviours - like `componentDidMount()`, they are implementations that eliminate having to use (or think like we are using) class-based components.

## Events & Their Handlers
We can create *event handler* functions in whatever way we like and pass them to the corresponding Event attribute for corresponding JSX elements.
- Event attributes expect functions or references to functions
	- If functions trigger re-renders as part of their invocation, they cannot be invoked like this: `onClick={handleClick()}`
		- The only time this is acceptable is if the *return* of `handleClick()` is a function.

## Parent and Child states
- In the case of React component hierarchies, what we want to do is create a composition of parent and child components.
- If a state exists that should be *shared* between children, that state should be "lifted up" to the parent, which can pass down the value of the state.
- Children should "bubble up" events by some way of shared event handler from the parent.

![[Pasted image 20230328170914.png]]
> In this case, children that want to reflect the *same* state should have their states be common to their closest ancestor.
> - i.e., the stateA must be in the Parent state, passed down to the component
> - Thus, since component A does not control the state directly, any events that should change the state should not directly manipulate, but rather propagate that event up.
> 	- The ideology of "Parent handles, child displays"
> 	- Do not attempt to hold the state within the children, and try and "sync" states between children using state functions - it doesn't work, a flawed design.
> Otherwise, if a component does not need its state to be synced between siblings, it can control its own state

## Components within Components
- Defining components *within* other components is a recipe for bad design
	- First of all, any renders consider these sub-components as new, unique components and cause so many re-rendering issues with states, and goes against the entirety of React design principles

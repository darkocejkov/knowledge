Summarizing and explaining how to use all the hooks bundled with React
___
# Hooks

## `useCallback`
[Reference](https://react.dev/reference/react/useCallback)

```js
const callback = useCallback((params) => {}, [deps])
```

- *cache* a function definition between renders
	- This is necessary because all render-scoped variables and functions are "re-created" in the render phase
	- similar to [[#`useMemo`]], except it "memoizes" the **identity** of a function

- the identity changes based on if the *dependencies* change, because it fundamentally changes the stateful values captured
	- this is general to JavaScript, function calls `() => {}` or `function() {}` always return *new* functions
- it's specifically useful because if we pass down a handler to a child, the handler *function* will always count as a "new" or "different" prop everytime
	- this means that in order to optimize heavy renders, we must use this hook to only create new, state-dependent functions when they are *needed*
		- really only needed when we are performing more wide-spread optimization through *memoization* - so we must wrap expensive functions to work properly with memoization.
		- also, React recursively re-renders children on parent updates for reconcilliation - so any functions defined *not* in `useCallback` are then created anew.

## `useContext`
[Reference](https://react.dev/reference/react/useContext)

```js
const object = useContext(ContextObject)
```

- *subscribe* to a specific context within a component
	- the single parameter to this hook is a context object created from `createContext`
- the "context" is the *nearest* Provider component, if none, then the default context (from the `ContextObject` defined in the `createContext` call)
	- this hook returns whatever is stored in the context
		- object, primitive, array, etc.
- any components that use/read contextual state are treated like direct stateful readers
	- any children of Providers that have a change to stateful context values will automatically be re-rendered

```jsx
const ThemeContext = createContext('light')

return(
	<ThemeContext.Provider value="dark">
		<Form />
	</ThemeContext.Provider>
)

const Form = () => {
	const theme = useContext(ThemeContext)
}
```
- `useContext` looks for the *first* Provider to take from that context.

## `useDebugValue`
[Reference](https://react.dev/reference/react/useDebugValue)
```js
	useDebugValue(state ? 'State is True/Exists' : 'State is False/DNE')
	useDebugValue(date, date => date.toDateString())
```
- meant for *custom hooks*, so that we can add debugging labels to the React DevTools
- we can pass a value as the first argument, and an optional formatting function that is applied to the first value

## `useDeferredValue`
[Reference](https://react.dev/reference/react/useDeferredValue)

```js
	const [query, setQuery] = useState('')
	const deferredQuery = useDeferredValue(query)
```

- *defer* updating part of the UI
- inital render returns a deferred value of the initial value
- updates to state mean that the deferred value "lags" behind the *latest* change in value
	- React re-renders *without* updating the deferred value, then re-render with the *new* value in the background
- it's most obvious when using `<Suspense>` and a fallback. 
	- Changes to state, like a search query cause the data flow to be put into loading states. We can use the deferred value to create a previous query state to use
- we can also compare the current query and the deferred value to see when the deferred query is "stale"

## `useEffect`

```js
useEffect(callback, deps)
useEffect(() => {
	//setup
	return () => {
		//cleanup
	}
}, []) //deps
```

- create an *effect*, meant for *synchronizing* component state/prop to some external system
	- these effects are *side-effects*, because they respond to changes in state/prop to allow for syncing, and not logical implications between React states
		- [[React#Poor use of effects exemplified:]]
	- the entire point of effects is to allow other systems that *don't* participate in the React data flow, to react to changes in props/state.
		- they are *escape hatches* for external functionality - to use DOM APIs directly, connecting to a server
- Order of effect:
	- (mount)
		- setup
	- (re-render + dependency update)
		- cleanup
		- setup
	- (unmount)
		- cleanup
- [[Advanced React (I❤️DAN)#Effects]]

## `useId`
[Reference](https://react.dev/reference/react/useId)
```js
	const id = useId()
```
- generates a *unique ID* for a particular hook invocation
	- it is *not* meant to generate keys for dynamic list rendering
		- keys of a list should be generated by the *data* within the list
	- it is *meant* for generating unique IDs for DOM attributes, like the `id` attribute, instead of needing to create a unique static string: `<p id='password-hint'>`, which creates conflicts if *more than one component* is rendered, because IDs should be globally unique

## `useImperativeHandle`
[Reference](https://react.dev/reference/react/useImperativeHandle)
```jsx
export default function Form() {
  const ref = useRef(null);

  function handleClick() {
    ref.current.focus();
    // This won't work because the DOM node isn't exposed:
    //ref.current.style.opacity = 0.5;
  }

  return (
    <form>
      <MyInput label="Enter your name:" ref={ref} />
      <button type="button" onClick={handleClick}>
        Edit
      </button>
    </form>
  );
}

const MyInput = forwardRef(function MyInput(props, ref) {  
	const inputRef = useRef(null);  
	useImperativeHandle(ref, () => {  
		return {  
			focus() {  
				inputRef.current.focus();  
			},  
			scrollIntoView() {  
				inputRef.current.scrollIntoView();  
			},  
		};  
	}, []);  
	
	return <input {...props} ref={inputRef} />;
}, []);
```
- customize a *handle* that is exposed as a *ref*, used in conjunction with [[#`forwardRef`]]
	- a *handle* is a way to initalize that ref to *expose* methods and properties of that ref, instead of passing the *entire* DOM node
	- as is seen in the example, this is quite useful for dealing with those edge-case components, uncontrolled inputs which are controlled by the DOM rather than states.

## `useInsertionEffect`
[Reference](https://react.dev/reference/react/useInsertionEffect)
> [!note] This is a hook made for `CSS-in-JS (aka JSS)` reasons - unless you are doing so, it's most likely you want [[#`useEffect`]] of [[#`useLayoutEffect`]].
- An *effect* that fires *before* DOM mutations

## `useLayoutEffect`
[Reference](https://react.dev/reference/react/useMemo)

```jsx
export default function Tooltip({ children, targetRect }) {
  const ref = useRef(null);
  const [tooltipHeight, setTooltipHeight] = useState(0);

  useLayoutEffect(() => {
	const { height } = ref.current.getBoundingClientRect();
	setTooltipHeight(height);
	console.log('Measured tooltip height: ' + height);
  }, []);

  let tooltipX = 0;
  let tooltipY = 0;
  if (targetRect !== null) {
    tooltipX = targetRect.left;
    tooltipY = targetRect.top - tooltipHeight;
    if (tooltipY < 0) {
      // It doesn't fit above, so place below.
      tooltipY = targetRect.bottom;
    }
  }

  return createPortal(
    <TooltipContainer x={tooltipX} y={tooltipY} contentRef={ref}>
      {children}
    </TooltipContainer>,
    document.body
  );
}
```
[In-depth Example](https://codesandbox.io/s/bj8hpt?file=/Tooltip.js&utm_medium=sandpack)

- An *effect* that fires before the browser *re-paints* the screen
	- it can negatively affect performance if used inappopriately or too often
	- it can also include a cleanup function, that works in the same way that [[#`useEffect`]] does.
- it is most often used to perform *layout measurements* before the browser re-paints the screen, so it's possible to check whether or not certain components/elements are where they *should* be, or how to draw them based on the current layout of elements
- A core difference in this and `useEffect` is that `useLayoutEffect` *blocks* the browser from re-painting, so any state updates will cause the current render to "throw away" and start anew, based on the new states
- Here's a breakdown of how rendering, layout, and re-painting works:
	- components only decide *what* to render, not any of the details of layout or size - the browser handles that and calculates layout, size, and repaints on those calculations.
	- what if a component we want to declare in React, like a tooltip, needs to know if it *fits* on the screen without clipping the edges - and what the best place to render is?
		- in this scenerio, we need to render this component in TWO passes:
			- render anywhere, even in the "wrong" place
			- measure height of content
			- render again, in the correct place
	- this all needs to happen *before* the browser re-paints, otherwise we can *see* the layout and rendering changes (even if it happens really fast - it still happens)
		- this is exactly what happens when we opt for `useEffect`, because the browser renders, re-paints, we calculate, then issue another render, re-painting.

## `useMemo`
[Reference](https://react.dev/reference/react/useMemo)

```js
import { useMemo } from 'react';  

function TodoList({ todos, tab }) {  
	const visibleTodos = useMemo(  
		() => filterTodos(todos, tab), //computing function (calculateValue)
		[todos, tab]   //deps
	);  
	// ...  
}
```
- a hook that *memoizes* a calculation
	- similar to memoizing components with `memo()` and memoizing the identity of functions with `useCallback`, this hook allows you to memoize values
	- use it when calculating or computing auxillary values. the calculations themselves might not be "expensive", but if those calculations depend on states that don't change often - there's no point in always re-computing those values if the dependencies *don't* change.
		- the `calculateValue` function should be pure, and take *no arguments*
- recall back to algorithms, most are very fast at low input (n), but certain complexities grow much faster than others. Transforming a list is fast for small n, and if there's a possibility to have large *n*, then we need to optimize when necessary, premature optimization leads to even *more* bugs.

## `useReducer`
[Reference](https://react.dev/reference/react/useReducer)

```js
import { useReducer } from 'react';  

function reducer(state, action) {
  if (action.type === 'incremented_age') {
    return {
	  ...state,
      age: state.age + 1
    };
  }
  throw Error('Unknown action.');
}

function MyComponent() {
	//const [state, dispatch] = useReducer(reducer, initialArg, init?)
	const [state, dispatch] = useReducer(reducer, { age: 42 });
	
	function handleClick() {  
		dispatch({ type: 'incremented_age' });  
	}
}
```
- sets up a *reducer* state manager
	- a "reducer" is a function that specifies *how* state is updated (pure, based on "actions", returns the *next* state)
		- the "state" and "action" can be of *any* type
	- the `initialArg` parameter is the initialization argument passed to the option `init` function, if no `init` function is specified, then the value of `initialArg` is used (as in the initial "state"). the `init` function is meant to be a transform function of some sort.
- this is a seperate *paradigm* of managing state, instead of creating granular single stateful variables with [[#`useState`]], we create a "store", which is of any type - it can be an object, a number, a string. The point is that 
- we update state through the *dispatch* function that is passed by the hook, which allows us to send *actions* to the reducer.
	- it's not obvious why we would use this to manage a *single* stateful variable, like age, but becomes much more important when we have multiple states that change at the same time based on a single *event* - which is interpreted as an *action*.
	- in the example, when the reducer receives an action with the type `incremented_age`, it can decide what the resulting change in state is. here, it's simply adding $1$ to the `age` property of the state store, but in other examples it might increment other properties that correlate, like a calculation of approx. birth year which happens at the same time the age changes
- similar to `useState`, never *mutate* values directly, we always return a *new* object. 
	- if this returned object is the *same* (based on the `Object.is` comparison), then React skips re-renders

## `useRef`
[Reference](https://react.dev/reference/react/useRef)

```js
const ref = useRef(initialValue)
```
- a *ref* is a direct reference to some variable that is *not* needed for rendering React elements, but persists through renders
	- the *value* stored in a ref is always accessed through the `.current` property
	- values are *mutable* if they are *not stateful*
		- however, it is very much recommended to *not* read/write from/to the value of the during *during rendering*, because it makes the value within the ref unpredictable, and thus decreases the *purity* of the component
			- reading and writing from/to refs should occur in event handlers and effects
	- changes to a ref's value do not trigger re-renders
- common uses of *refs* is for holding *interval IDs*, creating direct references to DOM elements and nodes
```jsx
const inputRef = useRef()
return <input ref={inputRef}/>
```
- attaching the ref to a React *element*, will create a direct reference to the DOM element, for which we can access like DOM APIs (`.focus`, etc.)

- the contents of the ref should be stable, and sometimes you might need to create objects to store in the ref:
```js
	const playerRef = useRef(new VideoPlayer())
```
- in this snippet, we initialize the ref to the return of `new VideoPlayer()`. the return is only used to intialize the ref on the **first** render, but on re-renders it continues to call the initialization, and does *not* use the return.

```js
	const playerRef = useRef(null)
	if(playerRef.current === null) playerRef.current = new VideoPlayer()
```
- so, it's much more efficient to write to the ref *after*, during rendering
	- even though we *shouldn't* read/write to the ref during a render, it's OK in this case because the result is predictable, based on the initial value

- In order to pass a ref to other components (children), we need to declare those children with [[#`forwardRef`]]

## `useState`
[Reference](https://react.dev/reference/react/useState)

```jsx
	const [age, setAge] = useState(28);  
	const [name, setName] = useState('Taylor');  
	const [todos, setTodos] = useState(() => createTodos());
```
- adds a *stateful variable* to the component
	- a stateful variable is one in which is:
		- saved between renders
		- changing stateful variables (via the provided *setter*) causes re-renders
			- as opposed to *ref* which do not participate in the data flow
- it can be passed any type of value (number, object, string, function)
	- when passed a function, it is an *initializer function* 
	- if we *invoke* a function, rather than *pass* it, then it runs on *every* render, but stores the value of the function only on the *first* render.
- it's extremely important to:
	- *never* mutate the state directly
		- any methods that mutate the value are forbidden
			- unless you are using something like `Immer`.
	- always update the state through the provided setter function

- here are some ways we can update a state:
```js
	//age = 28
	setAge(age + 1) //28 + 1 = 29
	setAge(age + 1) //28 + 1 = 29
	setAge(age + 1) //28 + 1 = 29
	
	setAge(x => x + 1) //28 => 28 + 1 = 29
	setAge(x => x + 1) //29 => 29 + 1 = 30
	setAge(x => x + 1) //30 => 30 + 1 = 31
```
> we can pass the updater a *single* value. this is very common, and satisfies most constraints. however, in the example, if we want to update the age state 3 times, can that see in the comments that it goes against our expectations. the "age" doesn't update value until the *next* render (more about this in [[Advanced React (I❤️DAN)#Batching]]).

- You *can* call state setters during a render, which causes React to immediately throw out the current render, and re-render
	- any time you *do* call setters during a render, they *must* be in some conditional logic to avoid being *infinitely called*.
	- it is more efficient to call during a render because of this *early exit*, rather than setting state in an *effect*, because effects run *after* a commit & re-paint, creating a re-render after a full render *just* happened.

### Resetting State
- State is based on the *position* of an component in the tree. If a component changes position (relative to it's siblings and parent) then the state resets. This is because React "keys" our components based on the position in the element tree.
	- We *can* pass an explicit `key` attribute to elements/components to tell React to identify component based on the key rather than the position - changing the key means that we can reset state.

### Controlled Components (Inputs)
- When dealing with `<input />` elements, it's important to note that if we want to *control* the internal state of these components using React's state - we should not initialize the React states to be *null*:

```jsx
const [state, setState] = useState(null)
return(
	<input value={state} onChange={setState}/>
)
```
- This is because when the *state* is null, then React thinks the component is *uncontrolled*, and assigning values to it, making it non-null, makes React think it *is controlled*.

## `useSyncExternalStore`
[Reference](https://react.dev/reference/react/useSyncExternalStore)

```jsx
export default function TodosApp() {

//const snapshot = useSyncExternalStore(subscribe, getSnapshot, getServerSnapshot?)
const todos = useSyncExternalStore(todosStore.subscribe, todosStore.getSnapshot);
return (
	<>
	  <button onClick={() => todosStore.addTodo()}>Add todo</button>
	  <hr />
	  <ul>
		{todos.map(todo => (
		  <li key={todo.id}>{todo.text}</li>
		))}
	  </ul>
	</>
);
}
```
- creates a *snapshot* of data in an "external store", with the ability to run subscription (+cleanup) code
	- the details of an "external store" are quite abstract. it's a little clearer to think of *state* an an *internal* store, it's interal to React specifically. Certain APIs can be considered "stores":
		- [This article](https://thisweekinreact.com/articles/useSyncExternalStore-the-underrated-react-api#link1) explains further - if we think about the `react-router` library, the `useLocation()` hook is an "external store" for the browser's history API. It's also true for the browser DOM API, for things like `scrollY`.

```js
function subscribe(onStoreChange) {  
	global.window?.addEventListener("scroll", onStoreChange);  
	return () =>  
		global.window?.removeEventListener(  
			"scroll",  
			onStoreChange  
		);  
}  
  
function useScrollY(selector = (id) => id) {  
	return useSyncExternalStore(  
		subscribe,  
		() => selector(global.window?.scrollY),  
		() => undefined  
	);  
}

function ScrollY() {  
	const scrollY = useScrollY();  
	return <div>{scrollY}</div>;  
}

function ScrollYFloored() {  
	const to = 100;  
	const scrollYFloored = useScrollY((y) =>  
		y ? Math.floor(y / to) * to : undefined  
	);  
	return <div>{scrollYFloored}</div>;  
}

```
- Instead of trying to add `scrollY` into the typical data flow of react states, we can synchronize the data flow (without effects) by "subscribing" to this "store". The subscribe function is merely the instruction of what to do to subscribe, for the DOM API's case, it's adding an event listener to the *window* for the `scroll` event.
	- for `ScrollYFloored`, the hook we create specifies a function to pass to the 

## `useTransition`
[Reference](https://react.dev/reference/react/useTransition)
```js
	const [isPending, startTransition] = useTransition();

	function selectTab(nextTab) {  
		startTransition(() => { //"scope"  
			setTab(nextTab);  
		});
	}
```
- update state without blocking the UI
	- `isPending` is a flag that indicates if a pending transaction is occuring
	- `startTransition` is a function to mark a updates as a "transition"
- the function that's passed to `startTransition` is called the scope - which updates state by calling 1+ *setter* functions
	- all executions within the scope must be *synchronous*, otherwise they won't be marked as transitions
- state updates that are marked as "transitions" can be *interrupted* by other state updates
	- if `setA` is a transition update, and some other event/action occurs, like `setB`, then `setA` is interrupted on the current render to immediately handle `setB`, for which it will start re-handling `setA` afterwards.
- Why use this? because the UI stays responsive during the re-render.
	- If we have some "transition" like switching tabs, and we switch to a tab that causes non-responsiveness, then the UI does not "freeze"
		- It's very obvious when this is needed, because clicking on buttons that require heavy computation/loading freeze the *rest* of the UI
	- furthermore, since we are returned the `isPending` flag, we can use this to display the pending state of this transition update

# APIs
## `createContext`
[Reference](https://react.dev/reference/react/createContext)
```jsx
import { createContext, useContext } from 'react';  
const ThemeContext = createContext('light');
const AuthContext = createContext(null);

function App() {  
	const [theme, setTheme] = useState('light');  
	const [user, setUser] = useState({username: 'Joe'})
	// ...  
	return (  
		<ThemeContext.Provider value={theme}>  
			<AuthContext.Provider value={user}>  
				<Page />  
			</AuthContext.Provider>  
		</ThemeContext.Provider>  
	);  
}

function Page(){
	const theme = useContext(ThemeContext)
	const user = useContext(AuthContext)
}

```
- creates a Context "store", that has a `.Provider` component wrapper
	- the Provider wrapper passes the context down to *all* of its children, and their children
- only components that *subscribe* to the context with `useContext` are considered in reconcilliation to changes in contextual state
- the value passed to `createContext` is the *default* value
	- when a compent wants to read the context, through `useContext`, it looks for the **nearest** parent provider. If there is none, it uses the default value.
		- if there are *multiple* parent wrappers for the *same* context, it uses the *first* one.
- the value of a context can be *anything*, number, string, object, function.
- the purpose of having more than one context, is that we can seperate them from objects that don't need them
	- perhaps all buttons, tooltips, and text components need the *theme* context, but don't need the *authentication* context

## `forwardRef`
[Reference](https://react.dev/reference/react/forwardRef#render-function)
```jsx
function Form() {  
	const ref = useRef(null);  
	function handleClick() {  
		ref.current.focus();  
	}
	return (  
		<form>  
			<MyInput label="Enter your name:" ref={ref} />  
			<button type="button" onClick={handleClick}>  
				Edit  
			</button>  
		</form>  
	);  
}

const MyInput = forwardRef(function MyInput(props, ref) {  
	const { label, ...otherProps } = props;  
	return (  
		<label>  
			{label}  
			<input {...otherProps} ref={ref} />  
		</label>  
	);  
});
```
- allows the component to expose a DOM node to a parent using a *ref*
	- the parent controls the *ref*, passes the ref down to the child, and the child can attach the ref to a DOM node that it renders, while the parent can reference the *same* node.
- it takes a *rendering* function as the first argument, and passes that renderer the *props* and the *ref*

## `lazy`
[Reference](https://react.dev/reference/react/lazy)
- defer loading component's code until it's rendered for the *first* time
```jsx
//const <component> = lazy(load)
const MarkdownPreview = lazy(() => import('./MarkdownPreview.js'));

<Suspense fallback={<Loading />}>  
	<h2>Preview</h2>  
	<MarkdownPreview />  
</Suspense>
```
- the *load* function receives no parameters
- however, the function must return a **Promise**, or a "thenable" object
	- "thenable" means it has a `.then` method
- the Suspense works with lazy loaded components

## `memo`
[Reference](https://react.dev/reference/react/memo)
- "memoize" components, skipping re-renders when its props are *unchanged*
```jsx
const MemoizedComponent = memo(SomeComponent, arePropsEqual?)
```
- this comparison between props is a *shallow* comparison
- it's not a *guarantee* that it skips, but memoization is definitely an optimization
- the `arePropsEqual` is a function that takes TWO arguments
	- previous props & new props
	- it should return `true` if the props are equal, *or*, if the outcome would be the same
- memoization relies on *props*, and not context or internal state
- 

## `startTransition`
- the top-level API that comes with [[#`useTransition`]]
- it's basically a way to create transition *scopes* without the need to use the hook, if you don't need the `isPending` flag.

# Components

## `Fragment`
```jsx
	<Fragment>
		<Child />
		<Child />
	</Fragment>

	//syntax sugar
	<>
		<Child />
		<Child />
	</>

```
- groups elements without a wrapper node/element
	- the effect on the DOM nodes is as if they had no parent - they are not grouped. 

## `Profiler`
[Reference](https://react.dev/reference/react/Profiler)
```jsx
<Profiler id="App" onRender={onRender}>  
	<App />  
</Profiler>

function onRender(id, phase, actualDuration, baseDuration, startTime, commitTime) {  
	// Aggregate or log render timings...  
}
```
- measure *rendering* performance programatically
	- disabled by default in *production* builds, 
- the `onRender` prop is a *function* that renders on every render, that receives information about:
	- what was rendered
	- the time it took
	
## `StrictMode`
[Reference](https://react.dev/reference/react/StrictMode)
```jsx
const root = createRoot(document.getElementById('root'));  
root.render(  
	<StrictMode>  
		<App />  
	</StrictMode>  
);

```
- This component wrapper adds automatic functionality to its children to debug and find impurities:
	- components re-render 1 extra time, for impure rendering
	- effects re-run 1 extra time, for bad/missing effect cleanup
	- components are checked for *deprecated* APIs

## `Suspense`
[Reference](https://react.dev/reference/react/Suspense)
```jsx
	<Suspense fallback={<Loading />}>  
		<Albums />  
	</Suspense>
```
> [!hot] Only *suspense-enabled* data sources activate the Suspense *component*
> Certain frameworks support suspense, like **Relay** or **Next.js**
> or, we can use Suspense in React using the [[#`lazy`]] API
> !! Suspense does *not* detect when fetching occurs in an *effect* or *event handler*

- A wrapper component that tracks loading progress of resources in its children
	- while children continue to load, it displays the *fallback* prop, which can be another component/element/etc
	- the data loading/fetching component does not need to be a direct *child* of the suspense boundary
- when we wrap components with Suspense, it creates a *boundary*
	- we can *nest* boundaries to create "waterfalls" of UI updates
		- rather than waiting for all A, B, and C to finish loading for the whole UI, we can create nested boundaries, so that once A finishes loading, it triggers the suspense boundary for B and its fallback, and so on
# React DOM 

## `createPortal`
[Reference](https://react.dev/reference/react-dom/createPortal#createportal)
```jsx
<div>  
	<SomeComponent />
	{createPortal(children, domNode)}  
</div>
```
- render children into different parts of the DOM
	- the children that are part of the portal are only *rendered* as children of the `domNode`, but are effectively still children of the original component
	- the `domNode` must be a DOM node
- events from the portals *propagate according to the React tree*, not the DOM tree

## `flushSync`
[Reference](https://react.dev/reference/react-dom/flushSync)
- force React to flush updates in the callback *immediately*

```jsx
import { flushSync } from 'react-dom';  

flushSync(() => {  
	setSomething(123);  
});
```
- it can also flush pending updates, effects, or updates inside effects
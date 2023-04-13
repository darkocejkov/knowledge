___
 
# ? ? ?
React is a [[Frameworks]] built on [[JavaScript + TypeScript]]. React has very interesting principles that it uses
to accomplish it's goals, because it is essential a scheduler that holds information about the DOM that it constructs, and schedules direct changing to those DOM elements. 

# Why use React?
-> Why not just use plain JavaScript? Why bother with JavaScript frameworks?
- trying to create a hierarchy of components and classes to *organize* repeatable components is, plainly, undo-able in vanilla JavaScript.

> I, however, cannot debate why React vs. OTHER frameworks (Angular, Vue, etc), because there are clearly uses for all of them.

# React Explained (Under the Hood)

## JavaScript as a DOM Manipulator
JavaScript was built to programatically read and write from/to **DOM nodes** in the DOM tree. You can set up a simple HTML form, and using JavaScript, you can extract all the info from those elements. You can attach *listeners* and to DOM elements, and perform dynamic changes. JavaScript deals with the DOM.
It basically allows you to very easily programmatically define DOM elements, while also making it easy to insert and update them.

## React as a DOM engine
React, is a DOM manipulation engine. In your `.js/.jsx/.tsx` files, you write in terms of components (classes OR functional), and those will eventually be ran (somehow, sometime), in which React will track the components to add, change, or remove from the (shadow) DOM that holds in its memory. React only *re-renders* or *updates* DOM elements that have state changes, and not the entire tree of DOM elements
- This is why React is so special, and allows for things like single-page applications. Instead of relying on totally different HTML definitions, you can *dynamically* insert HTML using JavaScript, which React tracks.

> [!hot] Manipuling the DOM outside React
> Bypassing React and manipulating the DOM without React knowing about it is going against everything React is about, it's very bad practice to do so.
> - That doesn't mean you CANNOT do it at all, it just means that you need to do A LOT more work to make sure that your changes don't mess with React at runtime, because when React *expects* a node to be there (and it's not), then it FREAKS OUT.

## Shadow DOM
> React works by *virtualizing* the DOM and keeping its OWN copy, called the **Shadow DOM**. Whenever your React-based JavaScript runs, it does so in the context of the shadow DOM, manipulating those elements.

React then keeps track of those shadow elements, and translates the updates from the shadow (virtual) to the real DOM tree, which allows react to update SPECIFIC target elements, instead of re-rendering the entire tree to display tiny updates.

## React as a package
At its core, React is just another package that we can "import" or "include" to use in JavaScript. React gives us special functions to create React elements which then are tracked by React.
> Such functions are like `React.createElement()`.

## "Transpilation"
React is much more powerful when you combine it with a *translating compiler*; these are other tools that take one language and compile it into another. The purpose is not to compile JavaScript into something else, but code in JSX (JavaScript XML), which is an extension to ES6 with XML-type tagging.

This power allows us to define complex HTML/XML with embedded JavaScript, which can be *transpiled* into vanilla JavaScript. 
Without this, we would have to write React with object-defined elements
```javascript
React.createElement("div", null, children?)
```
- Babel as a transpiler converts JSX to JS, but also generates JS code that is efficient and well-supported.
> Which is not a) intuitive and b) any easier.

## Bundling
When writing code in React, all the important code ends up in JavaScript files. Since JS is [[Object-Oriented Programming OOP]] (classes, objects, inheritence, blah-blah), its can be dynamically linked,
- You can encapsulate functionality between different files, folders, etc.
However, it's not in the best interest of servers to have to send hundreds of files (regardless of size, even if tiny, still not good), especially when you use external packages. So, in order to make it more efficient to send over the necessary files for your application, you can **bundle** all those JS files into a single "bundle" (which *can* be chunked into smaller bundles). 
- Bundlers can be passed external options to configure *how* to bundle and minimize your code.

> Typically, we use a tool called **Babel** to transpile JSX into JS, and Webpack to *bundle* all the generated JS code into a single file.
> - This goes a little more in-depth in the [[DevOps Basics]] section, because the differences between *toolchains* is a DevOps/Design decision.

> [!tip] Create React App
> A toolchain / automation package that helps you create a React template project with all the necessary packages.
> Automatically creates an `npm` directory ([[Package Management]]), installs `react` + `react-dom` packages, initializes `webpack` (with hot-loading), `react-scripts` package to allow running basic testing, and hosting/preview functions.


## Using external packages
There are maaaaaaaaaaaaaany different JavaScript packages that allow you to do complex things. The worst part is finding a really useful package, but having no React port, or no easy way to integrate it.

When using external JavaScript packages, we need to make sure that they can integrate with React, because as previously mentioned, making changes to the DOM without informing React will build a broken webpage.

# [React Design Principles](https://reactjs.org/docs/design-principles)


## Parent-Child Relationship & Hierarchy
The [[Parent-Child Hierarchy.canvas]] is a relationship that indicates the hierarchy between components. 


## Passing Dynamic Data
React is built and designed so that we can pass properties and data between components to be able to dynamically render content. We do so by passing *properties* between parent and child components.
The whole principle behind this is that we construct components depending on their display or function. Say, a list component that is given some array/list of data, and its responsibility is to transform, then display that list in a certain way.

## *Rendering* dynamic *lists*
Rendering *lists* of data, by passing some list of objects in array via `props` to a component is quite simple, but requires a little more configuration because of how React tracks changes *within* the list. 
Whenever we decide to render a list by **mapping** an array to JSX, if there are any changes to items in the list, React has a hard time trying to "find" the resulting component that it is mapped to in the DOM.
- Thus, there are times where we properly update states, and the list we are updating does in-fact change, but is not reflected in the visual DOM tree.
- This is because React doesn't know which mapped item changed in the first place, so it is advised to use the `key` property on JSX elements (only needed on the parent) to add some locally unique identifier (an ID) to the JSX element so React can track that element to its corresponding list item.
	- [Lists & Keys](https://reactjs.org/docs/lists-and-keys.html)
		- basically, if the data has some unique identifier, we *can* use that inherit identifier as a key
		- we can technically use the mapped *index*, but it's not advised because re-renders don't keep the index to the data
			> a caveat to this is that we can use indices properly by *pre-transforming* data *before* it is rendered (instead of using the render-dependent mapping index)

# Class-based vs. Functional Components
JavaScript is *object-oriented*, and recent React updates have added more and more support for *functional* components, rather than requiring components be classes.

### Why?
Classes can be very verbose and requires quite a bit of boilerplate, and React has built a layer of abstraction (for itself) so that functions called **hooks** perform the same functionality (and are constructed as classes under the hood). If we want to really quickly create a small component without much overhead, we can use functional hooks to do so. 
- Both are valid, and most importantly, essentially identical. It's become more and more acceptable (as React releases updates) to not need *any* class-based components.
- You can very well create a complex hierarchy of components without needing any classes.
	- You can definitely still use classes to create components, and you sometimes need to do so for much more technical concepts because of the ability to track components and their FULL *lifecycle*.


# JavaScript Concepts
## Destructuring Objects
> Specifically for *functional* React
```jsx

function Letters(props){
	...
}

<Letters x y z/>
// equates to Letters({x,y,z})

```

Functional React is interesting, because we define functions, and them call them as JSX tags. Under the hood, when we call components with the JSX method, what it actually does is call the function that is defined by, and passes all the properties in the HTML-format, as arguments to it.

In the definition of the function/component, we can specify the properties by their expected key-name:
```jsx
function Letters({x, y, z}){
...
}
```
-> this makes it easier and much more organized to create components with specific properties, and is called **destructuring** objects.

### How it works
When we define a "destructured" object, all that happens is that the corresponding (must match!) *keys* are mapped to those runtime variables. If there are no *matching* keys between the destructuring and passed in object, then no prop values are mapped.corresponding

```jsx
const {x, y} = return {x, y, z, a, b, c}
	// only destructures ("pulls out") the x and y key-value pairs

const [x, y] = return ['x', 'y', 'z', 'a', 'b', 'c']
	// equivalent index-series mapping
		// where x is mapped to the 0th index, while y to the 1st.
```

> [!hot] Destructuring Arrays
> Arrays are *technically* objects, but we can destructure their members by using a similar syntax
> 

## Spreading Objects
The JavaScript **spread** operator `...` allows us to fully destructure objects without mapping them
```jsx
let obj = {x: 'x', y: 'y', z: 'z'}

<Letters {...obj} /> = <Letters x y z/>
```

The spread operator also works on **arrays**:
```jsx
let array = ['a', 'b', 'c']
let x = [...x] = ['a', 'b', 'c']
```

# React State
-> React is *state-dependent*, meaning that has built-in functionality to manage the state of dynamic content and variables. React really *only* cares about changes in the state that we make, any changes we want to make visually, must be done through states.
> This is because any visual effects of programatically dynamic content come from states, and whenever a state is updated, React then runs its whole change-tracking engine to determine what states changed, and what should be re-rendered.
-> React states are related to [[#React Component Lifecycles]], but in isolation, are quite simple.
The overall concept is super simple, we define some data to be a state and give it a name, and we can use functions to trigger react to change that state to some other data value, to which React does all the overhead of re-rendering.

# React Component Lifecycles

# React Hooks
Hooks are specific to ==functional== react, because they implement the Class-based methods and members in terms of functions.
Hooks typically follow the naming convention: `use<Something>`

## useState
This hook allows us to define a *stateful variable* with a given initial value, and passes us the current state's value, and a function to update that state
```jsx
const state = useState()
// state = [<state value>, <function to set state>]

//destructured
const [state, setState] = useState()
```
> when passed *no value*, the state is initalized as `undefined`.
> states can be numbers, strings, or objects (arrays, json, etc.)

```jsx
{state === 'yes' ? 'State is YES' : 'State is NO'}
```

## useReducer
`useReducer` is functionally identical to useState, but allows for "reducing" the footprint of the state update. This is because we pass this hook a **reducer**, and an initial value. This reducer is  a pre-defined function that runs everytime we call the function, so we don't have necessarily worry about defining the result of the update within the JSX onClick.
```jsx
const [state, setState] = useReducer((state) => !state, false)
...
<button onClick={setState}>
</button>

```

## useEffect
`useEffect` is associated with [[#React Component Lifecycles]], specifically an "EFFECT" of state updates. we can utilize this hook to in-effect, "listen" to updates in state, which are the "effects".
```jsx
useEffect(function, [<dependencies>])
```
Anytime an effect occurs, it will run the first argument, a function, as a "side effect". It becomes much more useful when we learn that the dependencies array is the list of objects that mark the initial update effect.

## useRef
`useRef` is a handy hook that allows us to set DOM node references to variables. They are typically used so that we can have some more control in handling the DOM element by having a **direct reference** to it, rather than having some indirect relationship, like `id` attributes.

```jsx
const textRef = useRef()
...
<input type="text" ref={textRef}/>

```
Importantly, a *ref* is an object, and whose reference to some value actually lies in the `ref.current` key. So, for this `textRef`, the reference to the input DOM element is found by `textRef.current = <input ../>`
> References are most commonly used for [[#Forms]]

## Custom Hooks
Hooks are basically just ways to encapsulate repeatable logic. For example, the `useState` hook makes it really easy to define a state with an initial value, and a way to update that state. In the back, it basically creates some class-based component and allows us to *hook into* that functionality.

We can really easy create new, custom hooks to handle *repeatable* behaviour, 
to group together logic. Custom hooks are encouraged to try and reduce the number of times you re-create the same logic in more than 1 place.

### Philosophy + Breakdown of Components
In Class-based components, we define a class as the combination of some *members* or variables, which in React, are states. Alongside members, we have *methods* which are the functions of the class, which we can call on instances of that object to act on members of that instanced object.

Class-based React components look like this:
```jsx
Class List extends React.Component{

	state = {
		integer: 0
	}

	increment = () => {
		this.setState(integer + 1)
	}

	decrement = () => {
		this.setState(integer - 1)
	}
	
	render(){
		return(
			...
		)
	}
}

```
-> Which a `render` function allows you to render how it displays, while it has other methods to update state, and members which are the state.

Functional components don't have this, you *return* the render display function, and use *hooks* to mimic the members.
```jsx

function List(props){

	const [state, setState] = useState("")

	return(
		<div>
			...
		</div>
	)

}

```
If you think about the call operations to handle components, these functional components are **called** or **invoked** anytime:
1. a state they've registered in a hook is updated
2. a state they've been *passed* as a prop is updated
-> the key here being the fact that they are functions and are INVOKED, which then RETURN some JSX values, to be registered by React

In a class-based component, the `render` function is invoked, but it's not based in a function, so there's this seperation between the **LOGIC** and the **DISPLAY** of the component. So class based components are very useful for that seperation, which cannot logically occur in functional-based components.

However, functional components are supplemented by the ability to create Custom Hooks, in which we can seperate any "reusable" logic, such as states.

A good design principle for functional react components looks like this:

```jsx

function useInput({initial}){
	const [state, setState] = useState(initial)

	function calculate(){
		...
		return a + b
	}
	
	return {
		setters: {
			setState,
		},
		getters: {
			state,
		},
		calculate
	}
}

function TextInput(props){

	const {getters, setters} = useInput({initial: ""})

	return(
		<input />
	)
}

```
-> In this rudimentary example, we abstract the state setting and tracking logic to the custom hook. There's no point to using custom hooks if there's no *reusability* to the logic, but in this case, we can use the hook in different components to abstract the logic of controlling inputs.
	- it would be more obvious if there was deeper logic that was using effects and relating between states.

The most understandable way to seperate *HOOKS* vs. *COMPONENTS* is that:
> Hooks maintain the *logic* and states, including the effects.
> Components *render*, whose output depends on the states that arrive from hooks.

I think the **MAIN** reason to use custom hooks is to abstract your complex logic so that:
1. It offers the ability to be *easily* reusable.
2. Hooks can communicate via props to other hooks
3. It encapsulates the design of some logic to allow it to be easily parentable.
	1. Think of when logic must be shared between children, it is basically required to be stateful within the parent, otherwise you start developing anti-patterns, and is then easily isolated

>[!hot] TL;DR
> Hooks extract *logic* and use *other hooks*, while ==COMPONENTS== describe the UI. 

Custom hooks are meant to encapsulate and re-use logic. The logic that we may have for dealing with controlled inputs would be the same between duplicated inputs, so we can "extract" this logic into a hook to reduce the amount of "copy-pasting" or how much you "repeat" yourself.

#### Why bother?
The most obvious example to come to my mind is a time where building a "Chat" component followed the worst path it could have. The requirements of the chat component made it so that it had to be in two different views, but maintaining the SAME state. 
> I believe the fact that it had to be in 2 different views came later, so intead of "re-architecturing" and fixing the root of the issue (where it lied in the hierarchy, as children) we tried to find a way to "sync" them.
Syncing these children components meant that we had to pass so many control states to the parent, it was basically the most silly anti-pattern to ever exist. Props and states would be passed in an attempt to get both children's states to be THE SAME, without them actually being THE SAME. Instead of parenting that chat logic and state, so that we pass it to two children to render it in different areas, we decided to attempt to sync them.

# Forms

## Controlled vs. Uncontrolled Components/Inputs
There are TWO main ways to handle *inputs*. In a *controlled*, or by using *uncontrolled* way.

Uncontrolled inputs rely on the browser to handle the "state" of the input. This takes away work from us as we do not have to set up states and handle updating inputs on entry. The browser's rendering of the input will automatically have some way to track the input. 

However, we can *override* this by using custom states and setters to control the behaviour of the inputs. This is really useful for defining custom input types, and validating the data entered into inputs. 
> On the other hand, this is much more work, because then the browser's validation does not work, and depending on the number of inputs, might be a lot of state setting and controlling.
> Also, if there are a lot of inputs, not having optimized state setting may make the form difficult to use because of performance issues.

# [React (NEW) Docs](https://beta.reactjs.org/learn/choosing-the-state-structure)

## State as *memory*
-> The entire purpose of *states* is to persist values **BETWEEN** renders.
-> Using states is essential to making things actually happen when interaction occurs, because otherwise, updating regular JS variables like `let` or `var` do not:
1. Trigger re-renders of changed content
2. Persist *between* renders

Something interesting is that we don't need to hold *everything* we render in states, because there are certain things that *rely* on states, but not need to persist.
> The best way to visualize this is with redundant code
> If we have 3 states:
> ```jsx
> 	const [fullName, ...] = useState(""')
> 	const [firstName, ...] ...
> 	const [lastName, ...] ...
> ```
> > it's OMEGA redundant to have an effect "calculate" the first name and set it is a state, because you never *need* to persist fullname IF you have the first and last names!
>
> in fact, we can just declare `fullName` as a runtime constant equal to the first + last names:
> ```jsx
> 	const [firstName]
> 	const [lastName]
> 	const fullName = `${fullName} ${lastName}`
> ```
> to which, on re-renders of state, `fullName` is "calculated" with the *NEW* values of state.

### Setting state as a function
When creating a state through a hook, it returns an array of items:
```jsx
	const [state, setState] = useState()
```
-> `state` is the current value of the state on that render call
-> `setState` is a provided React state setter that allows you to pass either a static value, OR a function.
> when you pass the setter a FUNCTION, it acts as a way to *queue* changes. This is because invoking the *setter* triggers a re-render, and the value of the state is different on **the next render**. So, if we wanted to run the setter *more than once*, whose value changed depended on the last setter run, we could pass a function (that must be *pure*)

-> This is officially considered as *queueing* multiple state updates *before* the next render.
```jsx

const [number, setNumber] = useState(0)

//no queueing
setNumber(number + 1) //0 + 1 = 1
setNumber(number + 1) //0 + 1 = 1

//queued
setNumber(n => n + 1) // (0) => 0 + 1  = 1
setNumber(n => n + 1) // (1) => 1 + 1  = 2
```
-> Queueing allows us to use the previously "set" state without requiring that it re-renders

## States & Rendering
The previous way I was utilizing states is in a very class-based way, even though I was using *functional* components. Functional components are an entirely different paradigm to wrap your head around, that rely on function invocations, and not "objects" so to speak. 
While React may/may-not hold instanced objects of your functional components (it's not important to the way we should be handling states anways), render **returns** from functional components do NOT act like objects.

It's pretty difficult to explain the exact way I was using states, but here's an example:
```jsx

const Item = ({}) => {
	const [active, setActive] = useState(false)

	return(
		<div>
			{active
				? ("Active")
				: ("Inactive")}
		</div>
	)
}
```
-> While this approach is valid, it's kinda stupid given the idea of *functional* components. I was basically going off the idea that this *function* would instantiate some object with my JSX, and the state would return based off the state.

However, it's more logical to return states this way:
```jsx

const Item = ({}) => {
	const [active, setActive] = useState(false)

	if(active){
		return <div>Active</div>
	}

	return <div>Inactive</div>
}

```

This is because react is running that function and returning the result. 

It is *still* valid to do conditional rendering within the return JSX  because it is calculated on render. It's more appropriate to do so for small conditional logics, but when there is more complex logic, or large differences in the returned JSX, then we should have conditional branches outside of the JSX.

The whole point is that we should shift the perspective into a functional view, so React will "render" the component by calculating the resulting JSX on render runtime, and not have some object whose members change.
> That was my entire mental hurdle, because there are some points at which we treat states and rendering as class-based objects, and others like functional compositions.

## State as a "snapshot"
The entire principle behind React is that we use hooks to create the ability to read and write to states. Anytime states are updated, React takes all the updates and triggers a "re-render" content by running functions.

> As a sidenote, any state updates that happen together are *batched*  together, so that we don't have to update multiple times for things that happen together.

-> React only invokes functions which *depend* on updated content. All children to updated parents, must also then be updated, because it's a strong assumption that children depend on their parent's states.
Thus, any time a re-render is triggered, React will invoke all functions to "render" or "calculate" the resulting output when given the NEW state.

## State is ==immutable== (should be treated as -)
In technical JavaScript terms, whenever you define a variable, it is *mutable*, because the value itself that the variable points to, can be mutated naturally.
However, even though React is built in JavaScript, the structure of "stateful" variables should be treated as *immutable*, meaning that we ==should not edit their values directly==, because React's entire purpose is to manage that for us.
> This is because we trigger re-renders by updating state, and is why we use React.

Although we may not intentionally change the values of states in mutative ways, we might accidentally do so because certain JS in-built functions mutate the values directly.
> `Array.push`, `Array.splice`, `Array.sort`, `Array.reverse` ^[https://react.dev/learn/updating-arrays-in-state#updating-arrays-without-mutation]
> 	These are examples of "in-place" functions, that manipulate the original object.
> 	Sometimes we can get away with using these functions, but it is bad practice to do so on the original state variable.
> 	> If we are to use in-place funcitons, we should be creating copies of the objects *before*

### Using "change-drafting" libraries with React
`Immer` is a library that helps us write simpler code, because we don't have to care about the constraints of how we are changing React states. `Immer` handles all the overhead of copying object properties and contents. It allows us to write simpler code to define exactly what we want to change.

### JavaScript Objects & Copying
Whenever we "copy" an object, operators like the spread (`...`) create ==shallow== copies of the object. That means it creates a duplicate object of the same type, size, ..., but the contents of any *nested objects* are contained as **references**.
> This means that we can create a shallow copy of an object, and edit 1st depth properties without modifying the *original*, but editing any nested objects will end up manipulating the originals (because they are references to the original).
> > What this means is that it becomes too difficult to manage large lists of deeply-nested objects.
If we want to "update" an object (nested or not), we can use the spread operator to *copy* all the key-value pairs, and use overriding to change the keys (or add new ones):
```jsx
	setState({...state, stateKey5: '1'})
```

## State Structure
The structure that we construct state is important, specifically how we design various states of our "machine". Think about states less about the visual content, and more about the various results of interaction. 
-> Form submission, Error states, Loading states, etc.
Here are the key **principles**:
1. Group related state
	1. If states update together, they are related
2. Avoid Contradictions
	1. If there are any states that are mutually exclusive, they should not be *seperate* states.
		1. For example, an `isSuccess` and `isError` state. Even though you may set them properly, in terms of logic, it opens up the possibility that they could *both* be true and in that case, would not make any sense. 
3. Avoid Redundant State
	1. State does not need to be created for things that can be calculated from *other* states at render-time.
4. Avoid Duplication
	1. Avoid containing the same objects in two or more states
		1. like a state containing a list of items, and another state containing the selected item.
5. Avoid deeply nested state
	1. gets difficult to detect any changes

### Redundant States
Looking into redundant states gives us a better insight into what *should* be a state and what *should not* be. There were one-too-many times in which I created states that are just redundant, or states that are not condusive to good design.

### Duplicated States
Avoid creating states that contain the *same* things as other states, the most obvious being a set of items, with a state being a selected item. Why bother, when we could just set a key on the set of objects for the selected key, have just ONE state to be the `selectedId`state.

### [Flattening Nested Objects](https://react.dev/learn/choosing-the-state-structure#avoid-deeply-nested-state)
If we want to flatten the structure of an object, we could think about how *databases* do that. They use relational **keys**.
If we want to transform nested objects, we can borrow that same philosophy and use 1st depth, indexed objects to reference child elements:
```jsx

const object = {
	a: {
		title: 'a'
		children: [
			{title: 'a1', id: 'a1'},
			{title: 'a2', id: 'a2'},
			{title: 'a3', id: 'a3'},
			{title: 'a4', id: 'a4'},
		]	
	},
	b: {
		title: 'b'
		children: [
			{title: 'b1', id: 'b1'},
			{title: 'b2', id: 'b2'},
			{title: 'b3', id: 'b3'},
			{title: 'b4', id: 'b4'},
		]	
	}
}

const flatObject = {
	0: {
		title: 'a',
		children: [a1, a2, a3, a4]
	},
	1: {
		title: 'b',
		children: [b1, b2, b3, b4]
	},
	2: {
		title: 'a1',
		id: 'a1'
	},
	//...
	9: {
		title: 'b4',
		id: 'b4'
	}
}

```



## Position-based Elements
We're talking about position *within the DOM tree*:
- Position within the DOM tree is important, because it may *seem* like a component state is *internal* to itself, it's actually **global** in the scope of React, and it ties it to components based on their position/order within the DOM tree.
	- Thus, if you de-render and then re-render a component, and it ==does not change it's position== (making sure everything else is the same, such as the parents!) then it *preserves* that state.
		- It only perserves state between the *same components*, not different ones.
		- So to perserve state between renders, the entire structure of the component, including any removed parents, must be the same
		
	- As soon as the position is lost, like when a *parent* de-renders and removes itself (and its children) from the tree, then the persistence of the state is destroyed.
> What about forcing a reset even though the structure is the same, how do we tell react to clear that persistence?
> -> We use *keys* to uniquely identify components, and these keys are what then make the structure different, which cause state to be cleared

## Using Reducers & Dispatching Actions
Given that you have some data structure or component that handles multiple types of actions:
- adding
- changing (editing)
- deleting

You might have state handlers to handle *each* of them:
```jsx
function handleAdd(text){
}

function handleEdit(){

}

function handleDelete(id){

}
```
-> In each of these "handlers" you handle the action by setting the states.
> -> in `handleAdd`, you set the array in state to have an extra item
> -> In `handleDelete` you set the array in state to be the the result of the filtered array (without the item to delete)

Reducers move this logic to the top-level, by allow us to *dispatch* actions, and making it go from =="what to do"== to =="what the user did"==:
In your event handlers, you then handle dispatching an **action** event to the reducers, which live elsewhere, and can then be "more generic", so you can re-use them.

```jsx

const [actions, dispatch] = useReducer(actionReducer, intialActions)

function handleAdd(text){
	dispatch({
		type: 'add'
	})
}

function actionReducer(state, action){
	if(action.type === 'add'){
		
	}else if(action.type === 'delete'){
		return state.filter((t) => t.id !== action.id)
	}

	//can use switch statements:
	switch(action.type){
		case 'add': {
		}
		case 'delete': {
		}
	}
}

let actions = [
	{type: 'add', ...},
	{type: 'delete', ...},
	{type: 'add', ...},
	{type: 'add', ...},
	{type: 'edit', ...},
]

	 let resultingState = actions.reduce(actionsReducer, initalActions)

```
> -> You dispatch *actions*, which are just regular JS objects that can have *anything* in them, but the important common part is that you should describe in some field "action" what action you're handling.
> -> Since the reducer function takes the state as an argument, we can export/define it elsewhere because it's then just a function that will *return the next state*.

### Why "Reducer"?
It is meant to be an equivalent to the JavaScript array method `reduce()`, in which you can act on an array by passing a *function*, that reduces/accumulates a single value from that array.
ex:
```js
const array = [1,2,3,4,5]
const sum = array.reduce((res, n) => res + n) //returns 1 + 2 + 3 + 4 + 5
```
-> A reducer is similar to some *forEach* functionality, in which it runs for each element, but is unique because the input to the array changes everytime, because the value of the previous return goes into the next one (think of [[Loops & Recurrence Relations f47d8de94e5b4dada17948e63de11c2e]])
-> State reducers do the same ... to React's state.
-> State reducers allow us to abstract actions, and keep track of all the actions that have occurred to state, and allow us to have that determinism.
- GIven a list of actions (that would normally be "dispatched"), we can use the JS `.reduce()` method with the `actionReducer` we pre-defined to arrive at a final state.

## Purity & Components
Components and Functions are considered pure when they only *perform* a calculation, in which given the same inputs, they must always produce the same outputs.
What this means for React components is that given the same props & state, they must always produce the same JSX.
-> Components should only return their JSX, and not change any objects/variables that exist *before their own rendering*, if they did - they would be impure.

This only applies to variables that were created before the function's invocation existed, and not for variables that your function *created*. So, functions are still pure if they manipulate local variables (local mutation).

### Strict Mode
StrictMode is able to detect impure functions/components because for each render, it calls each function *twice* to detect the output, and if it's different between each call. If it is, then it is then impure.

## Context to avoid Prop Drilling
Lifting state **UP** is super important to React applications, it lets parents *share* the exact same state information to children that need it. It starts becoming a problem when we have many children in the component hierarchy that require the prop/state, because we "drill" that prop to each child.
Context is meant to solve this, because Context allows any component that explicitly states that it wants context, to use it (using the `useContext` hook).

Context is more than just a "global" variable like I've used previously, you *can* use it that way, but React has some more advanced usages.

1. Create a context using the `createContext` function imported from React. This can be in a different file.
2. Hook into the (imported) context file using the `useContext` hook in each component that requires the context.
3. *Provide* the context using the `.Provider` sub-component:
```jsx

//Context.js
export const Context = createContext(1) 
	//context can contain numbers, strings, objects, etc.

//Section
const Section = ({level, children}) => {
	<Context.Provider value={level}>
		{children}
	</Context.Provider>
}

//Heading
const level = useContext(Context)

switch(level){
	case 1:
	case 2:
	...
	case 6:
}

//App.js

<Section level={1}>
	<Heading>1</Heading>
	<Section level={2}>
		<Heading>2</Heading>
		<Heading>2</Heading>
		<Heading>2</Heading>
		<Section level={3}>
			<Heading>3</Heading>
			<Heading>3</Heading>
			<Heading>3</Heading>
		</Section>
	</Section>
</Section>


```

-> Components that are *provided* the context will use the value of the NEAREST Provider in the UI tree.
-> This section + heading example makes it such that each Section provides context to its children, who will use its closest *parent* Provider. Each section component sets the level in the context that it provides.
> Actually, since each component is provided context from it's parent, we don't need to actually have each section explicitly set the level through a prop, but rather can do so in the series (like a reducer), because each context `Provider` can return a level 1 greater than the previous context's

## Refs
Refs are considered *escape hatches*, they are something we can use sparingly to help us persist values between renders, that may not need to be read or written per render.
The whole point of *refs* is to to be able to hold some extra information that will persist between re-renders, but whose mutation does not trigger re-renders.

The most logical use for this is holding React-external information that allows us to interact with other APIs without causing problems with React's render cycles.

Obviously, if we create `useRef` references and use them to store information that is updated on render, it won't trigger re-renders, and does not visually update. 
```jsx
const count = useRef(0)
...
<button 
	onClick={() => count.current += 1}
></button>
```

> [!tips on using refs] 
> - storing interval/timeout IDs
> - using element specific node functions

> Refs are basically the same as states, with the *core* difference is the way we manipulate them, they are like states *without* setters.

Refs can be passed directly to JSX using the `ref` attribute, and help us connect directly to the DOM node with a reference to it. 
This allows us to directly access browser-native node functions like `focus`, `scroll`, attributes like `clientHeight`, etc.

### Forward Refs
Are how we can "lift" references up to parents, by using the `forwardRef` function to create a component, which allow us to pass a ref to the component. This makes it possible to use DOM APIs from the parent from higher-level events.

### State Synchronously & Flushing
A very common use of refs is to force the browser to do something in response to an event in React. A simple example is the effect that occurs when adding a new item to an arbitrary length list - what should happen if the list goes off screen? We would want to scroll to the element, and the only viable way to do so is using the `scrollIntoView()` API through `ref` nodes.
> The problem is when we should be doing this, because when we signal to React to add to the stateful list of items, the newest element is added in the *next* render, so if we attempt to `scrollIntoView()` right after the state setter, the newest element isn't there yet.
> So, to fix our problem, we use the `flushSync` React API to instruct React what to render *synchronously* within the event handler, and then perform our browser API afterwards, so that when the API runs, it does so only on the *next* render.

```jsx
	flushSync(() => {  
		setTodos([ ...todos, newTodo]);  
	});  
	
	listRef.current.lastChild.scrollIntoView();
```

> [!important] Performing DOM manipulation with **unsafe** functions like removal, or addition can lead to BIG problems with React

# We've been doing it **all** wrong.
As previously mentioned, the previous philosophy I've approached rendering in React comes from the fact that I thought hooks were meant to mimic class-based components, and "hook" into the lifecycle of components. This is true, but the missing piece is that functions are invoked, and are not instantiated by objects. When React would like to re-render, it invokes each component's functions and uses the JSX returns to piece together the resulting DOM for the next commit.

Effects were effectively used as chains of operations when states would be changed, which is entirely not how they are meant to be used as hooks. The next [[#Effects]] section will clarify *how* to effectively use *functional* effects.

## Effects
React has two logic types:
1. **Rendering code through JSX**
	1. given states and values, functional components *compute* and *return* the rendering code
2. **Event Handling**
	1. Functions given to components to do things in response to an event

==Effects== are functions that let us specify any side-effects that occur AFTER rendering, and not in-response to an event. Events and their handlers handle changing of state, but on the next render, there may be a *side-effect* of that change.
-> Effects are triggered at the ==end of commits==, which is after browser paint, on the next render.

> Effects are meant to be used only to "step out" of React to **synchronize** some external system to the state of react. 
-> This knowledge is my largest predicament, as the way that effects have been classically used are to update other states or to trigger calculation when data arrives and we want to store that calculation in a state.
-> This is precisely why the previous designs would basically treat functional components as class-based components, but built in functions. It was an entire anti-pattern, but it still worked.

```jsx

useEffect(!function, ?[dependencies])


useEffect(() => {
	//runs on EVERY render
})

useEffect(() => {
	//runs only after the FIRST render
}, [])

useEffect(() => {
	//runs only after "state" has changed
}, [state])

```
-> Effects are tested on *every* render to see if they *should* run. Effects with **dependencies** only run after renders in which their any one of their dependencies have changed
> Effects with multiple effects do not run if NONE of their dependencies have updated

### When TO USE effects:
1. Attempting to synchronize with non-React systems
2. When fetching data* [[#Data Fetching]]

### [When to not use effects](https://react.dev/learn/you-might-not-need-an-effect):
1. Updating state within effects, transforming data for rendering/display

#### Poor use of effects exemplified: 
- Something I have been very guilty for in the past, while using effects, is that I would "piggyback" off state changes to enforce rules, or other state changes
![[Pasted image 20230413111655.png]]
- The context here is that `equal`, `height`, and `width` are all stateful variables. `equal` is a boolean, and i would use effects to try to synchronize React components - this is WRONG WRONG WRONG. 
- Effects are not for synchronizing React state and logic - you do this in the event handlers. Instead of creating a side effect to listen on changes to `equal`, you handle this in the event handler directly.
	- Why? It's unneccessary to do so, because you can just shift this to the event handler, and the logic is centralized and not spread in various side effects. If it's too much to organize this logic in the event handler, then you can move this into a reducer.
		- Since effects run AFTER the commit, running an effect to set another state causes a new re-render, which causes a *chaining* of re-renders, because setting state automatically triggers re-renders, which then trigger effects, etc.

```jsx

const [data, setData] = useState()

// BAD
const [filtered, setFiltered] = useState()
useEffect(() => {
	setFiltered(data.filter(...))
}, [data])

// GOOD
const filtered = data.filter(...)

// GOOD (IF OPERATION IS SLOW)
const filtered = useMemo(() => {
	return data.filter(...)
}, [data])

```
-> useMemo allows you to skip unnecessary calculations, so you tell React only to re-calculate when at least 1 dependency has changes


2. In response to changes of other events to "reset" or change states
> Like in the previous point, using effects to reset or manipulate states as a result of state changing is an anti-pattern, because it results in more render updates then necessary.

If we would like to *reset* states, we can do so by de/re-rendering components, or being more intelligent and providing unique `key` to components (covered in [[#Position-based Elements]]). 

### Storing previous states
Storing previous states should not be used often, but we can still do this while maintaining good design patterns in React. It is mostly done as another way to respond to changes in other states to avoid using Effects to accomplish it.
To store previous states, we must create some state to store it. Uniquely, we should be calling this *during render*:
```jsx

const [prev, setPrev] = useState(items)
if(items !== prev){
	setPrev(items)
	setSelection(null)
}

```
-> Why is this okay? Because it's efficient in how it *skips* the rest of the render cycle. With effects, a full render occurs, the changes are commited, then the effect runs, and triggers another render + commit. 
-> Updating state directly in the render (although, should definitely be conditional) throws away the current render cycle on the return and triggers an immediate re-render.

3. Computation Chains
It's very simple in terms of logic and tempting to use effects that trigger on changes of other states, to calculate states based on rules (like a game, or process, or sequence of events). However, this is really stupid when we consider that for each state update, the component is re-rendered.
The whole point of states and functions as render is that each render is a 'snapshot' of states and what should be rendered - so requiring states to update in the *next* render to cause *another* render is just bad practice/logic. Most of the time, we can *calculate* the state using the current one, instead of trying to set a state.
-> There are times when chaining **IS** necessary, like when the previous state does influence the next one.

4. Initalizing the application
Instead of using an effect on mount (to mimic `componentDidMount`) to check auth or something like that, we can just run our init. functions *before* the app loads (on module load)

5. Synchronizing data between children & parents
Requiring to "sync" data between children and their parents is just bad logic, because the ultimate way that React components should respond to events is like this:
> Child bubbles, Parent handles.
In the case that the parent *does not need* the information, then there's no need for this sync to occur. But once the parent does need the information, it's just much simpler to have the parent handle the event, and pass down the information to the child.

6. Notifying parents of state changes
This one is a little more nuanced then just making the parent handle the state change itself, because it is still okay to notify parents of state changes. It's *inefficient* to do so within an effect, because it takes more than 1 render cycle to update parent's state in response to a child state update.
The more appropriate way to signal state changes to parents is to instead directly call the parent's passed down `onChange` function (whatever it may be) when the state is *supposed* to change:
```jsx
function Child({parentChange}){
	// BAD
	useEffect(() => {
		parentChange(state)
	}, [state])

	// GOOD
	function updateState(next){
		setState(next)
		parentChange(next)
	}
}
```
-> The reason this is efficient is that React can tell that you are updating the child component's state AND its parent, and **batches** their updates together, so it takes 1 render cycle for the state for both to change, rather than 2.

Overall, we should stick to these guidelines when dealing with states:
1. Only manipulate state in the event of a user action
2. Only use effects to synchronize external (non-React) API states with React's state

## Effect Cleanup
All effects can return a *cleanup* function, which allows you to perform cleanup on things that happen within the effect. These are most often used when performing doing things asynchronously to change flags or to issue disconnects for data streams.

```jsx

useEffect(() => {

	// SETUP code
	const connection = createConnection()

	// CLEANUP functions
	return () => {
		connection.disconnect()
	}
}, [dependency])

```

This is the order effects run in:
1. On mount, setup code runs 
2. After any re-renders, if any *dependencies* have changes, it re-runs the side-effects
	1. `cleanup` (to cleanup any side-effects of the setup code)
	2. `setup`
3. When the component is going to unmount, it runs the `cleanup` function once more.

> In React Development mode (StrictMode), React calls all functions TWICE.
> So it is common to see effects happen twice in 1 render, but only in StrictMode.

### LayoutEffect
Is an escape hatch for effects that lets us run the effect **BEFORE** the browser *repaints* the screen, meaning we can perform layout changes based on the new render information, but change states meant for dynamic content.
> An example is the need to `useLayoutEffect` for tooltips to set the height of the tooltip, because we need to know the height of the rendered tooltip to perform some React-specific rendering with that information.

## Effect Lifecycles
Effects are meant to synchronize React's states to some other (external) system, like some other API that React cannot interact with itself, like browser function APIs or data endpoint APIs.
The lifecycle of an effect is *meant* to use cleanup functions (whenever needed) to keep the state of React in sync with that external system. 
If an effect is dependent on some state, it will trigger after rendering, whenever its dependency changes. Whenever an effect re-fires after it's first initial setup, it calls the cleanup function (which is created as a "snapshot") when the setup first ran, so it can use the ==old== value.
Then, it runs the setup code to re-sync to the new updated render state.
On unmounting the component, the clenaup functions run one last time.
The point of this being is that it's useful to think of an effect's lifecycle in the perspective of the effect itself, and NOT the component's lifecycle.

> Essentially, React code should be **declarative**, in which you are describing the UI and the effects while React figures out how to do that. This is instead of the **imperative** way of thinking, where you *tell* React how to accomplish that.

## Effect Events (experimental)
Effect events are handy little hooks that allow you to declare *events* to use within effects, they are basically like event handlers. Their purpose is that they "detach" the reactivity from certain states, so that Effects don't trigger on changes in any states used in the Effect Events.
For example, imagine we have some component that uses effects to connect (and cleanup by disconnecting) to some API. If we wanted to include the addition of some extra state information, like themes/colors/etc, using those states results in that effect firing on changes to it - which are not ideal for the API. We can use effect events to wrap any reactive values to make the effect not trigger for changes in those, but they maintain reactive in the sense that we can continue to "see" the latest value.
```jsx

const [isDark, setIsDark] = useState(false)

<Chat id={...} theme={isDark}/>

const Chat({id, theme})

const onConnect = useEffectEvent(() => {
	showNotification('connected!', theme)
})

useEffect(() => {
	const connection = createConnection(url, id)
	connection.on('connected', () => {
		onConnect();
	})	
}, [id])
```
-> Effect *events* are basically ways to define ways to "read" the current value of a state, without initiating a sync effect trigger.
Of course, this depends on the principle of the event itself and the relationship between these states. If you want to POST to an API whenever a user changes the *URL route*, the effect requires the dependency of the URL. If you suddenly wanted to add in other information, like cart items, metadata, etc., then the effect depends on those *reactive* properties, and starts to fire not only when the URL changes, but when those other reactive properties do - which is not the intention of the sync action. That's what **effect events** are attempting to create as side-effects, ways to "read" the value without reacting to its changes.

Effect events should not be:
1. Called from anywhere ==except Effects==
2. Passed to other hooks/components.

## Effect Checklist
1. Effects listen to REACTIVE states to keep in sync between React states and whatever other external system is used.
	1. If we *prove* or *define* **constant/non-reactive** "states" or variables, then React does not need them to appear in the dependencies of an Effect
2. Effects should define how to *start* the sync, and how to appropriately *stop/cleanup*. 
3. Should only be dependent on states tha are *necessary* for the sync, any other states just cause re-triggers.
4. Code in Effects that is more of a response to a single, discrete *event* should be in *event handlers*, and not Effects.
	1. ie. Cut out the *middle man*, why bother having a "submitted" state to trigger a code in an effect, when you can trigger the code directly
5. Utilize local variable flags to cleanup any data fetches
6. Effects should be single, atomic logic that is *related* to a single sync operation. Just because two syncs might use the *same dependencies*, you can seperate them.
7. Use **updater functions** to define how states should be set. 
	1. This one is a little more nuanced, but if we are using an effect to create/sync some connection, and must define callbacks within the effect for that connection/resource, then using the *original* states creates an unnecessary dependency, when we could just define a *function* (like a reducer, etc).
8. Use Effect events to "read" but not "react" to state changes within Effects.
9. Trying to mimic "lifecycle" events is more of a class-based component, trying to do so with Hooks results in bad code that can introduce weird bugs.
10. 


### Functions as operators, not state readers
> As a sidenote, supplying the values of states to functions that are called makes development more cleaner, because a function is *meant* to take parameters and operate on them - not just use "global" state. 
> Of course, it depends entirely on the paradigm of the application and the ways that state is set. Always be mindful about the differences between *accessing* state, and *passing* state. 
> this becomes ESPECIALLY important when we have asynchronous logic. If a function depends on the value of a state, and that value changes before it's used, then we may be getting a different result.
> ```jsx
> 	const [url, setUrl] = useState('/')
> 	const visit = () => { window.location.href = url}
> 	
> 	setTimeout(() => {
> 		visit()
> 		visit(url)
> 	}, 5000)
> ```
> > What happens when the 5000ms passes and the function without arguments runs, there may be a time when this could cause a different URL to run other than the *intented* one.
> > If we supply an *argument*, it effectively sets the callback in the timeout function to be "replaced" with the *current state* when the callback is created, which leaves NO room for error.

Effects should be declarations of single effects, and even though some synchronization actions *depends* on the same state or prop, you should seperate them if they are totally seperate actions. Each effect is an **independent synchronization process**.

Effects are also aware of "reactive" states and variables. Even if you reference a variable within an effect, that's not in the dependency array, whether or not you are writing a valid effect depends on if that variable can change.
-> Calculated properties *from* states and props are considered reactive
- So, if a state changes, any calculated/memoized values that depend on it will be re-calculated. However, even if the state it depends on changes, that calculated value *may not change* (depending on what it is):
```jsx
const [state, setState] = useState(0)

const gt5 = state > 5 ? 'Yes' : 'No'

useEffect(() => {
	fetch('...')
	//if state changes and does not result in a change in gt5
	//then this effect does NOT run
	//ex. state = 6 -> state = 7
		// gt5 = 'Yes' -> gt5 = 'Yes' 
}, [gt5])
```
-> Mutable values are *not* reactive, this is because they are don't trigger re-renders like react states do. Even if you include them in dependencies, they don't trigger re-renders, and thus, do not trigger sync effects.

Thus, this *declarative* vs. *imperative* shift in perspective is exactly why the effects I've written are very poor in logic, because Effects don't really care about the Lifecycle of the component, but rather the states that it depends on. After all, this "effect" is not a method of a class, but a function depending on a hidden conditional statement: whether or not at least 1 dependency changed.
-> So, effects with "empty" `[]` dependency arrays don't necessarily mean to run "when the component mounts", but rather it has no dependent, reactive states, so it will *correspond* to running only on component mount/unmount.

## Subscribing to an external "store"
There are many built-in browser APIs to help to connect information about the client to JavaScript, like the `navigator.onLine` API to give information about whether or not the client [browser] is connected to the internet
This *was* normally done with Effects, but there is a hook built specifically to "subscribe" to changes in these stores of information, provided by the hook `useSyncExternalStore`. 
```jsx
	function subscribe(callback){
		window.addEventListener('online', callback)
		window.addEventListener('offline', callback)

		return () => {
			window.removeEventListener('online', callback)
			window.removeEventListener('offline', callback)
		}
	}

	function useOnlineStatus(){
		return useSyncExternalStore(subscribe, //what to do 
			() => navigator.onLine, //getting value on client
			() => true, //getting value on server
		)
	}

	function ChatIndicator(){
		const isOnline = useOnlineStatus()
	}

```
A "store" is really like some external variable, like anything we can access in `navigator`, `window`, etc. 
-> This hook allows us to hook into these variables rather than attempting to manually listening to them using effects. Why? because Effects are functions that are meant to be **pure**, and mutable stores/values do not trigger re-renders, so there may be renders where the results are different than expected.

## Effects vs. Events
Effects are meant to *synchronize* between changes in STATES and EXTERNAL resources. Again, they are NOT meant to synchronize states with OTHER states,  they are not methods to detect changes in state to create a CHAIN of computation, but rather should ONLY be synchronization.
Effects should typically be independent of SPECIFIC events, effects are the result of external events firing, updating state, then triggering the effects (on the subsequent) render.
Most effects are then independent of a *single* event, but rather a collection of them - it doesn't matter what the user clicks, drags, pans, etc. The effect should run regardless of those and only if the effect needs to sync a state with something external.

Effects are *reactive* to changes in reactive states, while Events are not *reactive* to state, but rather to browser events (clicks, scrolls, etc.)

## Data Fetching
Data fetching is a real complex subject, because to do data fetching *well*, we need a LOT of infrastructure in our React components and logic to be able to handle data. 
Of course, if we're handling just small amounts of data, in-frequently, then it's really okay to proceed with an inefficient or non-scalable method to fetch data. But, the more data we need, the more complex it becomes since we then need to start caring about the arrival of data, the way we cache data, cancel requests, data validity, etc.

### The basic way
Using an Effect is a valid way of fetching data, because we *are* synchronizing or using an external system outside of React, and effects are really simple ways to attach changes of state to API calls. 
> Of course, some API calls are *meant* to happen only on events, and not effects. Like submit buttons, search buttons, clicks, etc...

Here's a solid example of how data is fetched from within an effect:
```jsx

useEffect(() => {
	let ignore = false
	async function fetchData(){
		const json = await fetchUser(id)
		if(!ignore) setData(json)
	}

	fetchData()

	return () => ignore = true;

}, [id])

```
-> This simple example is a very easy way to understand how to proficiently use basic API calls from within `useEffect`.
-> The main takeaway is that given an effect is specific to interaction on a component, if something occurs between starting the data fetch and the time the fetch arrives with data, that would most likely 'invalidate' our data.
- If the user navigates away and the component unmounts, the data would still arrive and set the state even though the context may change and that data is not needed, or is invalid.
- Thus, using cleanup functions, we can automatically invalidate data we fetch that is not relevant.
	- We can also [abort](https://developer.mozilla.org/en-US/docs/Web/API/AbortController) the fetch using browser APIs.

### Harnessing parallelism for React data fetching
Instead of requiring the previous fetch to complete before starting the *next* one (which creates #waterfalls, through component mounting and prop requirements), we can propagate all fetches to occur at the top-level of our component.
-> Instead of having them occur synchronously, we can use the Promise API:
```jsx

// PARALLEL
// states are set only when the LAST promise result resolves
useEffect(async () => {
	const responses = [a, b, c] = await Promise.all([
		fetch('/a')
		fetch('/b')
		fetch('/c')
	]).map(r => r.json())

	const [aData, bData, cData] = await Promise.all(responses)

	setA(aData)
	setB(bData)
	setC(cData)
}, [])

// PARALLEL
// states are set only when EACH of them resolve
useEffect(async () => {
	const responses = [a, b, c] = await Promise.all([
		fetch('/a').then(data => data.json()).then(data => setA(data))
		fetch('/b').then(data => data.json()).then(data => setB(data))
		fetch('/c').then(data => data.json()).then(data => setC(data))
	])
}, [])

```
-> Why does this work? because they all start their fetches simultaneously (or when possible, but the `.all` method takes care of this...)

#### JavaScript breakdown:
- `Promise.all()` takes a list of promise-based functions and returns their results
- `r.json()` is a promise-based function, so mapping each fetch resolve to it's `json()` promise puts promises into that array
- then, we can run the `Promise.all()` method once more on this array of promises to get the resulting JSON data.


### Why shouldn't we use effects for complex data fetching?
1. Effects require states and re-renders, so there's no "pre-loading"
2. Without a caching system, data fetches can occur often and inefficiently
3. Since fetching is a result of component mounting, the order of mounting and render will cause "network waterfalls" as only the child component renders and starts fetching when the parent *finishes* fetching.
	1. Running requests in parallel (if possible) is limited to 6 requests at once (if HTTP1)


### Why is native React data fetching so difficult to perfect?
React is a framework built to make UI much easier and organized through components and states. It's not necessarily meant for dynamic data and content, but supports it. You can definitely build a really robust data-fetching method *only* with React.
There are a lot of pitfalls when using only React, and lots of implementation to add if you want to optimize *how* and *when* you fetch data. It's good to know how you can opt-in to doing custom data fetching techniques, but as an app grows and becomes much more complex.

### Data Fetching packages
- `useSWR`
	- built by Vercel, same who created NextJS
- `React Query`
- `React Router (^6.4)`
- ...

## React Frameworks
Believe it or not, there are **React** [frameworks](https://react.dev/learn/start-a-new-react-project#production-grade-react-frameworks) that build on-top of React:
1. NextJS
2. Remix
3. Gatsby
4. Expo (Native)

### Why?
They pre-implement a lot of the stuff that you would normally need for full-scale applications. 
-> For example, React only builds you a UI and interactivity between JS and DOM elements.
- To achieve routed paging, you need to install `react-router-dom`.
- To achieve API fetching, you can install `axios`.
- etc, etc, etc.
The point being is that these frameworks already have these features built-in, so there's no installing to do for these features.
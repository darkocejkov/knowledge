State management in React is super important, since React is all about the state and any changes to the state.

Whenever we create state using the `useState` hook, it creates a *getter*, a direct reference to the current value of the state, and a *setter* that allows us to update that state. This is great for small applications and components, but is difficult to handle when you start having many states to control an application, especially with different pages, modes, integrations, etc...

Thus, the "flux" architecture was developed to handle *actions* rather than imperative changes in state. It's based on the idea of *reducers*, in which we dispatch actions, and are able to manipulate a global store of states rather than a large list of individual states.
___

Flux is meant to re-work how we think about state changes because it assumes that different states will update in common ways to others, related to *actions*. If a user presses a button, in non-flux architectures, you have to update multple different states simultaneously. In a flex architecture, that event of a button press issues an action, which arrives at a "dispatcher" to choose the logical path, almost like a switch-case, which performs conditional logic based on the action. 

> It's called *flux* because the original solution was called Flux.


# Redux
Is a package that serves as a way to implement the flux architecture, which uses the same kind of action-dispatcher concept.
In Redux, we create *stores* to hold application states, which are essentially JS objects. 

## Reducers
Based on the idea of the Array method `.reduce`, reducers are ways to structure functions given:
	1. current state
	2. an action

Based on the action, the reducer can use conditional branching to perform 'actions' on the state, whatever that means for your application.

For example, if an action (a simple JS object) is given to a reducer, whose type is `INCREMENT`, then the reducer performs the appropriate INCREMENT logic, and returns the state.

Reducers are not meant to be manually called, but you use them with the `createStore` Redux method to set up a store that uses that reducer.

```js
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    case 'ZERO':
      return 0
    default: // if none of the above matches, code comes here
      return state
  }
}

import {createStore} from 'redux'

const counterStore = createStore(counterReducer)
counterStore.dispatch({type: 'INCREMENT'})
```

## Deterministic Actions
You can use *reducers* and *dispatchers* without Redux itself, through the `useReducer` hook from React itself. However, it makes creating a lot of stores and dispatchers easy with Redux.

Something that is much harder to implement with base states is a *history* of states. It's very natural to be able to create a list of "actions" and be able to move forwards and backwards through the "history" of actions, to which the reducer handles the dispatching of those actions. 

It *is* possible to do the same with base states, but it's much more natural in reducer/flux-architecture.

## "Synchronous" updates
Updating a state in react is *asynchronous*, meaning that triggering state updates does not give you the updated value until the *next* render.

```js
//update values
setState(state + 1) //1 + 1 = 2
setState(state + 1) //1 + 1 = 2

//update functions
setState(x => x + 1) // 1 + 1 = 2
setState(x => x + 1) // 2 + 1 = 3
console.log(state) // 1
```

The closest we can get to creating a *chain* of state updates is to use updater functions rather than values. 

Even then, these updater functions are declarative on the *next* render, and trying to "check" the value in between/after state sets does not work as you think it does.

Since Redux is the "middle-man" for our state, it's a bit smarter and we can synchronously view the state because it can "walk" through actions and we can use `store.getState()` to get the synchronous value of the state:

```js
const store = createStore(counterReducer)
console.log(store.getState()) //0
store.dispatch({ type: 'INCREMENT' }) 
store.dispatch({ type: 'INCREMENT' })
store.dispatch({ type: 'INCREMENT' })
console.log(store.getState()) //3
store.dispatch({ type: 'ZERO' })
store.dispatch({ type: 'DECREMENT' })
console.log(store.getState()) //-1
```

## Store Subscription
Similar to an effect, we can "subscribe" to updates in the store:

```js
store.subscribe(() => {
  const storeNow = store.getState()
  console.log(storeNow)
})
```

```js
const root = ReactDOM.createRoot(document.getElementById('root'))

const renderApp = () => {
  root.render(<App />)
}

renderApp()
store.subscribe(renderApp)
```
> Redux is independent from React's state, meaning that dispatching actions does not actually trigger re-renders, because we've decided to go with Redux stores. React therefore has no idea when these changes occur, so we can create a *manual* subscription create re-renders on dispatching actions.

## Immutability
Just like with React's states, we should never mutate the states directly, meaning that functions like `.push`, `.sort` are *never allowed* on the original states. We can *only* perform those methods on *copies* of objects
> remembering that if an object contains other objects, the manipulation of sub-objects in "shallow copies" causes mutation in the original object reference.

### deep-freeze
We can use the `deep-freeze` development library to help us assert this in any jest tests we create, because we "freeze" the state like this: `deepFreeze(state)`, and any time we call state setters or reducers, it will fail the tests in the case of direct mutations.

## Uncontrolled Forms
Creating controlled inputs or forms involves taking the control away from the browser and managing the *state* of form inputs through stateful variables. This approach is highly effective for *dynamic* forms and inputs, in which we would like to be able to have the form change/react to form state. 
**Uncontrolled** inputs on the other hand, do not have stateful variables and event handlers associated to them. We lose out on the dynamic, reactive control, but do not need to manage the overhead of native browser inputs.
> We can still manage the *submission* of the form through submission events so we don't have to go through the `action` and `method` attributes and default events of the `<form>` element.
When we need to *retrieve* values from inputs on submission, we can do so the submission event, direct `ref`, or javascript selectors to select the inputs and retrieve their values.

## Action Creators
Instead of dispatching *static* actions, we can use action "creators", which are functions that can generate actions for dispatching. This further abstracts our logic, so that we don't necessarily need to complicate event handler code with properties that always exist for actions, and can pass targeted arguments.

```js
addNote = (event) => {
  event.preventDefault()
  const content = event.target.note.value  event.target.note.value = ''
  store.dispatch({
    type: 'NEW_NOTE',
    payload: {
      content,
      important: false,
      id: generateId()
    }
  })
}

//OR: action generator
const addNote = (event) => {
    event.preventDefault()
    const content = event.target.note.value
    event.target.note.value = ''
    store.dispatch(createNote(content))    
}
```

# `react-redux`
This package is an implementation of Redux specifically meant for React, as it allows us to pass the store into a "context-like" component, and gives us nifty *hooks* to interact with the store.

## useDispatch
This is a really nice hook because it allows any *provided* child components the ability to dispatch actions. It basically is a nicer way to abstract and avoid using the *store* itself as before, so instead of `store.dispatch(action)`, it's:
```js
const dispatcher = useDispatch()
//...
dispatcher(action)
```

## useSelector
Since the Redux store is a single object, we can "select" specific sub-objects using this hook:

```js
const notes = useSelector(state => state)
```
> We pass the *useSelector* hook a function that describes *how* to traverse the store's state object. In this case, the store only contains the collection of notes, so we can return the entire state object.

If, for example, we had two properties in the state object: `notes` and `filter`, we would "select" each of them like so:
```js
const notes = useSelector(state => state.notes)
const filterType = useSelector(state => state.filter)
```
Since the hook takes a function, we can "compute" or manipulate the state before it actually gets inserted into the variable:
```js
const notes = useSelector(state => {
	if(state.filter === 'ALL') return state.notes
	if(state.filter === 'IMPORTANT'){
		return state.notes.filter(note => note.important)
	}
})

//or, with desctructuring
const notes = useSelector(({filter, notes}) => {
	if(filter === 'ALL') return notes
	if(filter === 'IMPORTANT'){
		return notes.filter(note => note.important)
	}
})
```

# Types of React Components
In React, there are 2 component structures that describe the function of the component itself:
1. Presentational
2. Container

## Presentational
A presentation component are ones that are pretty clearly only for presentation, they do not handle any logic manipulation. They usually receive event handlers that allow them to propagate events up to their parents. Presentational components are quite "children"-like, they are really meant to compose visual or presentational JSX elements without managing the logic

## Container
On the other hand, containers are "parent"-like, they are parents to presentational components that define application logic, like state setters, reducers, etc. They define the event handlers that are passed to presentational components, and how each presentational component is configured.

# Many Reducers
Instead of having one monolithic, giant reducer to handle *all* actions, we create reducers per functional related group. 
Think of how states are shaped in non-flux architecture, we would have states for each "functionality":
```js
const [darkMode, setDarkMode] = useState(true)
const [images, setImages] = useState([])
const [isLoading, setIsLoading] = useState(false)
```

In the flux-based architecture, we want to create logical reducers for each type of functionality, otherwise, we start creating really gross logical dependencies between functionality that aren't necessary. 

This would logically complicate the dispatching, but Redux has a solution called `combineReducers` that allows us to create virtual groupings of reducers. It handles the reducer mux and de-mux.
> How this basically works is that it does effectively just run all combined reducers, but it makes that combination logic hidden and not prone to logical errors that we can make trying to combine reducers manually.
> If an action also required multiple reducers to fire on that action, then we can define the same action in multiple reducers, which will cause a wide-spread chain of reducer firing.

# `@reduxjs/toolkit`
This toolkit simplifies and abstract a lot of the repetitive boilerplating we need to do by putting it all into a comprehensive toolkit that can combine a lot of these seperate stores, reducers, combinations of reducers, into a single `configureStore` automation variable.

## `configureStore`
A shorthand for creating a store with combined reducers.
```jsx
import {configureStore} from '@reduxjs/toolkit'
import {Provider} from 'react-redux'

const store = configureStore({
	reducer: {
		notes: noteReducer,
		filter: filterReducer
	}
})
ReactDOM.createRoot(document.getElementById('root')).render(
  <Provider store={store}>
    <App />
  </Provider>
)
```

## `createSlice`
A tool that allows us to define our action generators.

# Toolkit and Mutability
When we create our action generators, reducers, we can suddenly start using *mutable* methods. This is because the reducers that we define are implemented under-the-hood using `Immer`, which is an abstraction API of state setting. 
- It utilizes proxy objects that we can mutate however we like, without mutating original state.

> This poses a small challenge when trying to `console.log` objects from within Immer-enabled reducers, because the typical state is wrapped by the `Proxy` object. We can use the syntax `JSON.parse(JSON.stringify(object))` to unwrap the proxy.

# Redux Thunk
Is a toolkit-bundled package that helps us abstract `async` functions and perform server-based operations away from actions. It's automatically included when we are using `configureStore`.

For action generators within the `createSlice`, we can abstract our communication dependent action generators into their own modules (or anywhere/file!). The most important part of *Thunk* that we care about is the ability to return *functions* from action generators.

```js
export const createNote = content => {  
	return async dispatch => {    
		const newNote = await noteService.createNew(content)
		dispatch(appendNote(newNote))  
	}
}

//...
dispatch(createNote(content))
```
> So, any action generators that are dependent on communication to the server can then invoke these action generators, which return a function that initiates server communication.

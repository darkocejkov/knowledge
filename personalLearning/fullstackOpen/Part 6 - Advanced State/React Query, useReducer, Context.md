There are plenty of non-Redux architectures that we can use to manage states in applications, and that means that we can use advanced ways to manage data fetching, use `reducers` out of the Redux concepts, and share state globally thorough the *context*.
___

# React Query
A package that deals with the typical problems of data fetching in React. 

we use React Query by setting up a "context provider" (`QueryProvider`) and a `QueryClient` that gets passed down to children, to query async. API information.
> to actually use the query, we need to use the `useQuery` hook.

```jsx
	const result = useQuery(    'notes',    () =>
		axios.get('http://localhost:3001/notes')
		.then(res => res.data)  
	)  
	
	console.log(result)
	 
	if ( result.isLoading ) {    
		return <div>loading data...</div>  
	}
 
	const notes = result.data
```
> `react-query` enables us to data fetch through dedicated hooks, that eliminates `useEffect` and `useState` hooks, because it triggers re-renders based on the status of the query.

## Queries vs. Mutations
Even though you typically *query* an API with payload data to manipulate/mutate data on-server, `react-query` seperates these operations into their own hooks.

In order to perform a "mutation", we `useMutation`:
```js

	

	const createNote = newNote => axios.post(baseUrl, newNote)
	.then(res => res.data)
	//...
	const queryClient = useQueryClient()
	const newNote = useMutation(createNote, {
		onSuccess: () => {
			queryClient.invalidateQueries('notes')
		}
	})

	const addNote = async (event) => {
		//...
		newNote.mutate({content, important: true})
	}
```
1. Without the `onSuccess` configuration when a mutation occurs, the new "note" does not get rendered to the screen
2. on success of mutation, this `invalidateQueries` call tells `react-query` to invalidate the state of a `query` with the key/name of 'notes'.
	1. In the previous example where we `useQuery`, we create a query called `notes`, which is all notes.

> What *invalidating* basically does is that it causes the query to run again automatically, without the use of `useEffect` or event handling, and is done in the mutation's `onSuccess` callback instead.

Instead of causing a full query, we can instead mutate the state from within the `queryClient`:
```js
onSuccess: (newNote) => {
      const notes = queryClient.getQueryData('notes')     
      queryClient.setQueryData('notes', notes.concat(newNote))    }
```
- We do so by getting and setting the query data of a specific query.

There's a lot more to `react-query` in terms of configuration, so that you can tailor it to your app's needs in data. Another example of enabled functionality is that *queries* will automatically re-fetch on window focus changes:
```js
useQuery('notes', getNotes, {
	refetchOnWindowFocus: false
})
```
> As a reminder, re-rendering your app should only happen when it *needs* to, based on the needs of your app.

React Query is a *server-state library*, it's meant to manage asynchronous operations and the state of the data, and depends entirely on query 
> Redux is a *client-state library*, it allows us to manage the state of React.

As we've seen, you can store data in React states using `useState` hooks, through Redux stores which are based on actions. Using `react-query` means that we maintain the state of the server in the frontend by querying and mutating server-side information.

# useReducer
Is a hook provided by React that is identical to the "reducers" we've used in Redux. It allows us to implement an action-based approach to setting states, with the ability to handle React state instead of Redux state.

The idea is identical in that we create a "reducer" function that takes a state and an action and chooses how to manipulate state based on those actions.

This allows us to organize and handle actions and state in a more Redux-like fashion, while being able to directly use React states. In the next section about *context* and passing down states, we'll see why using React state directly can be a very simple and intuitive approach.

# Context
Given an application that has many components, each requiring their own *props* from the parent, it can become really complex to deal with what is called **prop drilling**:
```jsx
	const [counter, setCounter] = useState(0)

	//...
	return(
		<Display count={counter}/>
	)

	const Display = ({count}) => {
		return(
			<Number value={count}/>
		)
	}
```
> Prop drilling is when we *manually* pass down props to child components through JSX attributes.
> This concept will take you far in the organization of React apps, but is very limiting when writing big applications with many interlinked components that require those props.
> What if you had to pass down a prop from the root, all the way down 10 components? Using context is great for 1 to 2 children, but in the event that your structure changes, ALL prop drills need to be refactored into somewhere else, making it even harder to re-factor.

The **Context** API is React's built-in solution to providing a "global state" access to components that require it.

In order to use it, we need to `createContext`. The context is an object structure (key-value pairs), and is embedded with a `Provider` component:

```jsx
const CounterContext = createContext()
//...
const contextObject = {
	//...
}
return(
	<CounterContext.Provider value={contextObject}>
		<Home />
	</CounterContext.Provider>
)
```

So, the *context* is *provided* to any wrapped children. 
Something else that is super important is that any provided children take from their *nearest* provider as the scope, and nothing else.

In order to use the context in the children, we need the `useContext` hook:
```jsx
import CounterContext from ''

const Home = () => {
	const {key} = useContext(CounterContext)
}
```
> The point is that the context's *value* can be anything, an Array, Object, number, string, etc ...
> We can use array/object destructuring to achieve a cleaner context environment.
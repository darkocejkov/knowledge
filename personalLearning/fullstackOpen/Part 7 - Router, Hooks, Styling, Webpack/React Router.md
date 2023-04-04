All previous parts manage the state, views, and components of a single application, which has had only a single page. A notes application that is *only* the notes application, there's no URL-based views.

If we are developing an SPA with multiple "pages" or URL endpoints, the only way we can do this is through component-based conditional state rendering. It's quite difficult to manage the browser's URL changes in React because it's a browser API and is not tied directly to JS.

There's many problems with using this old, state-based method and we need a better way.

`react-router-dom` is a package that ties URL endpoints for the frontend to specific views, so we can execute different "routes" based on endpoints, and hook into changes to the URL and "history".
___

# Routing (v5)
`react-router-dom` specifically enables the ability to route different views or components based on the URL that your browser is serving.

> In non-routed applications, changing the URL to a sub-resource typically *refreshes* the page because it attempts to grab a new resource from the server. Instead, the router is able to keep the application stable because it synchronizes the HTML5 History API to internally route components based on the URL, using JS.

## Components

### Link
`<Link>` is a router-specific element that renders into an `<a>`, to which we are able to pass href-style relative/absolute URLs into:

```jsx
<Link to={`/notes/${id}`}>{id}</Link>
```
Without the Link component, attempting to use a basic Anchor element causes weird things to happen. The Link component uses `react-router-dom` directly to manipulate the history and impose route changes.

### Router / BrowserRouter
Routes are basically conditional renders, with the stipulation is that they are tied to specific history/URL paths.

```jsx
<Router>
	//...
	<Routes>
		<Route path='/notes/:id' element={<Note id={id}/>}/>
		<Route path='/notes/' element={<Notes />}/>
		<Route path='/users' element={
			user ? <Users /> : <Navigate replace to='/login' />
		}/>
		<Route path='/login' element={<Login />}/>
	</Routes>
</Router>
```
> We can *parameterize* URLs by "binding" the parameters with the colon `:`.

- When the `/users` route is navigated to, the route conditionally renders components within the route itself.
	- If something exists in the *user* state, then the Users component is rendered, otherwise, it renders a Navigate component, which, when rendered, replaces the history to navigate to the Login route.

## Hooks

### useNavigate
Allows us to manually set navigation/history paths.

### useParams
Extracts the *parameters* from the URL based on their defined parameter name in the route

### useMatch
A more manual way to access URL characteristics by *matching*.
```js
	const match = useMatch('/notes/:id')
	const note = match ? notes.find(note => note.id === match.params.id) : null
	
```
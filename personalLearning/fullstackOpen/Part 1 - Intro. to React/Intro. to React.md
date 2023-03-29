Considering I have quite in-depth, intermediate knowledge about React, I will not go as in-depth on concepts that are already familiar.
___
# create-react-app
Above and beyond the easiest way to start a React project. You can also use *Vite*, but the CRA is by default, no-config the simplest and does not need to be "installed"

# Rendering
React is an example of client-side, runtime HTML rendering. This is clearly shown through the filestructure of any React app, as there is a `/public` folder that contains all the final resources that servers actually serve.
Within the `/public` folder, the `index.html` is the root HTML file that will be "injected" into. It's the base, the foundation of the HTML UI that we create - because everything else is defined *declaratively* within JavaScript.

"Components" are merely semantic definitions for distinct groupings of JavaScript. If we are using *class-based* React, components are defined as extensions to the `Component` class and have a more rigid structure. However, in *functional* React, it's even simpler and a Component is a single function that provides a "template" or "boilerplate" which is the result of the function, and is the component.

# Functions as "snapshots"
Since I've had trouble getting into the concept of hooks and functions in the past, as shown in the detailed Documentation break-down in [[React]], this should be a very blank reminder. Functions are evaluated at *runtime*. Functions are not *classes* in that we need to always define *states* for ALL displayed content.
Components in the lens of functions means that when React renders components, it will *evaluate* the function, and it runs in a typical, linear fashion. I'll show you concretely what I mean.

```jsx

function Bad(){

	const [date, setDate] = useState(null)

	useEffect(() => {
		setDate(new moment())
	}, [])

	return(
		<>
			{date && date.format()}
		</>
	)
}

function Best(){
	return new moment().format()
}

```
> The point here being that I used to believe ALL components and all "visually rendered" things must be in the state or set in the state using effects. That's all wrong, it's just stupid. This entire misnomer was perpetuated by the fact that I did not read the React documentation sooner - even without the new docs, this would've been extremely clear.

> The best practice way of thinking of functions as components is that *states* are things that we *need* to store between renders, like the *state* of the component concretely (OK, ERR, LOADING, etc...). What we *don't* or *shouldn't* store are transient, computable values from those states. It's entirely redundant to store something that is calculated every render because it doesn't need to be remembered between renders.

# JSX
JSX, or JavaScript with XML is a language developed to make it SO much easier to write complex things in React. It's basically XML/HTML with the addition of allowing embedded JS. Instead of continuously using the `React.createElement(...)` syntax to create elements, we can be much more elegant and use JSX to do so.

# Components
- Are meant to bring encapsulation and organization into JavaScript and React. You seperate distinct visual components into their own classes/functions. It's important to *seperate their concerns*, because a Button component only cares about the contents, and events of the button, and not of its parents. 

## Passing information to components through `props`
- Any component in its signature can receive an object called `props` as in the example: `(props) => ...`
	- components that ingest this object can utilize any attribute property defined on it

```jsx
const Child = (props) => {
	console.log(props.a)
	console.log(props.b)
	console.log(props.c)
}

const Parent = () => {
	return(
		<>
			<Child a='a'/>
			<Child a='a' b='b'/>
			<Child a='a' b='b' c='c'/>
		</>
	)
}

const ChildDestructured = ({a, b, c}) => {
	...
}
```
> In this example, we see that through JSX, we defined the 'props' that we pass down from the `Parent` component is through HTML-like attributes. Props can be numbers, objects (any, functions, arrays, json, ...), strings.
> As a bonus, we can make our code much cleaner and "type-safe" by *destructuring* the props object. This way, if we pass child a prop `d`, it does not receive that prop unless it destructures it, making it very easy to control and have that visibility into what is actually being passed down.

# Syntax & Rules for Components
- All components must *start* with a Capital letter `App`, `Footer`, `Button`.
- Any and all JSX must have a single root element, meaning that any "sibling elements" must have a *common parent*.
	- we can use `React.Fragment` elements as a way to work-around this, or the shorthand `<> </>`
- Any returned JSX must not embed *objects* to render. Absolutely cannot render pure JS objects, because they are NOT primitives. We can render values of objects given that they are primitives, like strings or numbers. 
	- In order to render an object, it should be parsed to be prepared for rendering, or be passed to a component that can do that parsing itself.


# [Exercises]()
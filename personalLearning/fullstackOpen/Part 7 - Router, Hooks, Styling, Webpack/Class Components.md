Modern React ^16.8 allows the use of *hooks*, which makes functional React possible. However, before this magical version, all components *must* have been composed of JS Classes.

Functional components are *equivalent* to class components, they perform the same job through different means - thus, they are functionally identical. However, in terms of their *paradigm* of development, they are *very* different. Yet, it's still important to understand how to read and break-down old class-based React code.
___

```js
class App extends React.Component {
  constructor(props) {
	    super(props)
	
	    this.state = {      
		    anecdotes: [],      current: 0    
		}  
	}
	
 componentDidMount = () => {    
	 axios.get('http://localhost:3001/anecdotes')
	 .then(response => {      
		 this.setState({ anecdotes: response.data })   
	  })  
}

  render() {
    if (this.state.anecdotes.length === 0) {      
	    return <div>no anecdotes...</div>    
	}
    return (
      <div>
        <h1>anecdote of the day</h1>
        <div>          {this.state.anecdotes[this.state.current].content}        </div>        <button>next</button>      </div>
    )
  }
}
```
Here's a port of a previously functional-based component into a class-based one. 
1. Components *extend* the `React.Component` interface/class.
2. Components have "constructors"
	1. We initialize the "state" of the component as a variable, typically an Object
3. Components have a *render* method, that allows them to be rendered - it's their JSX output.
4. We must always reference the *state* by using `this.state`.
5. We are using *lifecycle methods* to "hook" into the current React-based status of components.
	1. Whether they are *going* to be mounted, *have* mounted, *will* unmount, *have unmounted*, *have updated*, etc... It's based on the lifecycle of the component.
6. We must use the implicit method `this.setState`, to manually  trigger state changes.
	1. The arguments to `setState` involve the name of the state's property we would like to change.

## Class vs. Functional
Class and Functional React are identical in terms of their output, but functional React offers a cleaner way to write the same code, and when you fully understand the paradigm of functional components, they are super simple to understand with states, effects, and hooks.

If you're using a version that supports functional components, it's highly recommended (even by React team themselves) to use Functional components in newer versions of React, as the future of React's futures lie in hooks.
> That being said, there's no need to convert ALL class-based code into functional ones.

## Virtual DOM
Given that the root/base of all React projects is `index.html`, which has nothing until runtime, we're not actually manipulating the *real* DOM when we use React. This is because we're declaratively defining our UI and functionality, while React works in the background *simulate* the real DOM using a "shadow" or "virtual" DOM. This way, it can manipulate and calculate changes to the virtual DOM and figure out the best way to change the real DOM efficiently.

## Architecture of React Applications
React is *not* a Model-View-Controller pattern, because React really only cares about the *view*, the UI. React is not a "framework" for frontend, but a "library".

# Vulnerabilities

## Injection (SQL, Any)
The ability to inject code that runs on the runtime. Very typical and simple in SQL:

Original:
`SELECT * FROM Users WHERE Name = '" + userName + "';"`
Injected:
`SELECT * FROM Users WHERE name = 'Arto'; DROP TABLE Users; --`
- They are typically solved by *sanitization*, meaning that any user input should be checked and injected into the query if its safe, or will be treated as string input, and not executed as code.
	- When dealing with SQL and other such packages, they usually have some sort of templating or parameter insertion functionality that *automatically* sanitizes input.

## Cross-site Scripting (XSS)
The ability to inject JavaScript code to run as code and not text.

## Using NPM to track vulnerabilities
NPM  can automatically tell us what packages and their respective versions have known vulnerabilities, and which versions fix those. 
- use `npm audit`

# Trends

## Typed JavaScript
- JavaScript is weakly typed, meaning we do not have to care about the types we assign to our variables, this makes it super fast and easy, but on the other hand, enables more and more bugs because there's no way to "enforce" the types that we pass to components and functions to verify this at compile-time.
	- PropTypes adds a typing system for component props
	- TypeScript is a superset of JS, which allows for full-depth static typing

## Server-Side Rendering, Isomorphic, Universal Code
- Client-side rendering (React, JavaScript) has downsides for high-level desires like SEO, because it depends on a long initial load and computation time at the *start*.
- To combat this, we can have React render its first pages and content on the server very fast and pass that down.
	- Isomorphic applications render on both front AND back ends
	- Universal code applications can do either at a time, or both at once.
- `Next.js` is a framework on top of React ([[NextJS]]) that allows us to build universal code applications.

### Progressive Web Apps
- Almost like "installable" web applications, that should work perfectly on and offline, with or without internet, with encrypted network communications.
	- `create-react-app` has a PWA template.

## Microservice Architecture
- Simple APIs are typically *monolithic*, meaning that ONE application makes up and runs on a SINGLE server that serves all the API endpoints.
- Microservice architectures sound quite simple, they are a collection of various *services* that run seperately to create several points of contact. 
	- A *user service* is responsible for registration and authentication, blog services perform CRUD of blog objects and data, etc ...
	- Services do not *share* a database
- Microservice architectures scale really well, but are logically, much more complex to orchestrate.

## Serverless
- AWS Lambda, Google Cloud functions, Azure
- Enables execution of individual functions in the cloud
- Less about the fact that there's "no server", but rather about the structure of the server.
	- It enables a higher abstraction to work with, because you don't need to care about the routing of HTTP requests or database relations, because the could infrastructure does all that for you.

# Packages!
React is a really beautiful and extensible framework/library, it can get *very* custom, and you can definitely develop your own solutions to problems. 
However, it's definitely *not* necessary to do so! The beauty of React (and especially NPM) is that you don't have to continuously re-invent the wheel (unless you want to, of course). There's so many packages that just work out-of-the-box, and also provide *tons* of customization.

# [React Patterns](https://reactpatterns.com)
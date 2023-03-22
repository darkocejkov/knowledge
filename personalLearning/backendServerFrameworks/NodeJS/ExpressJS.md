# ?
Express is a *package* for NodeJS that allows you to *easily* handle HTTP requests through a **middleware** configuration. Essentially, it adds additional functionality on-top-of NodeJS.

You *could* implement your own methods to handle HTTP requests directly in NodeJS, but Express is there to make it super simple, and super easy to do this. It's become an industry standard because it does its job so well, and makes implementing complex API endpoints a breeze.

# Middleware Stack
Express is built on the pattern of *middleware*. [[Node Explained]] describes how NodeJS is a runtime for JavaScript that is meant to run server-side commands in JS

Express faciliates bridging data between HTTP requests from the client and sending back HTTP responses from the server easily. 

Middleware as develop in Express, is a "stack" of functions that runs on NodeJS. It's a little perplexing at first, but all middleware does is this:
```js
	use(endpoint?, function(request, response, next), function?)
```
> Essentially, middleware defines a relationship between an *endpoint*, (like some `URI`) and a resulting function. When the middleware runs, it basically defines that when it receives some request at a specific endpoint (endpoints are *optional*, if none is specified - it *automatically* runs.), then the related function will be triggered.
> This is similar to the concept of *events* in NodeJS, except the "event" is when *any client* makes a request at that endpoint, rather than some programmatic NodeJS event.
> That being said, Express *abstracts* the events of NodeJS to accomplish what it does

```ts

use(express.static())
use(express.json())

use(() => one())
use('/milk', (percent: number) => ...)
use('/orangejuice', (pulp: bool) => )

```
	In this example, we define a middleware *stack* using the "use" keyword to define relationships between endpoints and functions.

When the NodeJS server receives some HTTP request, express runs through the stack (top-to-bottom) executing all middleware that is appropriate - like those without specific endpoints and those whose endpoints match the requested URI.

This illustrates the "chain of command" or "message chains" that happens when some request arrives. It's a series of functions that are applied to the request, or rules that the request is "filtered" by.
![[Pasted image 20230321152123.png]]

The point of creating middleware *at the top of the stack* that transform the request is to enhance and abstract ways to use the request, because HTTP requests aren't in easy-to-use formats, so we do things like parse their bodies, enforce CORS, de/serialize cookies from the request, session information, etc.

# Middleware Functions 
Middleware functions typically follow this scheme:
```js
const app = Express()

app.<use | get | put | post | delete>(route?, (request, response, next) => {
	request.body
	...
	response.send()
	//OR
	next()
 }, function(req, res) => {
	 ...
	 response.send()
 })

```
1. We can utilize the follow methods of the express package:
	1. `use` for generic middleware
	2. `get, put, post, delete` for HTTP request middleware
2. they associate a route (optional) to function(s)
	1. more than 1 function "callback" can be passed, because we are dealing with a "stack" of middleware we can use chains of callbacks to accomplish tasks

Middleware functions have 2 required parameters:
1. `request`
	1. holds information about the request that the callback was invoked for
2. `response`
	1. allows express to deal with sending back information to the client as a response

## next
Is the 3rd parameter to middleware function that allows us to invoke the *next* function in the stack.

# HTTP Method Routing
When we use express, we can setup pre-defined middleware for dealing with HTTP requests, specific to their:
1. route
2. method

When we create an HTTP middleware, anytime the middleware stack *runs*, and there exists some request that matches these conditions, it runs the associated function.

> This essentially allows us to create a "middleware microservice API", because we specify mappings from routes to functions, which we can use to accomplish various tasks on the server.

# Chained Routing
```js
app.route('/item')
.get(fn => {})
.post(fn => {})
.put(fn => {})
.delete(fn => {})
```
Instead of creating 4 seperate middlewares, 1 for each method, we can use chaining to create 1 route with 4 different methods

> No more do we have to create routes like `/item/delete` or `/item/create`, since they are *redundant* as the method describes the action we wish to take.

# Route Parameters
We can create "dynamic" routes using parameter binding in the endpoint. This means that we can create a structure for some endpoint and can pull information from the endpoint itself.

We can bind parameters by their name in an endpoint by using the colon `:parameter` scheme:
```js
app.get(`/item/:id/subitem/:uid`)
```
These parameters can be *pulled out* from the `request` object as in `request.params`, which is a key-value pairing in which the key is the literal name.


# Error Handling
Since we are using a Middleware stack, we don't necessarily have to deal with errors *on the spot* when they are created, but can rather propagate errors down the stack and catch them using an error middleware function. This way, we can create a composed error handler, with detailed information about the error.
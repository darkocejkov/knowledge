___
Node is a JS runtime that allows us to execute JS code. Node is designed to be used on servers, and not just browsers, so it has a global object that can do very many things, like file system tasks, data manipulation, etc.

We can "run" a JS file by using the `node` CLI, which will execute the JS file in the context of the Node global object.

# Simple Web Server
```js
const http = require('http')

const app = http.createServer((request, response) => {
  response.writeHead(200, { 'Content-Type': 'text/plain' })
  response.end('Hello World')
})

const PORT = 3001
app.listen(PORT)
console.log(`Server running on port ${PORT}`)
```
> Does not *require* Express.
> Allows us to receive HTTP requests, and serve HTTP responses. 
> The `.createServer` registers an event handler which will fire on EVERY request to the server (currently).

# Express Server
Building a simple web server with the HTTP object is simple to start, but gets more and more complex when you start serving lots of information, have different types of requests and responses, and so on. 
Using an *express* server is much easier, because it allows you to easily insert "add-ons" through *middleware* functions. It's even easier to set up API endpoints to specific routes for specific functionality.
-> Why? because Express is designed to make HTTP requests and responses easier. A lot of the overhead of knowing how to exactly format HTTP headers and data is handled by Express - so you just have to declare what happens when a route is requested, and Express handles the delivery.

## node-repl
`REPL` is an acronym for "Read-Evaluate-Print-Loop" which is a very useful line-by-line tool to test JS code. It does exactly that, it reads JS code, evaluates it, prints the response (if any), and then loops.

> node-repl is a package that allows us to easily create a Node-based REPL session in the command line just by using the `node` CLI.

## nodemon
An essential package in the *development* aspect of NodeJS. Anytime we start a server using Node, it continuously runs, and anytime we make changes - we must stop and restart the server to implement those changes into the server that's running.
`nodemon` is a development dependency that is a *wrapper* for the `node` CLI, because it "watches" for changes in the code and will automatically restart the server.

# REST
> REpresentational State Transfer, an architectural style

Items or "things" in the view of REST, are called *resources*.
Resources are "unique" by some identifier, like an ID, that allows us to ask the RESTful API for resources based on those identifiers or a general structure.

Take for example *notes* as resources, stored in JSON format (strings). Our RESTful API could be reached at the `/api` endpoint. If each note is a resource, and the structure of *all* notes would be unified in some collection, then `/api/notes` would be responsible for the entire collection, while `/api/notes/10` would be a single note with identifier "10".

We *could* deliniate all the different actions on these resources from the endpoint:
```js
app.get('/get/notes/:id')
app.update('/update/notes/:id')
```
> The stupidity in this example is that we have created redundant routes and naming which will get confusing. We have endpoints related to a collection, or individual resources, for which we can remove redundancy from the route and just use the HTTP verb.

A large point that remains is what *exactly* is REST? Have we created a RESTful API? Since it's an *architecture*, there's nuance in REST APIs, and ours is *closer* to a "resource-oriented architecture" rather than a RESTful, but there's no point in being semantic.

## Parameter Binding
We can bind parameters to endpoints in Express as in the last example, by using the `:key` syntax in endpoint definitions.
> Any request values that are parsed from the endpoint route can be found in an object called `request.params` by the name of the key itself.
> > Parameters are *strings*

## Not Founds
```js
if (note) {    
	response.json(note)  
} 
else {
	//response.statusMessage = "No note found for id"
	response.status(404).end()  
}
```
> In the case that we request a specific resource and none is found for a given unique ID, then this is a good practice for setting the status of the response so the frontend can handle the response gracefully.

# Testing Backends
When we create backend functionality and resource endpoints, there are sometimes no way to invoke these endpoints through the browser's address bar, mostly because endpoints might require data in the *body* of a request, which is not possible through simple browser URLs.

It's also not entirely realistic to have to implement frontend buttons and form submissions to test backend - how would backend developers who cannot create frontend do so?

Instead, it's much more succinct to use API testing tools.
- cURL for the CLI
- Postman for the GUI
- IDE / Editor Extensions
	- [WebStorm](https://www.jetbrains.com/help/webstorm/http-client-in-product-code-editor.html)
	- VS Code

# JSON Requests
Express manages a lot of overhead for us, but we need to give it additional instructions on how we want the `body` property of requests to be parsed. 

Express can *use* middleware functions that operate on the requests before they reach the endpoint callbacks (middleware as a stack: [[Node Explained]]). 

Thankfully, Express comes bundled with `json-parser` and we can use it through `app.use(express.json())`. This way, we can then easily use the `request.body` property on incoming requests to get data in JS objects format.

# Importance of Headers
Headers are very important pieces of metadata that tell servers and clients what kind of data, and the constraints of the HTTP.
A very common problem is the mismatching of the `Content-Type` header. If we expect Express to receive JSON - if client requests use any other Content-Type, then Express does not parse the content as JSON.

We can "get" the values of headers through the `req.get()` API, for which we can request the name of a header and be returned its value.

# HTTP Request Standards
HTTP Requests have two properties associated with them:
1. Safety
2. Idempotency

## Safety
Refers to the actions which *do not cause side-effects* by altering the state of data, but rather only *retrieve* data.
HTTP methods that should be safe are:
- GET
- HEAD
	- GET without data, returning only the *status* code and response headers.

## Idempotent
Similar to the idea of purity, the outcome of identical requests are the same for a single request.
- GET, HEAD, PUT, DELETE

> POST is neither *safe* nor *idempotent*.

# Middleware
Are order-based middle-man functions that run on requests to parse, or check contents. `json-parser` for example, is middleware that we assigned in Express using the `app.use(express.json())` call. Any requests Express gets have middleware functions called in the order that they are defined in `.use`.

Technically, the routes that we define are "middleware" in themselves, but specific to routes and HTTP methods.

Middleware isn't "special" to using packages or routes, we can easily define custom middleware functions:

```js
app.use((request, response, next) => {
  console.log('Method:', request.method)
  console.log('Path:  ', request.path)
  console.log('Body:  ', request.body)
  console.log('---')
  next()
})
```
> Middleware that logs the `request` object's properties
> Should be called *after* the `json-parser` middleware, otherwise `request.body` is not defined.
> the `next()` function invocation is a middleware function that runs the *next* middleware in the chain.

```js
app.use((request, response) => {
  response.status(404).send({ error: 'unknown endpoint' })}
```
> Here we've defined a middleware that should be defined at the *end* of the middleware stack, because it sends a response when this middleware is ran.

## Sending Multiple Responses
Is not something that is possible. For every request, only ONE response should be sent, and no more. If we avoid sending multiple responses, there may be areas in logic where we don't *return* after we send a response, causing other code to execute and send other responses, crashing the backend.







How should we create the file structure of the backend to make it logical in module seperation?

[Seperating server and API declarations](https://dev.to/nermineslimane/always-separate-app-and-server-files--1nc7)
___

```bash
├── index.js
├── app.js
├── build
│   └── ...
├── controllers
│   └── notes.js
├── models
│   └── note.js
├── package-lock.json
├── package.json
├── utils
│   ├── config.js
│   ├── logger.js
│   └── middleware.js  
```
> - *index.js* is the root of the project
> - *app.js* is where we link all other middleware and controllers
> - within the controllers directory, we have object-specific controller functionality
> - we define the Mongoose models in the models folder.
> - the utils directory is for helper and custom functions
> 	- *config.js* for passwords, environment variable, config objects
> 	- *logger.js* defines custom wrappers for the `console` object
> 	- *middleware.js* holds the custom middleware we defined, like 404 handlers for unknown endpoints, error handling, etc...

# Testing Node
- Testing each route, each database manipulation manually is great way to verify things are working, but whenever you make a high-level change that could possibly affect all these small low-level things, we need to re-test. 
- Instead of manually testing, we can create *unit* and *integration* automated tests using the industry standard: **jest**. 
	- Jest can test both React and Node applications, so it makes it very flexible
```js
test('reverse of a', () => {
  const result = reverse('a')

  expect(result).toBe('a')
})
```
> Without knowing what `reverse` actually does, the test is simple - we invoke the function on same case, and we assert what the result *should* be.
> - It's really easy to just think of creating a single test, but creating good and meaningful tests is an art in itself. 
> - Tests for a single *unit* should go into many cases, edge cases, common cases, etc.

In Jest, we can group tests to "describe" a unit:
```js
describe('average', () => {
	test('of one is value itself', ...)
	test('of many', ...)
	test('of none', ...)
})
```
Essentially, we create and group tests to build a "truth" for a unit, things that should *always* be true, regardless of implementation. It should be able to catch implementation-specific things like what happens if we give no arguments, wrong types, etc.

## Personal Experience
Speaking anecdotally, developing an application in Node + React with absolutely *no automated testing* was quite possibly, the worst thing I did not know about. Regardless of the blame or responsibility, the fact is that there was no automated testing methods to cover even 1% of the code we created.
- This caused many invisible issues that no one would find because of new changes, which are later exposed and everyone is freaking out
- If we had an automated testing step before any changes are made, we would have caught so many errors before they ever occurred.
- It avoids any silly mistakes that could propagate to the codebase, like accidental letters, etc.

# Testing the API
How can we automate the backend API through HTTP requests and responses? Jest is a testing *framework* so it can handle a lot of things - but we still have to add other packages to help us do it easily. Jest simply allows to create the tests and assertions, while something like `supertest` will allow HTTP request testing.

## Testing Databases
If our API is uses a database, these automated tests create data and manipulate it. It's best practice to use a *seperate database* entirely, which is most easily done through in-memory (installations) or Docker images. 
> Not only does the testing create and change data, the testing can be intense in how it connects to the database resources.

## Testing App API
```js
const app = require('../app')
const mongoose = require('mongoose')
const supertest = require('supertest')

const api = supertest(app)

test('notes are returned as json', async () => {
  await api
    .get('/api/notes')
    .expect(200)
    .expect('Content-Type', /application\/json/)
})

afterAll(async () => {
  await mongoose.connection.close()
})
```
> Supertest is pretty interesting, because it ingests our *app.js* module (our Express application), and creates a **superagent**, which can make and receive HTTP communications
> - Supertest does NOT need to server to be listening on a port already, because it does so automatically.

## State of Database
Testing responses from APIs means that we are essentially testing against the state of the database. If we want to create simple, but effective tests, then we can programatically trigger pre-test actions to be taken, like clearing the database entirely to have the database be in the same state every test run.

Also, if we are testing about database specifics, like the content and not just that calls were successful, then it's important that tests are run *in-band* (sequence, non-parallel).

# Dealing with Asynchronous Code
Is a syntax introduced in ES7, which allows a very simple and clean way to handle asynchronous processing.

1. Async callbacks
```js
asyncFunction(() => {
	asyncFunction(() => {
		asyncFunction(() => {
		
		})
	})
})
```
> When code relies on callbacks, it is possible to create **callback hell**, where async functions are nested. This is semantically great, because it's very visual in how they're executed, a "chain"

2. Promise Chaining
```js
asyncFunction()
.then(...)
.then(...)
.then(...)
.then(...)
.catch(...)
```

3. Async/Await
```js
async doAsync(){
	await asyncFunction()
	// "synchronous" code

	await asyncFunction()
}
```
> async/await is a very beautiful syntax that allows us to write asynchronous functions as if they were synchronous
> - they are NOT synchronous, they just *look* like it.
> - we can *only* call await in functions that are 'async', and can only await things that *return* promise.

## Dealing with Errors in async/await
It's recommended to use the `try/catch` logic:
```js
try{
	const data = await errorProneFunction()
}catch(err){
	next(err)
}
```
> Using this idea, we can successfully isolate code that can throw exceptions, and handle it gracefully by passing the exception to the *next* middleware, and since we pass an arugment - it gets sent to the error handler.

## Advanced async/await error handling
Since the above method of handling async errors can be a bit clunky, and all our try/catches are doing is passing the exception to the error-handler middleware, then we could refactor and refine this process further.
If we install the `express-async-errors` package and require it, we no longer have to *wrap awaited functions in try/catch* as long as the routes we use are considered `async`. the `express-async-errors` will 'inject' the error handling, so we only have to care about writing the main body of routes.

# Testing Utilities
When creating tests, it's important to know what we should "extrapolate" or "factor" from the operations to make creating tests easier.
The ability to easily create new objects with random properties, save them to the database, etc.

1. Non-existing ID
	1. in the case of MongoDB, we can create a document, save it, store the ID, delete the document, and return the unique ID which is *guaranteed* to not be in the DB anymore.
2. Get All
	1. simple and effective call to fetch all objects

These are just examples of basic functions that can be abstracted to help us deal with data, especially if we wanted to just create an object with random data, or create an object that *should* cause an error.

# Promise Arrays
Dealing with promises and asynchronous functions can be tricky when we want to deal with a dynamic, or collection of them. Imagine we want to loop over some data array, creating objects for them in the database.
Instead of using a loop to create the object, initiate an async function, then only re-loop until after the async finishes, we can use the `Promise.all([Promise, ..., Promise])` function meant for this.

Here's an example:
```js
const noteObjects = helper.initialNotes
    .map(note => new Note(note))
  const promiseArray = noteObjects.map(note => note.save())
  await Promise.all(promiseArray)
```
> We have a list of objects to create with MDB Models, and we want to save each of them into the database. 
> We can use `map` to create an array of *promises*, which we pass to the `Promise.all` method, which creates a *single* promise out of the array of promises we give it, so that the total promise can only be fulfilled once every sub-promise is resolved.

As an additional note, if we care about the *returns* of those sub-promises, the `Promise.all` method returns a *list* of resolved values, in the original order.

#### `Promise.all` executes in *parallel*

If we instead would like each promise to be executed sequentially, we should use the `for(... of ...)` syntax.

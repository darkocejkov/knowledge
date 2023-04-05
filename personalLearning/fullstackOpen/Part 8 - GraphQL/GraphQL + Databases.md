If we remember back to MongoDB + Mongoose, we were able to store non-volatile information in *documents* in MongoDB. We used Mongoose to set up a schema for the various types of objects to create a rigid structure for the flexibility of documents. 

Both GraphQL and Mongoose use schemas for their own *seperate* purpose, the schemas for both should be quite similar given that they should represent the same data and structure of that data, but don't necessarily need to be exactly the same. 
___

## Asynchronous
- Since the interface between GraphQL and the data is now seperated, it requires asynchronous operations. 
	- Apollo Server can see that certain Mongoose APIs like `find`, `findOne` return *promises*, and thus we can do the following syntax to really easily return the result of the promise, without worrying about anything else (since Apollo handles the async)
```js
allPersons: async (root, args) => {
  return Person.find({})
},
```

![[Pasted image 20230405134401.png]]

## Server Context
- using the `startStandaloneServer` call allows us to specify additional `context` property:
```js
startStandaloneServer(server, {
  listen: { port: 4000 },
  context: async ({ req, res }) => {
	  const auth = req ? req.headers.authorization : null    
	  if (auth && auth.startsWith('Bearer ')) {      
		  const decodedToken = jwt.verify(auth.substring(7), process.env.JWT_SECRET)      
		  const currentUser = await User.findById(decodedToken.id).populate('friends')      
		  return { currentUser }
	  }
  },
}).then(({ url }) => {
  console.log(`Server ready at ${url}`)
})
```
> the code within the *context* section allows ALL *resolvers* to receive the returned value from this context as their *third* parameter:
```js
Mutation: {
	addPerson: async (root, args, context) => {
	},
	addAsFriend: async (root, args, {currentUser}) => {
	}
}
```
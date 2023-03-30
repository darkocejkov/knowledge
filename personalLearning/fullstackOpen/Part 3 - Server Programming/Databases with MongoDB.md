Databases can be pretty elusive because they're complicated. They have many different ways to query them, to connect to them, to manage them.

Databases are essentially just software programs like Excel that manage data storage. They have specific protocols to access and edit entries in data, and different types of databases use different data structures to store data.

We can host databases as their own *service* and require a network connection. We can "install" a database program on the machine of the server and use that local database. We can use cloud databases from AWS or MongoDB Atlas.

If we really reduce the complexity of databases, all they are is some process that understands how entries are stored, how to find entries, how to manipulate entries. It's really nothing more than a large text document holding all data in storage, and how it can change this document.

Excel could be considered a "database", as long as we set up the format of the columns/rows in a way so that we can easily use data.
___

# Relational Databases
The most typical and standard way to organize lots of data is in a relational database. The constraint in relational databases is that we have many records which are *related* by some key. 
For example, think of database tables like User, Books, UserBooks.

Users describe the collection of Users, which all must follow the same schema of User. Books describes a collection of all the books within the system. UserBooks is a collection that relates Users, to Books, with the semantic representation of a User logging a Book to their account.

Each table (User, Book, UserBook) has a primary *key*, which guarantees that all entries within each table have a unique identifier that can be used to "index" them. Think of an algebraic function - they are only valid when one value of $x$ maps to one value of $y$, no two records may share the same primary key value, because if you are looking for a single record with that ID, you're going to get two+ records.

## Querying
Relational Databases often use forms of SQL (Structured Query Language) to access and manipulate DB records.
SQL works because records are inherently unique, and relate to other records. 

## SQL
SQL is a large family of languages, but the most common factor is that any databases that use SQL are relational databases.
- Oracle
- MySQL
- Microsoft SQL Server
- PostreSQL

## NoSQL
Is a shorthand for "non SQL" which describes databases that are not relational, and do not use SQL. 


## Non-Relational Databases
Relational databases are organized into tables, which are rigid and non-flexible. Each entry must conform to the schema of the table, and require significant amounts of planning in terms of data models.

Non-relational databases are more recent, and instead of organizing data into entries in a table, organize data in different types of data structures:
- Document-based:
	- MongoDB, CouchDB
- Key-Value Pairs:
	- Redis, DynamoDB
- Wide-Column
	- Cassandra, HBase
- Graph
	- Neo4j, Amazon Neptune

## Pros + Cons to NoSQL
Of course, different structures offer different benefits and downsides. 
- NoSQL scales *horizontally* rather than *vertically*.
	- Vertical scaling means you cannot distribute the database over multiple servers, and have to upgrade servers. Horizontal means that you can create many cheaper and smaller server instances  to distribute the database
- Flexible Data models
	- Databases are not bound to data structure schemas, or rigid structures.
- Faster Queries
	- since SQL *normalizes* and creates virtual tables for joins, SQL can scale downwards in performance. NoSQL is optimizes for querying without joining.

Drawbacks:
- No support of ACID (Atomicity, Consistency, Isolation, Durability) out of the box
- Relational databases reduce data duplication (redundancy) by relating entries. NoSQL cannot provide that, and can be larger in memory
	- however, this is a small one since you can compress stored data, and storage isn't expensive
		- especially because you can scale horizontally

## Thinking about SQL vs. NoSQL
SQL is so normalized to think about storing data. It's rigid, and has a lot of purpose. 
The problem is that SQL requires a lot of design in terms of the data model, because you need to create and manage the fields of tables.
In a very simple system, it's typically not worth creating such a rigid structure or data model, because there's no benefit to *normalizing* relational data. 
Sometimes, you just need a solution to store data in a non-volatile way.

# MongoDB
[Overview](https://www.mongodb.com/docs/manual/core/databases-and-collections/)

MongoDB is a *document-oriented* databases. It stores data in "documents", in a BSON (Binary JSON) format.
A database holds 1+ collections of documents, which a *collection* relates to a *table*.

As such, document-oriented DBs are considered a "NoSQL" database, because 

Documents within a collection do *not* have to conform to the same "schema", so there's a very flexible schema structure that depends on the data in the collection.

## Mongoose
Is a package built for interacting with MongoDB, which is a high-level API that allows us to have more semantic interaction.
Mongoose is an *object document mapper (ODM)*, which allows us to interface with MongoDB using javascript objects (it maps JS objects to documents ...)

### [Schemas & Models](https://mongoosejs.com/docs/index.html)
A schema is like a class that describes the structure of documents - a Kitten, a Dog, an Animal. 
Schemas include the *name* of the properties, and the associated *type* (String, Boolean, ...)

Schemas and Models go together, as we create a Schema and compile the schema into a Model with a given name.

Thus, a Model is the *complete* class-like definition for documents that include the structure, and the "class" name. Documents are *instances* of the Model, like Objects are instances of the Class.

Models have methods associated with them, either *custom* ones, defined in the schema (before compiled into the Model), or built-in methods that allow interacting with database versions.

Document Methods
- `.save`

Model Methods
- `.find`

We create new "documents" using the prototypical object construction in JS:
```js
const note = new Note({...})
note
	.save()
	.then(...)
```

## Schema-less
MongoDB is NoSQL, and has no rigid structure for documents in collections - thus, MongoDB is *schema-less*, because it really does not care for the structure of our schemas that we defined in Mongoose. 

Why we use Mongoose, is that it helps us adhere to the principles of our system better, to cut down on room for bugs.
> Think about not using some schema/model API. Without knowing (or even looking at) the structure of existing objects, how do you know how properties are spelled or defined? 
> It just makes it easier to interface with MongoDB to achieve a consistent data model.

# Reminder: Hide Credentials
Do not store any account-specific credentials in any plaintext or application code without considering who can see your code.

If your code is hosted in a public repository, *anyone* can see the source code, and could find your sacred, secret API keys, database logins, etc ...

It's best practice to not include these credentials in the repo, even in private repos. What's much better and logical, is to use *environment variables* as a key holder encryption scenario. 

Your secret keys can be stored in server-side files and on files on machines that need to locally host the code.

# Advanced Error Handling
Within every routing middleware, we *could* have a way to deal with errors immediately as they are thrown in the promise chain. This makes it clear exactly where and when errors occur, but creates larger rout functions.

Instead, we can utilize the full power of middleware functions and create an *error handling* middleware:

```js

//routing
app.get('/api/:id', (req, res, next) => {
	somePromise()
	.then(...)
	.catch(err => {
		next(err)
	})

})

// ...

//last middleware in the stack
app.use((error, request, response, next) => {
  console.error(error.message)

  if (error.name === 'CastError') {
    return response.status(400).send({ error: 'malformatted id' })
  } 
  next(error)
})
```
> Express understands that this error-handling middleware is meant for errors because it has 4 parameters, and we pass the error as the first argument to the `next(err)` invocation.

# Mongoose Validation
We can use Mongoose schemas to create validation rules , so we don't have to *manually* validate and throw errors - on creation, mongoose will always check against the rules of the schema.
> Unfortunately, it's not automatic for the `.findByIdAndUpdate`, to check validation rules, so we have to tell it

```js
Note.findByIdAndUpdate(
    request.params.id, 
    { content, important },    { new: true, runValidators: true, context: 'query' }  ) 
```




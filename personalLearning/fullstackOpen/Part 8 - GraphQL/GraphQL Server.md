GraphQL is an alternative to RESTful APIs, as it dictates how we query our API for specific data.
RESTful APIs hinge on the fact that we are attempting to access *resources*, which should be structured in a way so that we may `GET`, `POST`, `PUT`, `DELETE` resources based on the API endpoints. The point is, APIs are RESTful because each endpoint should describe a specific resource, whether its a file or a SQL-based primary key, and what we do with it.

GraphQL is different in that any time we make a request, we are *building* the structure of what we want. It's not too far from the logic of SQL queries, in which we build a total query using subqueries and joins, and we can "select" fields - GraphQL defines a language to select fields at the same time as joining related fields.
___

# Motivation
Think about a strict RESTful API and how we would get information that is related to other information - without developing an endpoint that does so in the SQL. We would have to query the API multiple times with resource information from the previous queries. Otherwise, when using GraphQL, we can build the relationship between fields in the query itself.

> For example, show a list of *all blogs* added by *users* who have *commented* on ANY blog we follow. We would go backwards and get a list of all the blogs we follow, then find all users that commented on those blogs, then find all blogs that each user has created.
> Not necessarily a "complex" query, but an example of how much work it would take in a RESTful API requiring multiple endpoints and computation.

```bash
query FetchBlogsQuery {
  user(username: "mluukkai") {
    followedUsers {
      blogs {
        comments {
          user {
            blogs {
              title
            }
          }
        }
      }
    }
  }
}
```
1. For a user, specifically one with a username
2. Get all of that user's followed users
3. Get each of those user's followed blogs
4. Get all comments of each of those blogs
5. Get the users of each of those comments
6. Get all the blogs that relate to each user
7. Get the title of each user's blogs

It builds the relation between all objects, with any leaf nodes/fields being a data return.

# Schemas
GraphQL is made possible by the use of *schemas*, similar to those of [[Databases with MongoDB#Mongoose]], or just the idea of type-schemas in general.

Basically, we define *types* as interfaces, within each type, their fields and metadata.
- Names of fields
- Types of fields
- Their requirement

## [Data Types](https://graphql.org/learn/schema/#object-types-and-fields)
- Objects:
	- higher-level components that represent an *object*, which are combinations of scalars, enumerations, or other objects.
	- defined using the `type` keyword

```bash
type Starship {
	id: ID!
	name: String!
	length(unit: LengthUnit = METER): Float
}
```
- Fields within an object type can have 0+ arguments, which are defined and used specifically by their name (not by order!)
- The `Starship` object type has 3 fields, `id` whose type is ID, `name`, whose type is String, and `length`, which has an **argument** called `unit` which has its own type of LengthUnit, set to `METER` by default if not provided. The type of `length` is a float.

- Scalar: do not have sub-fields, are examples of *concrete* data.
	- Int
	- Float
	- String
	- Boolean
	- ID
		- a *unique* string, not necessarily human-readable
> - can specify "custom" scalars: `scalar Date`

- Enumerations: scalars that can only be one of a specified few enumerations
	- `enum Episode { NEWHOPE EMPIRE JEDI }`

- Lists and Non-nulls
	- If we want to describe a field as *required*, meaning that it must always be non-null, then we append the exclamation `!` to the end of it
	- If we want to describe a field as a List/Array of some type, we wrap the type of the field in `[]`.

```bash
type Character{
	name: String!
	appearsIn: [Episode!]!
}
```
> In this example, the field `name` is required. The field `appearsIn` is also required, but is defined as a *list* of Episodes, which are required as well?
> Since the *array is non-nullable*, that means the array must always exist with 0+ items, and means that every item MUST be an `Episode` object.

### Interfaces
Interfaces are abstract types that describe a set of fields that *must* be defined within other types.
```bash
interface Character{
	id: ID!
	name: String!
	friends: [Character]
}

type Human implements Character {
	id: ID!
	name: String!
	friends: [Character]
	starships: [Starship]
}
```
> Here, we define a `Character` interface that describes a character within a movie series. The `Human` type implements the `Character` interface, meaning that a `Human` type implementation must contain a superset of the interface's fields, so all of them, and perhaps more!

### Query and Mutation types
These are two special types that we must define as *entry* points into our schema relation. They act as the starting point to our objects, and defines the types of queries we can make to our API.
If it's still a little confusing, think back to "header" files from `C`, in which we define our function signatures and their returns:

```js
type Person {
  name: String!
  phone: String
  street: String!
  city: String!
  id: ID! 
}

type Query {
  personCount: Int!
  allPersons: [Person!]!
  findPerson(name: String!): Person
}
```
> the `Query` type defines our query start point, for which we have 3 "functions", and what they're supposed to return. It helps tell whoever is trying to query the API what kind of data to expect on the return of a query
> - the `personCount` query must return a non-null Int
> - the `allPersons` query must return a 0+ array of Persons
> - the `findPerson` query has an argument, a string called `name`, and this query will return a Person object, but it's not required that it have a value (in the case of there being no existing person)

So, fields of the query object describe the available queries the client can send to the server, and what kind of data we must, or can provide, and what to expect in return.

Also, despite the fact that it's a "query language", it's not actually tied to databases at all. It doesn't matter how the data is actually stored or what we use to query and mutate the data in the store. GraphQL actually describes the language of the client and server API requests.
> Under the hood, a GraphQL request can basically be a RESTful request with a singular method allowed: POST. The payload is the query.

# Apollo Server

```js
const server = new ApolloServer({
	typeDefs,
	resolvers
})
```

- `typeDefs` corresponds to a string literal that contains all the type definitions for our GraphQL schema, including Query and Mutation types.
- `resolvers` is a JS object that contains a Query property, which itself defines the *actual behaviour* of the defined type Query in the `typeDefs`.  These behaviours are defined as *functions*, that run when a GraphQL request queries them

## Resolvers and Parameters
When defining resolves, it's common to see at least TWO parameters:
- `(root, args) => ...`

Technically, resolves can receive 4 parameters, but it's most common to see the `root` and `args`. This is because the *root* parameter describes the root object, and the *args* parameter describes any incoming arguments to the query.

Resolvers can be defined for *each* field of ALL types - but if none is defined, then Apollo creates default resolvers for them. This indicates to us that all resolvers do is define how to access a specific field on an object.

## Nested Objects
Given a GraphQL schema that contains objects as types within other objects, the way we query and mutate these objects must follow the direction of the schema - meaning that if an object is nested within another (take for example the `address` object within `person` object).

However, this doesn't mean that the data itself must be stored in the same way - that's what resolvers are for. Resolvers define how we can structure the stored object in the way of the schema.

## Mutations
Similar to how the `Query` type describes the "GET" queries of our schema, the `Mutation` type describes the schema of any mutation-bound queries.
Continuing with this resolver pattern, we define the behaviour of mutations through resolvers.

## Error Handling
GraphQL can handle runtime errors through its *validation* and pass back appropriate error messages. The beauty of GraphQL lies partially in how detailed the error messages can be. 
We can create "custom" errors through the `GraphQLError` object.

## Multiple (Combined) Queries
GraphQL provides ease-of-use by automatically parsing multiple queries. We can even invoke the same query more than once in the same query request, with different parameters. In that case, we must assign a unique name to those queries.
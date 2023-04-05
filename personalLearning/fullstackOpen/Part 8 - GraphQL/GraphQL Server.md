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



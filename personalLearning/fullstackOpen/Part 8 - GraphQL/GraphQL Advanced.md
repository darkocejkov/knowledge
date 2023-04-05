# Fragments
- Allows us to define sets of fields, essentially shorthands for queries
- Defined in the **client**, not the **schema**.

```js
export const PERSON_DETAILS = gql`
fragment PersonDetails on Person {
    name
    phone 
    address {
      street 
      city
    }
  }
`

export const FIND_PERSON = gql`
  query findPersonByName($nameToSearch: String!) {
    findPerson(name: $nameToSearch) {
      ...PersonDetails
    }
  }
  ${PERSON_DETAILS}
`
```

# Subscriptions
- subverts the type of communication of HTTP requests as responses, as instead of having to *ask* or request for data, a two-way communication pipeline can be used to listen (publisher-subscriber) for updates
- the *secret* third type of operations alongside queries and mutations
	- clients *subscribe* to updates in the server
- Apollo uses `WebSockets` for server -> browser communication
- Not supported in Apollo <= v3
- Requires starting the server using *Express* instead of a `startStandaloneServer`.
	- We still use `new ApolloServer`, but use the `expressMiddleWare(server, {options})` function from Apollo to turn the server and schema into middleware.
- The whole point of this new type
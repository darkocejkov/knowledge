GraphQL is defined on the server, but how do we use it in the frontend? It's an entire different approach to a RESTful API interface, so we're going to have to dive deeper.
___

As previously mentioned, we *can* facilitate communication between Apollo through a HTTP POST requests to the `/graphql` endpoint. However, it might be more suitable to use a client package for our client frontend because it fits better with the schema.

2 Options:
- Relay (Facebook)
- Apollo Client

# Apollo Client
- `@apollo/client`
- Allows us to instantiate an `ApolloClient` object with server endpoint and client configuration details, like a cache object
```js
const client = new ApolloClient({uri, cache: new InMemoryCache()})
```
- We use this `client` object's methods like `.query` to query the Apollo  API in the backend.
- Instead of drilling client, we can use the `ApolloProvider` context component to pass down the client
	- which allows us to use the `useQuery` hook.

```js
const ALL_PERSONS = gql`
query {
  allPersons {
    name
    phone
    id
  }
}
`

const App = () => {
  const result = useQuery(ALL_PERSONS)

  if (result.loading) {
    return <div>loading...</div>
  }

  return (
    <div>
      {result.data.allPersons.map(p => p.name).join(', ')}
    </div>
  )
}
```
> The query is a template literal containing the query

- The flow of data is similar to using `react-query` because it utilizes a hook, we declare the various functional *states* and the output, and the hook handles requests, caching, and re-renders 

## Query Variables
- Allows us to replace query arguments with variables, so we can programatically make requests
- When we define our query, we need to replace any hardcoded argments with variables:
```js
query findPersonByName($nameToSearch: String!) {
  findPerson(name: $nameToSearch) {
    name
    phone 
    address {
      street
      city
    }
  }
}
```
> These variables are built-in to GraphQL itself, not Apollo Client

When we would like to request a query, Apollo Client allows us to pass a `variables` option to declare variables *by name*:
```js
	const result = useQuery(FIND_PERSON, {    
		variables: { nameToSearch },    
		skip: !nameToSearch,
	})
```
> The query is executed only when the state `nameToSearch` has a value, if not, it *skips* the query.

## Cached Queries
- Apollo Client is able to *cache* queries and their results in-memory
	- so if a query is repeated with the same arguments, etc ... then the request is not made to the server, but rather uses data from the *cache*.
- The problem is: *when should we refresh the data in the cache using server response data?*
- we can provide the `pollInterval` (in milliseconds) as an option to a query which will automatically re-query (without the cache)
	- however, this generates more network load, with the most likely chance that the data will not change

## Mutations
- We need to use the `useMutation` hook
	- We provide it the mutation type, preferably with variables in-place

```js
const CREATE_PERSON = gql`
	mutation createPerson($name: String!, ...){
		addPerson(
			name: $name,
			street: $street,
		){
			name
			id
			address {
				street
			}
		}
	}
`

const [createPerson, result] = useMutation(CREATE_PERSON, {
	refetchQueries: [{query: ALL_PERSONS}],
	onError: (err) => {
		// handle error from server
	}
})
//...

createPerson({
	variables: {
		name, phone, street, city //states
	}
})
```
- can provide `refetchQueries` option a list of objects, each specifying a query to re-fetch on mutation
- `onError` is an additional property option on the `useMutation` hook that allows us to "catch"  errors in the promise
- on the other hand, if there's an 'error' in our application that does not have an exception tied to it, but our UI needs to respond, then we can use the `result` element of the `useMutation` hook.
	- imagine that we are mutating a person's phone based on their name look-up (assuming names are *unique*). If we try and update a person with a name that does not exist on any person object, then the data sent back is `null`, and no exception is thrown. we need to handle this case in the UI, and the `result` return of the hook allows us to check the value of the returned result.
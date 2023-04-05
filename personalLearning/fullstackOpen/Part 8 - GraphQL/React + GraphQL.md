GraphQL is defined on the server, but how do we use it in the frontend? It's an entire different approach to a RESTful API interface, so we're going to have to dive deeper.
___

As previously mentioned, we *can* facilitate communication between Apollo through a HTTP POST requests to the `/graphql` endpoint. However, it might be more suitable to use a client package for our client frontend because it fits better with the schema.

2 Options:
- Relay (Facebook)
- Apollo Client

# Apollo Client

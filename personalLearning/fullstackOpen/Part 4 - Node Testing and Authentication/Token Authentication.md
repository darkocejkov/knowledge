Authenticating and "logging in" is good authentication, but there's something else we can implement to further authenticate every *request*, which are *tokens*. This is similar to the idea of API tokens that we get from public APIs, which we need to pass to the endpoints to show them that we are indeed, authorized to make requests, and can uniquely identify the user account associated with the request.
___
Of course, there are many, many different ways to enforce authentication. We could use `passport` to "serialize" into a cookie, which is similar to token authentication, as the cookie is passed back and forth and we can "deserialize" the user from their cookie through lookup.

# JSON Web Tokens
A handy and useful package for generating *signed* tokens based on content.

## Signed Tokens
Remember in [[User Administration#Hashing and Security]], I mentioned that a possible form of encryption is that we have some *reversible* transformation on content? Signed tokens are just that, but don't worry, they *are* secure, as much as I hinted that they are NOT.
Signed tokens are a different form of encryption security, and are inherently *less secure* than hashing, because we *need* to be able to reverse the transformation to see the content. 
Signed tokens are exactly like coming up with a secret language with some way to decipher what's being said, with the exception that you keep the deciphering rules secret themselves. That way, if anyone *hears* what's being said, they cannot *know*, unless they ALSO have access to the rules.
> Again, that doesn't mean it's *uncrackable*. In terms of security, your encryption or security is only as secure as the weakest vulnerability. 

```js
const userForToken = {
  username: user.username,
  id: user._id,
}

const token = jwt.sign(userForToken, process.env.SECRET)
```
In this case, we "serialize" the user's username and ID into the token, and "sign" it with a secret key.


## Why Signed Tokens?
It's a really secure way to pass information between parties, such as the client and server, without much overhead. 
Secondly, it adds a level of authorization serialization to requests, if we encode various levels of information into the token - like expiry date of token, user, access level, etc ... we don't have to repeatedly pass that information back and forth - and we might not *want* to pass that information un-encrypted!

## Sending Tokens In Requests
A common way to send authorization tokens in requests is to use the standard `Authorization` HEADER of requests, which has various [authentication schemes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication#authentication_schemes) (Basic, Bearer, Digest, HOBA).
The one that fits to our case most is `Bearer`, as it's a signed token using a secret.

This way, when we get HTTP requests, we can create parsing functions to parse the tokens from the header - and can support different schemes of auth.

```js
const decodedToken = jwt.verify(getTokenFrom(request), process.env.SECRET)
```

With signed tokens, we can safely pass data back-and-forth between the client and server that we need for various things. Since we are using a document-model database, there are cases in which we need to pass extra data between requests so we can make the referential objectID process easier. 

We are essentially implementing an OAuth authentication interface.

## OAuth2.0 as Tokens
OAuth2.0 is a programmatic access protocol. It's a process that offers us a unique access ID and a secret key. Anytime we want to communicate with an OAuth2.0 API, the implementation between APIs may be slightly different. It could be enough to just pass the ID and Secret on requests, which the API can authenticate and authorize our requests on.
Other times, we might be passed back a token in the same way we are passing `JWT` tokens back, to encode data in requests and authorize them at the same time.

## Flaws of simple token access
Thinking about it, there are some pretty big flaws in the way that we authenticate Users from their access token. 
1. Firstly, it never "expires" - if a User finds and saves their token, it will always work, so they don't need a new token.
2. Access cannot be "revoked", beWcause if a token is present in the headers, which is a valid token, then they can make any request
3. We are not limiting requests from the same token. The same token can make infinitely many requests, back-to-back.

We can add some more security to tokens by adding a timestamp to when they were created, or when they expire.
> If we use the "created" timestamp, then it's up to the server to find out the difference in time between a token'd request and how long it's been, and have some way to determine if it's expired. Otherwise, with a "expires on " timestamp, we simply have to check if the time of the requests is >= expiry time.

### What happens if a token expires?
Force user to re-log, resetting their frontend states and pushing them to the login page, which re-acquires a token on login

## Server-side Sessions
Are another way to check for access and authorization. They are more complex than a simple token-bearer because they rely on lookups to the user's session, often times the "token" does not need to encode data like `jwt` does, because there's no need to encode data when we are creating references between a user's session and their token.
Redis is a powerful key-value pair database that can easily store session information (because it's a single key-value pairing), which has a very high performance (because it only deals with key-value pairs, making lookups $O(1)$).

### Previous Experience
Previously, something I've implemented is the use of *passport* as a middleware function that can be really easily integrated with a Redis store. Passport will handle the authentication of the user using "strategies", and when a succesful login happens, it "serializes" the user into a cookie-token, passed in the request. When *any* request is made, the cookie allows the backend to "deserialize" the user from Redis, thus finding the user's information super fast, and if they are authorized and still have access to query.


Adding Users as an object can lead to many different functions and features. 
Using the user object, we can add authentication to the mix, we can add the functionality of relating objects to users.
___

## Relational vs. Document based users
In a relational database, the idea of relating Notes to Users is super simple. Each user has its own record with an ID. Anytime that user creates a "note", we use their user ID as a *foreign key* in the note record.

Document-based databases are very fluid, and the way you set up the "ownership" or "relation" between these objects depends a lot on the theoretical relationship.

There's no way to "join" documents as you would tables to find a common relation. 
-> MongoDB (^3.2) supports *lookup aggregation queries*, but is not used in this course.

Instead, to "look up" relationships between data in documents, we take the explicit approach and create our own lookups using multiple queries.

# Structuring the Database
As previously mentioned, the way we create our documents is based on our data model - which can often times can have many different structures.

Given that each "object" of a specific type is stored in its own "collection", how do we create that relationship that could be one of the following:
1. one-to-one
2. one-to-many
3. many-to-many

For a more concrete example, if we have a collection of Users that can be assigned a unique username and unique ID, how can we relate any Note objects that those Users create?
> Of course, given that a Note itself has an object ID, and a User ID.

Document databases do not have a strict policy against redundancy, so we *could* also directly store an array of Note IDs in the User object:
```js
{
	username: 'darko',
	_id: 0,
	notes: [0, 1, 2]
}
```

OR, we could possibly store the entirety of the Note object itself instead of the IDs.

It's not as obvious how we cross-reference other Mongoose Schemas within schema definitions - here, we  create the semantic link between a User and the Note schemas like so:
```js
const userSchema = new mongoose.Schema({
  username: String,
  name: String,
  passwordHash: String,
  notes: [
    {
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Note'
    }
  ],
})
```
> In which the `Schema.Types.ObjectId` is a generic type supplied by Mongoose to reference object IDs, but the `ref` portion denotes the object IDs are specific to the `Note` schema's IDs.

Again, these Schemas are entirely in the lens of Mongoose, and *not* MongoDB. MongoDB honestly couldn't give a f\*ck about the way we define schemas. These references to types and other schemas are purely for development consistency, because our documents should follow the schemas.

## Schema Methods and Transformations
I briefly noted down that schemas may have methods, similar to classes. We can create custom methods to invoke on documents, or, can use built-in methods.

```js
userSchema.set('toJSON', {
  transform: (document, returnedObject) => {
    returnedObject.id = returnedObject._id.toString()
    delete returnedObject._id
    delete returnedObject.__v
    // the passwordHash should not be revealed
    delete returnedObject.passwordHash
  }
})
```
> This is an example in which we set the `toJSON` method to transform the document we invoke `.toJSON` on in a certain way. Instead of just passing the *whole* document, there are some things that we *don't* need, or even *shouldn't* pass back.
> - The hash of the password does not need (*shouldn't*) be held in the object, the version (`__v`), or the object ID as an object - instead, we create a *new* property `.id` that relates to the object ID as a string.

# User Authentication & Encryption
Users with the ability to authenticate need *at least* 2 things, a unique identifier, and a secret password.

This allows users to have unique names, emails, ..., whatever, just as long as we can know that a single unique (named) identifier does not reference more than 1 user document/object, then we're fine.

Also, this allows users to have secret access to their own account through a secret password only they should know. Of course, this is only as secret as they want it to be.

It's really stupid to store these secret passwords in the database without any form of encryption, in plaintext for example ^[[Even Facebook](https://techcrunch.com/2019/03/21/facebook-plaintext-passwords/)]. Without going into too much detail, the obvious reason(s) is that if your database is itself vulnerable, then your all user accounts are then compromised if the database is leaked. Also, if don't take care to create a strong integrity between the data that can be passed back from the server, packet sniffers and other various methods can be used to find random passwords of people who are using the service.

An industry standard is to use *hashing* to store passwords. 

## Hashing and Security
There's a whole discipline and many different courses that explain the differences between hashing and encryption, secrets, salting, and so on. 
Instead, the easiest way to explain hashing is that it's a **one-way transformation**. 
Instead of storing passwords using some transformation that is *meant* to be reversed, we store passwords in guaranteed, unique transformations.

Take for example, the transformation to reverse the password string. If you enter "havefun" as your password, your "encrypted" password is stored as "nufevah". If you want to validate against this password, all you need to do is re-reverse the stored password and compare: `"havefun" === "nufevah".reverse()`, or vice versa.

The problem is that no matter how difficult, how intense that transformation is, the weak part is that it is reversible. All you have to do reverse the transformation is to do all the steps in reverse, which is something that can be cracked and figured out, making all stored passwords vulnerable. Even if all passwords use different reversible functions depending on randomness, the point still stands even though it would take a lot of work.

However, hashing is a transformation that depends on the content itself, and applies a hashing function such that no two unique hashed passwords are the same, unless they are hashed on the same content. 
This way, if your database gets leaked, the fact that the passwords are hashed means that they are un-reversible, and cannot be known. The only way to *know* what the contents of the *unhashed* password are, is to compare every possible password hash to every unhashed password - which is impossible. 
> Basically, if you hash `havefun`, the only way to know that the hashed version (not the real hash:) `Ajh!21u*Ahh1JAhjhdA*71` means "havefun", is to hash "havefun" and compare the hashes.
> I think there's a lot more to it, considering hashing functions have "rounds" and "salts" that they use to change how intense the hashing function is, to the detriment of the computational engine, but that's out of scope of the concept.

## NodeJS Hashing
Thankfully, we don't have to learn, implement and hope that our custom hash function works well - because people have already created it (the beauty of package managers).
`bcrypt` is a tried and true package to help hash passwords easily.

## User Creation
- end-users fill out a form to indicate their desired username and password
- create hash using `bcrypt`, discard entered password and save only the (unique) username, and the password hash.

# Testing!
The beauty and grace of testing is that we know the constraints of the models and routes we build. For users, they should have a unique name, they should have a password that's secure, they should have entered all the details of the form, etc.

Instead of manually validating this using frontend API, or even Postman, what are you going to do when your application grows much larger and you have logic intensely more complex, manually validate that these things still work?

Again, from [[Backend Structure & Testing#Personal Experience]], creating complex systems without *any* automated testing is actually the recipe to disaster. It means that the testing relies on the manual aspect of people, and even though it takes more work to write and validate tests, humans err and even the most rigorous, in-depth manual testing process is bound to miss the small things.

Also, it's really fucking boring doing manual testing. Some test cases require a LOTTTTT of setup. It's infinitely easier to create automated tests that have easy setup. Otherwise, if you need to  test the response to a new User with an existing unique username, you have to already have a User in there!

# Test-Driven Development (TDD)
Is a practice to developing where we plan functionality around the tests. The principle depends on the "blackbox" aspect of testing, in which we have a feature, like user authentication, and some constraint to impose on it, like no two users can share the same *username*. The testing is independent of the implementation of the User object, other than the name of the fields itself, and what we expect it should return. 

# Mongoose Uniqueness Validation
In order to enforce that fields are unique in a schema, a collection of documents that follows a Mongoose schema, we need to install the `mongoose-unique-validator` package. 
It allows us to insert the `unique: true` property on Schemas.

# Mongoose Populate
Since we are using non-relational database, we cannot create joins of documents in the same way that SQL can.

> A beautiful thing about SQL is that all queries are *transactional*, meaning that during the execution of queries, there is a guarantee that the state of the data will not change during the query itself, from some external query or change.

Since MongoDB is not transactional like SQL is, the state of the data *may* change between queries - especially because in order to create "joins" or related lookups, we need to do multiple queries.

Document databases cannot implement joins between collections in the way that relational DBs can. However, Mongoose has an abstraction of joins through the `populate` method.

Here's an example:
```js
await User.find({}).populate('notes')
```
We use the `.populate` method *after* a find operation (which returns a list of Users, and in this case - all users). The populate method is passed the name of a property expected to be in the schema of Users.
-> the property `notes` is an array of items, which we've told Mongoose in the Schema of User, that the array references IDs of Note documents, which Mongoose will then "populate" the array of notes for all instances of found Users.
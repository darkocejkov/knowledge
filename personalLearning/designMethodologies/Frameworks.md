## So common, yet elusive
> Frameworks are becoming all the more common, especially in terms of developing software. 

# What are they?
Frameworks are *abstractions* of other things, meaning that they build on TOP of it. 

Think of the analogy of **building a house**, in which there are many ways you can start to approach it, but the main concern is whther or not we start at a high, or low leve.
1. **Low Level**
	1. Secure a plot of land
	2. Design the entirety of each floor to its nearest 1/4 inch
		1. where are the windows, where are the walls
		2. making sure to accomodate for add-ins like electrical applicances/wires, plumbing, heat, insulation, vents, etc.
		3. ...
	1. Get the necessary tools and vehicles to dig holes, place nails, screws, etc
	2. Start digging, preparing the foundation
	3. ...
2. **High Level**
	1. Design house
	2. Start building floor 1
	3. Start building floor 2

> 	We abstract the process of building the house into discrete *groupings* of tasks. Certain tasks become implicit in the process. The job of frameworks is to abstract tasks that make it difficult to achieve high levels of design and speed because it's not necessary to create that repetition.

For example, it's implicit that in order to build a house, we need to have a plot of land. Even that is an abstraction, because what do we do if there is already something there? We would first then have to demolish the existing building. That's an implicit task that does not necessarily need to be defined in the framework.

In terms of developing software and writing code, frameworks allow you to get large amounts of progress with much less work, because frameworks handle a lot of the overhead that exists for complex tasks.

Examples:
- Building a RESTful API on Node is quite difficult, because where do you start? You have to (by-hand) write all the code to define the various server handling processes, how network requests are handled, sending back data and information.
	- Thankfully, **Express** is a *framework* that you can include in NodeJS which automatically deals with all that complexity, and allows the user to write custom code to define endpoints, and what happens when those endpoints are requested, and the user touches very little server-code.

| Framework | Builds On  | Purpose          |
| --------- | ---------- | ---------------- |
| Django    | Python     | Front-end Web UI |
| Rails     | Ruby       | Back-end server  |
| Express   | NodeJS     | Back-end API     |
| React     | JavaScript | Front-end Web UI |
| Angular   | JavaScript | Front-end Web UI |
| Flask     | Python     | Back-end Server  | 

## Pros:
- Frameworks make it really easy to start building functional and scalable projects
- Frameworks are much easier to understand and learn than the code it builds on

## Drawbacks:
- Since frameworks build on TOP of some language, the customization is limited to the API of the framework.
- When using frameworks, there is a limit to how much you can *optimize* code, because frameworks may not be optimized themselves (black-box design).



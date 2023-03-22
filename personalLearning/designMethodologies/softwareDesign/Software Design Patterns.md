> [design patterns](https://refactoring.guru/design-patterns)
___

# Design Patterns?
Solution patterns to problems in designing software, like "blueprints" that define a strategy or "algorithm", whose structure is loose and is agnostic to any languages or frameworks. 

Patterns are similar to, but ultimately more general than *algorithms*. Algorithms are concise (imperative) actions to achieve a goal, while patterns are higher-level. Patterns can apply to algorithms, while algorithms do not apply to patterns.

Patterns are formalized in the following format:
1. Intent
	1. Problem and Solution
2. Motivation
3. Structure
4. Code Example

# Classification
-> Low-level patterns are called *idioms* and usually depend on a language
-> High-level pattners are *architectural* because they describe an abstraction, and can be applied to any language or system.

Patterns are classified by their intents usually, with 3 broad categories:

# Patterns: Creational
> object creation mechanisms to increase flexibility and reuse
## Factory Method
Interface for creating objects in superclass, whose *subclasses* offer ways to alter objects that are created
The problem is that if you build your app in a way that depends on specific classes, rather than broad ones, you then box yourself off from easily adding new types of input. 
Classes should be structured such that any core input should extend some interface that groups commonalities between input, what is *really* important about inputs. So, any usage of those inputs are "blackboxed" to the methods that use them.3

## Builder
Builders are design patterns that are meant to get rid of the following:
1. Long parameter lists
2. Too many subclasses
Instead of creating some constructor that takes so many different parameters, we shift the perspective into creating builder *methods*, which we can use to "build on" objects.

The example here is that we have a base class like a House, and instead of running `House(2, 2, 2, false, true, null, null, null, true, 4, 5, null, false, true)`, we can run various builder methods to add onto a `House` object.

The builder pattern can be extended by adding a *Director* class, which essentially orchestrates order in the steps of building.

## Prototype
A way to create "copies" of existing objects without making code dependent on the classes themselves. The first idea about creating clones might be do deal with all the overhead and create some way to copy all values all values of the original object, one-by-way, onto a new object. 
That plan starts to fall apart when there's limitations on how we can access certain fields - if we create a cloner class and it can't see *ALL* the fields / methods, we cannot possibly clone all those fields. Not only that, but the cloner now depends on the class itself and not for any other classes.

The key factor is to implement a superclass that parents all child classes. The superclass only needs a clone method, which each class implements themselves. This shifts the responsbility of cloning to the subclasses, because they can access private fields, and don't link other classes to that one.

## Singleton
A class that has only *one* instance, with the ability to be a "global access point" to that instance. This is typically something built out of a constraint that there must *only* be ONE instance, for a shared resource. Instead of creating multiple instances that link a shared resource and make it impossible to sync between those instances, just have 1.

The biggest problem with this pattern is just constructors are *meant* to create `new` instances, and that any global references to that single instance are possibility volatile. The solutions are to control creation as a method of the class itself, and implementing logic that serves as both a `new` creator (if no instance exists), otherwise returning some reference to the instance.

# Patterns: Structural
	Assemble objects into larger structures

## Adapter
Objects with *incompatible* interfaces *should* be able to interaction. We create adapter interfaces to wrap objects to expose the type of data we want. For example, if we have some object that contains address information, but we need information in a more absolute way for some extension, then we can create an adapter class that takes relative positions (like addresses) and turns them into absolute positions such as lat/long.

## Bridge
Splits large classes, or sets of related classes into two seperate hierarchies, the idea of *abstraction* and *implementation* that are developed independently.
Instead of developing the hierarchy of a class in more than 1 dimension, that is - subclasses are variants of more than 1 dimension (shape AND color = redCircle, redSquare, blueCircle, blueSquare, etc.), we can use the *bridge* pattern to compose rather than inherit these traits.

Bridges seperate a large concept into an **abstraction** layer, and an **implementation** layer. Similar to model-view-controller principles, we develop an abstraction layer to seperate complex under-the-hood operations. The easiest real example is the idea of a GUI as the abstraction, versus the underlying API of classes, functions, and members that implements what the GUI represents.

Without the pattern of bridges, you are creating a monolothic structure that is vulnerable to changes, because there is no abstraction vs. implementation to focus changes onto, but any changes can affect both in the monolothic.

In essence, this pattern promots the idea of creating your own framework, because you create a bridge/abstraction. 

## Composite
Composing objects into trees with the ability to treat each node as an individual object. This pattern owes itself to *recursion*, because the point is that we have some nested objects, and instead of creating a complex way to traverse the tree externally, we can use recursion to our advantage and traverse the tree with very simple subproblems. 

	Why create an algorithm that examines all levels of the tree at once, when a much easier subproblem is to accomplish a simple task, then pass it down?

## Decorator
Decorators are extremely useful, because they attach behaviours to objects by wrapping them in other objects. I guess it's similar to adapters, but instead of requiring this wrapping to interact with other objects, we wrap objects to pass down behaviour, like the ability to give a `Dog` class, the ability to `meow()`.
-> This bypasses several constraints of inheritence, as inheritence is a static (class-based) approach, in which we can't really change at run-time the inheritence of an object, and subclasses can't inherit from more than ONE parent. 
A `shepard`, child to `dog` can't also be a child `cat`. 

Instead of inheritence, we can use *aggregation* or *composition* of objects to create **references** to other objects to delegate work.

### Aggregation
A contains B, but B can live *without* A.
### Composition
A consists of B, where A manages the lifecycle of B, and B *cannot live without* A.

These class wrappers are implemented such that the wrapper class links a target object and delegates work, but also can "inject" behaviour.

![[Pasted image 20230321122900.png]]
> Here, the BaseDecorator is the wrapper, while specific decorators are subclasses to it. The BaseDecorator itself is a subclass to the class we want to decorate.

## Facade
A simple interface for some library, framework, or set of classes.
In a real example, it's identical to the front-facing interfaces when dealing with things that are truly complex. Online order for one, is a facade for a huge logistical solution. All you do is use the interface to find items, add them to a cart, press checkout, fill in your information, then confirm.
-> This is the 'facade' as your job stops there, and the responsbility shifts to the application(s) to then use encrypted billing, find the closest instance of the product(s) you ordered, figure out the most cost-efficient way to get it to the customer.

## Flyweight
An optimization strategy to seperate *constant* qualities of objects and *dynamic* qualities. Instead of wasting resources on instrinsic (constant) state of an object, 

## Proxy

# Refactoring & Quality of Code
> [Techniques & Patterns](https://refactoring.guru/refactoring/techniques)

While patterns exist and we can harness their architectural patterns to create nice code, that's not exactly enough. 

Even code that utilizes patterns can be bad, because they lean too much on other things and forfeit proper organization.

When code is dirty, or not well maintained - refactoring is the process of re-working the codebase to follow a consistent ruleset.

**Clean** code ideals:
1. Obvious to others
	- Means that it's simple and concise, variable names, connections, etc.
2. Minimal classes
	- Less is more = less maintenance, less bugs
3. Tested
	- Dirty code means 95% coverage, while awful code has 0% coverage.

**Technical Debt** is synonymous to *real* debt, in which we attempt to "speed up" the process by foregoing the process of additional work, which starts to rack up the amount of future work.
This happens when you avoid using testing suites, when you don't bother organizing or designing from the start.
1. Business pressure of "crunch" and trying to cut corners
2. Lack of understanding, no "value" is seen in re-factoring
3. Codebase is more of a "monolith" rather than an organized network of components, which makes it too difficult to split up work without affecting others
4. Lack of testing makes integration much more difficult, as well as the  possibility to introduce BIG breaks
5. Lack of documentation makes it difficult to onboard new people, and remove the time it takes to "re-learn" solutions
6. Lack of style/content compliance, when individual developers don't take the time to keep code compliant to the style of the project
7. Siloed development between branches, which hugely increases technical debt because avoiding creating merge conflicts will create many, many more in the future

## When should you refactor?
	1. When you've done something the same way THREE (3) times, without having an elegant way to continue it further.
	2. When you add a *new* feature
	3. When fixing a bug

## What's a good way to start refactoring?

> The main principle of refactoring is to use hindsight about what *could* be better in combination with planning and design. 

*refactoring* checklist:
1. code *should* be cleaner
2. should only refactor related functionality
3. should not introduce new features, but rather make it easier to develop and manage old ones.
4. existing tests must still apply

# Code Smells 🤢

## Bloaters
> Methods + Classes that have grown too large to work with, accumulated over time.

### Long Method
Methods or functions that grow too large because nothing is abstracted or taken out. "Why create a new method for 2 - 3 lines?".
-> Any code that needs to be explained is a candidate.

### Large Class
Classes that "do too many things". Logically, classes are abstractions of some logical collection of functions and members. A class is too large when it starts to perform other things than the original intent.
-> The most obvious way to deal with this is to seperate the class into other classes, or implement some inheritence hierarchy.

### Primitive Obsession
Creating (one too many) primitives as ways to hold information instead of doing the smart thing, and using objects/structures.
Instead of creating a type or implying structure to the data primitives, you create a scattered network that becomes quite difficult to maintain.

### Long Parameter List
Methods with more than 3 - 4 parameters. Typically happens when too many things are happening within a single method.

### Data Clumps
Copypasta programming that leads to "clumps" of repeated code. This code should be centralized into its own structure to be easily as a dependency rather than a novel implementation

## Object-Orientation Abusers
> Bad / Incorrect usage of OOP principles

### Switch Statements & Strings of Conditionals
A confusing, perplexing sequence of switch statements that works like a sh\*tty multiplexer. Anytime a new condition is added, you need to then find and add to that conditional logic.

### Temporary Field
Fields or objects that are created to temporarily hold values. Typical implementations of temporary objects are not optimal since they are usually empty, and introduced for that purpose only.

### Refused Bequest
Subclasses which only use *some* methods / members from their parents, so the hierarchy between these classes is not strong.
It's typically caused when there's some connection between classes, and there is some reason to have a hierarchy between them, but their lack of connection makes most of the shared / inherited properties useless because they don't share a real connection.

### Alternative Classes with Different Interfaces
Classes that perform the same function, but have different method / member names. Typically when someone doesn't know the other existed.

## Change Preventers
> they *prevent* change because wanting to make change limits how much change you can make easily, or how many other things you need to change

### Divergent Change
Any changes to a class requiring changes a lot of the other (unrelated0 methods). If you wanted to add a new type of some object, you would then need to change the existing CRUD methods for example. That's an example of bad implementation, because implementation should be agnostic to specific values like that and should abstract.
> Applies to changes *within* a single class.

### Shotgun Surgery
Similar to [[#Divergent Change]], but applies to changes in multiple classes (even worse).

### Parallel Inheritance Hierarchies
Are when a hierarchy of classes have overlap in what they are used for, and become very similar in terms of their hierarchy. Anytime you want to add to one of the hierarchies, you must add to the other.

## Dispensables
> pointless, unneccessary additions

### Comments
Comments are useful for explaining or giving insight for others. Good code doesn't need much explaining, especially if it's obvious. Comments are useful for learning, but in a huge codebase, it might be better suited to write referencing documentation elsewhere rather than the code itself.

### Duplicate Code
It's really, really easy to just copypasta the f\*ck out of certain repeatable segments of code, especially if it saves time. Unfortunately, if no time is given to refactor, it starts to pile up and have a really bad smell.

### Lazy Class
Classes that aren't used often OR aren't special enough for constant maintenance should be refactored to fit into other classes (too much and we risk [[#Large Class]]). 

### Data Class
Classes that are meant *only* for holding, and primitive operations on data (getters / setters). They do not perform any meaningful operations themselves.

### Dead Code
Unused, deprecated, or obsolete code. Just fills up space in the repository and serves for no purpose.
> Typically variables, parameters, fields, methods, or classes

### Speculative Generality
Unused class, methods, fields, or parameters - distinct to [[#Dead Code]] because the code is meant for *future* use, to just boilerplate/template architecture.

## Couplers
> Excessive coupling between classes

### Feature Envy
Methods access data of *other* objects more than its own. Typical in code using [[#Data Class]].

### Inappropriate Intimacy
Classes use internal fields/methods of another class. Classes are meant to be siloed, only exposing certain things to each other (like black boxes). It would then be more logical to seperate methods to the classes that use them the most.

### Message Chains
A constant requirement to use multiple different objects in some sequence. A "waterfall" of resources are needed.

### Middle Man
When classes exist to "delegate" work to other classes. 
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
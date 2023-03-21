[Source](https://www.educative.io/blog/object-oriented-programming)
___

# ?
OOP is a *paradigm* that changes how we structure discrete components of programming. It changes the way we create and hold data in programs and assigns order to the components, to promote good practices in designing complex systems.

OOP is exactly that, we use **OBJECTS** as structures, with their corresponding **CLASSES** that make up their "blueprint". Think of a system of multiple modules that interact with each other, sharing,  accessing, and manipulating data. Without OOP, you're reduced to *procedural* programming only, and any similar groupings of functions live only in a file, and not a class.

> Essentially, OOP is a way to organize functions and variables into classes. Moreso than just grouping similar functions into distinct files.

# Classes
Classes are abstract blueprints that describe how functions and variables exist. They are "instantiated" as **objects**. 
Classes exist as broad groupings of the systems that exist in the problem set that we are programming to solve, but in terms of learning purposes, are usually done with *hierarchies* of objects and their relation.

Think of `Animal` > `Dog` > `Laborador` > `Yellow`. That's a hierarchy, which starts at some arbitrary root, like the concept of animals, and has children. A dog is an animal, so are cats, so are pigs, etc. The hierarchy is built entirely based on the problem that we are solving. Thus, if it mattered to us, our grouping might not be "ALL ANIMALS", but rather domesticated animals, or farm animals, etc.

The point being is that we establish a hierarchy, a relationship between all the classes. Each class should share attributes. Between **all** animals, there should be some distinct way to qualify or quantify an attribute. 
-> For example, animals can either have fur, or no fur. OR, they can have feathers, or not. All animals have a lifespan, all animals have some classification of vertebrate vs. invertebrate, etc ...

Classes additionally contain **methods**, which are some arbitrary action that can be performed on/by them.
Cars, you *drive* them, you *fix* them, you *crash* them. Those can all be methods, provided that they perform some actions on the attributes.

So, to recap, classes contain #attributes (also called #members) quantify or qualify some quality about them that are shared between all other classes of that type. Classes also implement #methods or #functions, which are groups of actions that can be taken on objects of that type, typically operating on the #members.
1. Classes live in a *hierarchy*, which means that they have an innate *parent-child* relationship. 
2. Classes are *instantiated* as objects. Think of the difference between a *concept* which are classes, while objects are examples of those classes.
	1. Thus, we have the concept of "cars" or "vehicles" in general, but there are then differences between "my car" and "your car", which are *instances* of cars. Both come from the same class, but are different in terms of their attributes.

# Why?
Why use OOP when other paradigms can get the job done as well?
OOP is special in development because it's meant for better design and organization. In turn, this organization will lead to more meaningful interaction and development between classes, because there is a semantic quality to the problems we solve.

OOP itself implements **encapsulation**, which is a way to "blackbox" functionality to classes. Classes handle their own data and function, but can "share" what it wants to. It makes it much easier and digestable  to create a foundation, then build on that foundation by piecing together objects.

Overall, it promotes a way to group together logic that *should be* together into classes, and create objects that deal with their own data. It makes programming much more logical because we operate on semantic objects rather than non-semantic variables and structures.

# Pillars of OOP
These are inherent features that OOP provides, because of the structure of classes. 

## Inheritance
Classes may *inherit* features of other classes. Child classes may inherit parent class features through extension. This is a way that OOP promotes re-usability because it creates that specificity between objects.
Parents are responsible for being the generic template that contain attributes that *all* children should contain
> or, for the most part, *ALMOST ALL* of the attributes of parents should be common in ALL children.

That is the entire point for having the tree of parent-child relationships. Each parent specifies the generic implementation, while children specify their attributes and functions to suit themselves, and ultimately serve as generic, all-encompassing implementations for *their* children as well.

## Encapsulation
Is a side effect of creating classes, because when you create a class, you encapsulate all the relevant information for that system within that class.
The goal of encapsulation is to further create that seperation, that "black-box" of the class. Each class should be able to define how it wants its data to be used or exposed.
In typical OOP languages, we can usually differentiate *private* and *public* attributes and methods. Private methods are *only* for accessing WITHIN the object, and Public meaning that other classes may use that feature.

This promotes the ability to really care about what the class itself should concern itself with, and what information it gives out to others, adding security.

## Abstraction

## Polymorphism
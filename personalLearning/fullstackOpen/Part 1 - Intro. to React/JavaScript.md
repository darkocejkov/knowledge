- JS  is actually based on the ECMAScript standard, which in 2022, is at version ES13.
- As JS grows, browsers need to catch up, and not all browsers can do so all the time
	- Which is why browsers set their own standard for supporting JS, and we can use "middle-man" tools like Bable that "transpiles" newer versions of JS to older ones using *polyfills*.
		- Transpilation is a portmanteau of "Translation Compile", which is a process that is less about compiling to machine code, and rather between versions or languages.
- NodeJS is a JS runtime that is based on the V8 Engine that *Chrome* implements that allows NodeJS to run on any device, executing JS.

# Variables
`const`
> constant, initialized at definition. immutable

`let`
> untyped dynamic variable

*deprecated* `var`
> untyped dynamic variable that differs in *scope* of blocks.

# Arrays
> implicitly are *objects*

`const t = [1, 2, '3', {a: {b: 'c'}}, (fn) => fn()]`
> Dynamically typed arrays that contain any type of member

> [!references]
> JavaScript is untyped, but heavily relies on *references* to objects (almost like pointers)
> In the array example, `t` is a constant (immutable) variable, but we **CAN** mutate its members. This is because the reference itself is constant and not the members.

> [!Immutability]
> React contains States, which are basically interfaces to control, read, and manipulate regular JS variables that React will know about. In terms of manipulating *state*, it should only be done through the state *setters*, because any implicit (in-place) mutations to a state reference/variable will go unchecked and immediately makes functions *impure*, because the output of a React functional component cannot be 100% deterministic then.
> Certain methods on objects and arrays are "in-place", meaning that they don't *return* a copy or new object, but rather manipulate the reference to the original. 

| Reference-safe Array Functions |
| ------------------------------ |
| map()                          |
| concat()                               |

## Destructuring
We can *destructure* arrays by their index using the syntax `[a, b, ...c] = t`, which in the case of `t = [1, 2, 3, 4, 5]` then we get 3 variables, `a, b, c` whose values are `a = 1, b = 2, c = [3, 4, 5]`.

# Objects
Within JS, we can declare *custom objects* using the "object literal" notation:
```js
const obj = {
	user: {
		id: 0,
		password: '123'
	},
	status: 'inactive',
	friends: [1, 2, 3]
}
```

Object literals use the curly braces `{}`. Any objects must follow a key-value pair notation, where a "key" is paired using a colon `:` to a value, which can be any JS type, like arrays, numbers, strings, or other objects.

We can reference properties (or 'keys') of the object by using DOT notation: `obj.status`, or index syntax: `obj['status']`.
> Using this same syntax we can add dynamic or static properties at runtime as well.

> JSON?
> JSON stands for "JavaScript Object Notation" and it's a generic / general format to format objects in files (typically .json). It follows the key-value pair structure of JS objects.

## Destructuring
`const {user.id, status} = obj`

# Functions
- Two syntaxes to define functions: arrow syntax `() => {}` or keyword `function ...(){ }`.
	- *function declarations* or as *anonymous functions in a variable*.
```js
function square(a){
	return a*a
}

const square = (a) => a * a
const square = (a) => {
	return a * a
}
```

# JavaScript as Object-Oriented

## Objects and `this`
In functional React, there's no need to create "methods" for objects. In-fact, JS is not exactly Object-Oriented as other languages like Python or Java are, the `class` keyword syntax *exists*, but does not mean that it is exactly the same kind of OOP. Nevertheless, we can create "objects" using object literals. These are basically like "classes" but are automatically instantiated, if that makes sense. Thus, we can create objects with variables which are singleton properties, or methods as members through functions.

The `this` keyword is especially important when using this syntax because it allows the self-referential pointer to be binded to the object when the function runs, and is an implicit argument to functions as methods.

```js
const person = {
	age: 35,
	name: "Pleebo",
	education: 'PhD',
	greet: function() {
		console.log("Hello, I'm " + this.name)
	},
	doAddition: function(a, b) {    console.log(a + b)  },
}

person.greet() //Hello, I'm Pleebo
person.doAddition(5, 5) //10

const add = person.doAddition //"add" is a constant reference to this objects doAddition method
const sayhi = person.greet //"sayhi" is a reference to .greet method.
sayhi() //however, using this reference without the context of the person binding, it'll print: "Hello, I'm undefined", because the '.name' property does not exist on "sayhi" reference. The `this` keyword is binded to the GLOBAL object when called as a reference like this.

//namely, the `this` keyword depends on HOW THE METHOD ITSELF IS CALLED

//we can FORCE javascript to bind objects for methods by using the `.bind` method
sayhi.bind(person) //creates a "new" function bound to the object instance
```
> Arrow functions do NOT allow the `this` keyword, there is no way implicitly use it.

## Classes
As previously mentioned, the "class" functionality of OOPs is simulated in JS through the useage of objects. Objects are like *class-less* instances, which have no reference or integrity to some *class*, until we create a *class interface* using the `class` keyword.

The purpose of defining classes is to create some structure, or blueprint for objects which share those properties. If we had some generic, common grouping of properties, is in this `user` example, there must be a *better* and cleaner way to instantiate `user` objects if they always have the same properties.

```js
const user1 = {
	name: 'a',
	id: 0,
	title: 'Lonely',
}

const user2 = {
	name: 'b',
	id: 1,
	friends: [0,3,4]
}

const user3 = {
	name: 'c',
	id: 2,
	title: 'Fresh',
	friends: [0,3,4]
}

const user4 = {
	name: 'd',
	id: 3,
	title: 'Fun',
	friends: [0,1,2]
}
```

```js

class User{
	constructor(name, id, title, friends){
		this.name = name
		this.id = id
		//...
	}

	logIn(){
	
	}
}

const one = new User('a', 0, 'Lonely')
const two = new User('b', 1, null, [0,3,4])
//...
```

## How does this work?
JavaScript implements [prototypes](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes) which are basically higher-order classes for the object literals we create in JavaScript. Like previously mentioned, [[#Arrays]] are objects because they are constructed out of objects through the prototype.
Prototypes are the base "class" that allows classes that extend or interface with prototypes to inherit their features, which is a key component to [[Object-Oriented Programming OOP]].

## Prototypes?
Prototypes are implicitly defined, built-in properties to ALL objects in JS.  It's defined in the `__proto__` property. When you write JS code, and you attempt to access a property of some object, the JS runtime will attempt to find the *closest definition of that property* in the prototype chain. 
If your object *inherits* a property, or extends some other prototype which has some property, JS will look for the closest definition by look at your object, your object's prototype, that object's prototype, and onwards. If your object is not defined by some root prototype, then `undefined` is returned from the `Object.getPrototypeOf()` function.
> This is why when you try and read/invoke a property, and that property is not defined at runtime, the uncaught error screams that it `cannot read property of "undefined"`.

"Shadowing" definitions is when a child *overrides* or changes the definition of a property in the parent prototype.
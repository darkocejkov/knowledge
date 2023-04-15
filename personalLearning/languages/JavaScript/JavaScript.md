[Reference](https://javascript.info)

JavaScript was developed for the web, to enable static content to "live". It provides programmatic access to the rendered DOM elements of HTML, it's the middle-man between the programmer and the browser. It can utilize browser APIs.

In modern times, JavaScript doesn't only run on browsers. JavaScript runs on *engines* - the browser engine is embedded and 
___

# Data Types

## Primitives

### Number
- Any "number" value, an integer, float, double.
### BigInt
- A specific integer that's able to do larger than the typical 64-big integer: $\pm 2^{53} - 1$
- Denote any `bigint` numbers by appeding `n`: `90912839128381971781273n`

### Boolean
- logical type
- true/false

### String
- represent any information literally within them - `"hello"`
- 3 different ways to represent them:
	- double quotes `""`
	- single quotes `""`
	- backticks

### `null`
- is it's own special type
- `typeof` will say it's an object, it is NOT an object
- it represents an "empty" value - a placeholder, the lack of data

### `undefined`
- another special type
- represents an *undefined* value, a variable or property that has no value, or does not "exist"
- different from `null`

## Non-Primitives
- Objects

# Operators

## Nullish Coalescing Operator `??`
`a ?? b`
- means that if a is defined, then we return *a*, otherwise we return *b*.
- it treats `null` and `undefined` the same, so as long as the first operand is neither null and not undefined, then it returns it.

# Conditional Logic
## Switch
- A more concise "case"-based conditional branching syntax
```js
switch(variable){
	case "a":
		//...
	case "b":
		//...
	case "c":
		//...
		break;
	default:
		//...
}
```
- It's conditional branching based on cases of a single variable, for which the cases are values of any type
- If a case omits the `break`, then the evaluated case proceeds to the *next* case without evaluation
	- using this, we can "group" cases to have the same resulting functionality
- The equality check is *strict*, values must be of the *same type*.
- 

# Functions

### Function Declaration
```js
function sayHi() {}
```

### Function Expression
```js
let sayHi = function() {}
```

- functions are *values*, the are technically "objects"
- however a function is created, it may still be *invoked* by the syntax `sayHi()`
- while there aren't many differences between *expression* and *declared* functions, they still exist:
	- expression functions may only be used *after* they are defined, while declared functions can be used at any point
		- this is because the JS engine hoists up all declared functions, to their highest available scope.
	- expression functions are great for *dynamic* functions, whose functionality can change depending on logic and other values, we store it in a variable and can invoke it.

## Arrow Functions
```js
let sayHi = () => {
	//...
}
```


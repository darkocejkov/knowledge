# JavaScript, TypeScript, jQuery

# Interesting Libraries, Packages, and Tools

<aside>
💡 [D3 Charting library with native Crossfilter](https://dc-js.github.io/dc.js/) (DC.js)

</aside>

<aside>
💡 [Data filtering and optimization library](http://square.github.io/crossfilter/) (Crossfilter)

[World Bank example](https://drarmstr.github.io/chartcollection/examples/#worldbank/)

</aside>

# TypeScript ([https://www.typescriptlang.org/docs/handbook/intro.html](https://www.typescriptlang.org/docs/handbook/intro.html))

## Basics

## What?

TypeScript is a language ****very**** closely related to JavaScript. It is JavaScript at it’s core, except it is a ****************************strongly typed**************************** language.

<aside>
🔣 **Typed Languages?** 
Languages can vary in their degree of ‘typed’-ness, that is, how much the syntax is based on declaring exactly the types and values of functions. Python and JavaScript are dynamically, or weakly, typed. This means that whenever you create variables, the type of the variable does not matter, because it dynamically changes. The return values of functions, the type of returns, the type of the arguments are not necessary, and make it easier to create simple code, but make it really easy to have breakpoints, because you need to manually check types at runtime and use conditional logic. Typed languages enforce types syntactically, making it easier to write code that is clear.

</aside>

## Why? Why bother enforcing types in JavaScript?

Frameworks built in Java, like React, have a lot of different built-in types, which make developing slightly more verbose and difficult, but makes maintaining and developing require more thought, and thus, developing better code. This is because we would develop functions to be resilient to errors in runtime, because you developed in JavaScript without making sure the types at runtime are correct.

Here are some examples:

Exception errors, which create exceptions down the call stack and cause total crash if not handled

```jsx
const x = null
x.property
	//ERR: cannot read property of null
```

```jsx
const x = ""
x()
	//ERROR: x is not a function
```

“Non-exception” errors, which are logic errors

```jsx
const x = {
	y: 1
}

x.z
	//x.z returns undefined
```

## How do we use TypeScript?

`tsc` is the ‘typescript compiler’, packaged with the `typescript` package. 

### Emitting on/off Errors

We can use the flag `noEmitOnError` when compiling to keep TS strict, because even when typechecking indicates a problem, it will still compile and emit JavaScript

## Explicit Typing

We can write “TypeScript” as typical JavaScript, and it will work. The difference is that TypeScript allows explicitly typed variables and arguments.

```tsx
function greet(person: **string**, date: **Date**)

//OK
greet("abc", new Date())

//ERROR
greet("abc", Date())
		// Date() returns a STRING, and not a Date object
```

## Implicit Typing

TypeScript can also ******assume****** the type of a variable based on the actions taken on it. If we assign 

```tsx
let message = "message"
```

and assign nothing else to it, then TS knows its a string type.

## Type Erasure

TypeScript is compiled down into JavaScript, so it’s an extra layer, and in order for that code to be properly interpreted as JS, the typing is simply for static typechecking while writing code, and is erased when compiled into JS.

## Downleveling

is when languages move from a higher version to a lower version (typically in compilation). An example of this is when we use “template” strings

```tsx
`Hello ${x}`
```

which are translated to:

```tsx
"Hello " + x
```

or:

```tsx
"Hello ".concat(x)
```

because of the different versions of ECMAScript, templating strings and syntactical sugar might not be in the supported target JS version

<aside>
🔣 We can change the target version by using 
`--target es2015`

</aside>

## Strictness

- If we want TS to only use explicit typing and NEVER infer the `any` type, we can use the `noImplicitAny` flag to disable that
- we can enable null and undefined strictness using `strictNullChecks`

## Primitive Types

- **string**
    - “hello, world”
- **number**
    - int, float, etc. (no difference, they’re all numbers)
- **boolean**
    - true
    - false
- arrays
    - collections of types, created by:
    
    ```tsx
    string[]
    number[]
    boolean[]
    
    //OR: as a 'generic'
    Array<number>
    ```
    
- any
    - dynamic type, can be ***any*** type of data, basically disables typechecking
    

### Declaring Types

```tsx
//variable typing
let message: string = "message"
	//for most cases, TS can easily infer variable types without explicit typing

//parameter typing
greet(name: string)

//return types
function getNumber(n: number): number {
	return n * 1
}

const getNumber = (n: number): number => {

}
	//again, not NECESSARY because it can be inferred
```

→ Typing for anonymous functions is ****************contextual**************** as their calling context is used with inferred types to infer the arguments and returns of anonymous functions

### Object Typing

Create JS objects with predefined, typed properties

```tsx
function printCoord(pt: {x: number; y: number})

//optional properties
function printName(obj: {first: string; last?: string)
		// use '?' to indicate optional properties
		// optional properties are allowed to be undefined
				//a good practice is to use optional chaining to access optional properties
```

- IMPORTANT: defining objects in this manner we must use comma OR semicolon

### Union Types

are typed properties which can be one of a *****union***** of types:

```tsx
function printId(id: number | string)
```

→ operations on the argument or property are only considered VALID if the operation is valid for all POSSIBLE types

> this means that if `id` is a number OR a string, that `id.toUpperCase` is not valid
> 

→ thus, if we are unionizing types, we could also use “narrowing” principles, meaning manual (runtime) typechecking using `typeof` and object-specific “instanceof” or “is” meta functions.

### Type Alias

a way to globalize the definition of a type

```tsx
type Point = {
	x: number;
	y: number
}

type ID = number | string

//aliases are exactly that, copies or macros
type String2 = string
function fun(input: string): String2
		// this is valid, because String2 is an alias

//JS interface
interface Animal{
	name: string
}

interface Bear extends Animal{
	honey: boolean
}

//TS Type
type Animal = {
	name: s
}

type Bear = Animal & {
	honey: boolean
}
```

→ TS Types CANNOT be “re-opened” to add new properties, while Interfaces are ALWAYS extendable

### Type Assertions

Will cast or specify a specific type

```tsx
document.getElemenyById("canvas") as HTMLCanvasElement
```

→ This has uses because `getElementById` returns some `HTMLElement`, which is a parent/generic object, but if you KNOW that the element will be more (or less) specific, we can ******assert****** the type

### Literal Types

are ways of defining “enumerated” or custom shorthand types through the use of ****************constant**************** variables.

```tsx
let anyString = "hello, world"
anyString = "hi, world"

const helloWorld = "hello, world"
```

→ anyString of the `var/let` scope can be changed, so it’s type is inferred as a ******string******. however, helloWorld as a constant can never change, so it can be considered a literal type, so the contents of that constant variable is the ********type******** itself.

→ as a shorthand, we can create custom/literal types without pre-defining constant variables or aliases, but just using literal strings or numbers as types.

→ this is ESPECIALLY useful when we use union typing to create custom type choices, and limit the contents of the literal typed variables

```tsx
let x: "hello" = "hello"
x = "howdy" //ERROR, not assignable

function printText(s: string, alignment: "left" | "right" | "center")
//alignment can ONLY be of left, right, or center

function compare(a: string, b: string): -1 | 0 | 1
//returns either -1, 0, or 1
```

→ the `boolean` type is an alias for the union `boolean = true | false`

### Literal Inference

→ properties of objects must have their types correctly inferred, because even though a property is initialized as a specific number or string, ie:

```tsx
const obj = { counter: 0 }
```

obj’s *******counter******* property is not of literal type 0, but rather a `number` that is initialized as 0. TS has areas where it may infer the type as literal rather than implicitly, and there are errors when you try and assign or change. to get past this, we can use [Type Assertions](JavaScript,%20TypeScript,%20jQuery%20aaa64771717a4c229695f59d6d31bc7e.md), for specific values, or using the `as const` assertion to ‘convert’ the object to be a const type literal,

### Null Checking

we can turn `strictNullChecks` on or off to define whether TS will be enforcing that you CHECK for null values before you access methods, call, or properties of objects.

→ a shorthand that is the “non-null assertion” is this syntax:

```tsx
function liveDangerously(x?: number | null){
	... x!.toFixed()
}
```

the postfix syntax of `!` is a null/undefined check, almost identical to optional chaining
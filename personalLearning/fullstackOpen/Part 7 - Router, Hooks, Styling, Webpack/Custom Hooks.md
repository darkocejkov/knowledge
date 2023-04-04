Hooks are incredibly amazing and useful, there are so many that come with base React ^16.8 (15 of them). Every up-to-date package has some way to implement reusable logic with hooks as well.

The most flexible part is that hooks are just special functions, that can only be called within the *top-level* of other hooks, or React components.
___

# Creating your own Hooks
Hooks are great, and the fact that you can make your own is even better. Any function can be a hook, and to enforce the rules of hooks better, your hooks should always start with `use`.

Again, hooks are nothing more than functions that allow you to call other hooks in them. Why is that important? Because it allows us to extract application logic into re-usable hooks.

Based on the example from React itself, imagine we have an application that has a "friend's list", which allows you to see the status of your friends (online, offline, etc). When building a React component like a chat, you want to group and encapsulate related things. You might create a friend's list window, which is parent to container of related *controls* (filters, sorts, etc.), which has a collection of "friends" as children itself. Each "Friend" component has an avatar, their name, a status indicator.

Now, think about the status indicator, it's really simple to develop the status indicator on the Friend component, but what if you need it else where in your application? You would need to copy and paste that code to the other component. That's just bad practice, when we can extract that logic to re-use it through a hook. 

That way, when you want to use the status indicator anywhere, we can import and invoke the custom hook: `const status = useStatus({options})`. 

## Personal Experience
As stated in [[React#We've been doing it **all** wrong.]], there's an architecture that comes innate to functional components in React. It boils down to 2 simple things:
1. React components have *logic* like state and rules
2. React components return JSX that depends on that logic

Hooks should not return anything other than logical components, while components return only JSX. Technically, we *can* do both, but it's a bad introduction to anti-patterns that are not helpful down the road.

## Reusability
Hooks make it possible to reuse logic code much easier. Think of the logic of a simple counter and its logic functions; increments, decrements, managing the state of the value. What if we wanted button have *four* counters? You *could* create 3 additional logic states and functions with different names - ORRRRRRRRRRRRRR - you can make a hook ...

> What looks better, you decide:

```jsx

// NO HOOKS
const [counterNorth, setCounterNorth] = useState(0)
const [counterEast, setCounterEast] = useState(0)
const [counterWest, setCounterWest] = useState(0)
const [counterSouth, setCounterSouth] = useState(0)

const incrementNorth = () => {
	setCounterNorth(counterNorth + 1)
}

const incrementEast = () => {
	setCounterEast(counterEast + 1)
}

const incrementWest = () => {
	setCounterWest(counterWest + 1)
}

// HOOKS
const north = useCounter()
const east = useCounter()
const south = useCounter()
const west = useCounter()

	//...
north.increment
east.decrement

```

Custom hooks really shine when it comes to abstracting the logic of Form Input components, especially if ALL your inputs are controlled through React state.

Instead of having:
1. `useState` hook
2. event/change handler
	1. on top of both, each has to be named individually unique when not using custom hooks

We can abstract our controlled input states through re-usable hooks to the degree we like. We may have custom hooks for text-based inputs, number-based inputs, password inputs, email inputs, etc...

### Spreading Attributes
The spread `...` syntax is very useful and versatile and allows us to do lots of shorthanding.

Spreading is very useful when it comes to JSX and component attributes, because we can "assign" the attributes of components through the object's key-value pairs:
```jsx

const useField = (type) => {
	//...
	return{
		value: state,
		onChange: handleChange,
		type,
	}
}


	const name = useField('text')

	return(
		<input {...name}/>
	)
```
> When we spread the "output" of the "name" instance of the field hook directly on the `<input />`, we effectively map the properties of the object which share the appropriate attribute names.



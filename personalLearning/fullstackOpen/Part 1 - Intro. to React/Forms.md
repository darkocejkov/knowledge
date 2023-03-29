___
Forms can be incredibly complex, because there's a lot of room for control for both the user and the JS.
The concept of a *form* is more conceptual than a physical thing. Even though there exists the `<form>` element in HTML - forms are not rigid constructs.

# Forms and Events
- Handling forms and their submission can be handled by React's event handler paradigm
	- instead of relying on the *default* behaviour (AJAX-based) of forms, we can use events to either trigger event handlers on button press
		- the key idea is that we do not have to care about the 90s approach to submitting forms through the `<form>` element - any button can be a submit whether or not its in a form wrapper.

- For inputs that create the form itself, we have 2 methods to control their input:
1. Controlled Inputs
2. Uncontrolled Inputs

## Controlled Inputs
Are those in which we manage the *state* of the input ourselves, the current value and the way the value is set.
- This is done through *stateful variables*.

## Uncontrolled Inputs
Are those in which we *do not* manage their state directly, instead - the browser's rendered HTML input components manage their own state and value.
- The downside is that we then cannot *react* or "observe" the state of the input, and we need to know *when* to reach into the *getter* API for elements to read the value.


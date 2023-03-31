As previously seen in the [[Backend Structure & Testing]] section, it's very important to always remember the utility that automated tests bring. 
Not only do we have to verify that our backend application logic is able to be robust and can handle errors properly, our frontend should do the same!
___

# Jest & React Testing Library
Remember, Jest is a testing framework that allows us to define and group tests (which are isolated function calls that should have definable and predictable behaviours), and assert what tests *should* output.

Testing in React is a little more confusing, because we're *rendering* content. Using Jest with a package called `@testing-library/react` with `@testing-library/jest-dom` allows us to create powerful render-based tests.

Here's an example:
```js
import React from 'react'
import '@testing-library/jest-dom/extend-expect'
import { render, screen } from '@testing-library/react'
import Note from './Note'

test('renders content', () => {
  const note = {
    content: 'Component testing is done with react-testing-library',
    important: true
  }

  render(<Note note={note} />)

  const element = screen.getByText('Component testing is done with react-testing-library')
  expect(element).toBeDefined()
})
```
> Here, we use the `render` and `screen` exports from RTL to render (without the DOM), and access the rendered content using screen.

## `@testing-library/user-event`
Allows the execution of user-based events, like clicks, etc...

# Children as Props
HTML is based on the parent-child relationships between components and their composition.

React components are typically stubs, or "leaves" in terms of hierarchy.
Like for example, you'll most often see `<Note />`, in which the component Note, has no children that it wraps.

React components *can* wrap others, and we can access the children components in the parent to render them through the `props.children` array. Even if it's a stub component with no children, the array is an empty one.

# Refs
Another common hook provided from React is the `useRef` hook, in which we can create a state-less variable to access direct values.
This is most ocmmonly used to create direct *ref*erences to DOM elements.

# Prop-Types
A package like `prop-types` allows us to define a "schema" for component props.

```js
import PropTypes from 'prop-types'

const Login = ({handleSubmit, username, password}) => {
	// ...
}

Login.propTypes = {
	handleSubmit: PropTypes.func.isRequired,
	username: PropTypes.string.isRequired,
	password: PropTypes.string.isRequired
}
```
> This is similar to the reason we'd use TypeScript, it doesn't offer additional functionality, but adds a better developer experience (DX).

# End-to-End testing (E2E)
Unit testing is about the function of single components in isolation, things like whether or not buttons do what they're meant to do, labels and styles.

End-to-end tests are similar in terms of framework to unit testing like Jest - we define tests, invoke actions, and assert the expected results.

Some common frameworks used for e2e testing are *Selenium* and *Cypress*. The important part is that instead of testing a single component, we test a page, view, or flow's function with buttons.


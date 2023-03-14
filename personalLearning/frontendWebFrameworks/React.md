# ? ? ?
React is a [[Frameworks]] built on [[JavaScript + TypeScript]]. React has very interesting principles that it uses
to accomplish it's goals, because it is essential a scheduler that holds information about the DOM that it constructs, and schedules direct changing to those DOM elements. 

## JavaScript as a DOM Manipulator
JavaScript was built to programatically read and write from/to DOM nodes in the DOM tree. You can set up a simple HTML form, and using JavaScript, you can extract all the info from those elements. You can attach *listeners* and to DOM elements, and perform dynamic changes. JavaScript deals with the DOM.

React, is a DOM manipulation engine. In your `.js/.jsx/.tsx` files, you write in terms of components (classes OR functional), and those will eventually be ran (somehow, sometime), in-which React will track the components to add, change, or remove from the (shadow) DOM that holds in its memory. React only *re-renders* or *updates* DOM elements that have state changes, and not the entire tree of DOM elements
- This is why React is so special, and allows for things like single-page applications. Instead of relying on totally different HTML definitions, you can *dynamically* insert HTML using JavaScript, which React tracks.

> [!hot] Manipuling the DOM outside React
> Bypassing React and manipulating the DOM without React knowing about it is going against everything React is about, it's very bad practice to do so.
> - That doesn't mean you CANNOT do it at all, it just means that you need to do A LOT more work to make sure that your changes don't mess with React at runtime, because when React *expects* a node to be there (and it's not), then it FREAKS OUT.
> -

## Using D3.js in React

<aside>
💡 [https://blog.griddynamics.com/using-d3-js-with-react-js-an-8-step-comprehensive-manual/](https://blog.griddynamics.com/using-d3-js-with-react-js-an-8-step-comprehensive-manual/)

</aside>

<aside>
💡 [https://wattenberger.com/blog/react-and-d3](https://wattenberger.com/blog/react-and-d3)

</aside>

<aside>
💡 [React-based animation elements](https://www.framer.com/docs/introduction/) (FRAMER)

</aside>

<aside>
💡 [Simple and highly interactive graphing library](https://formidable.com/open-source/victory/guides) (Victory)

</aside>

<aside>
🟡 [https://www.framer.com/motion/](https://www.framer.com/motion/)

</aside>
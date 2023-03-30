Styling React applications has many different avenues and tools to choose from. The most common:
1. Old-school, single CSS file
2. CSS Preprocessor
	a. a tool that allows additional features to help devs write less, but more effective code.
	  i. SASS, LESS, PostCSS, ...
___

# CSS
- is a language that combines *selectors* with *declarations*
- we use a selector notation to choose elements programatically, then impose styles on them using declarations of the style `property: value`.

## Selectors
| Selector Syntax | What it Selects |
| --------------- | --------------- |
| .               | class           |
| #               | id              |
| \<tag>          | DOM elements of that tag                |
> There are SO many different types of selectors, pseudo-selectors, pseudo-elements, etc.
> The most important part is that selectors in CSS are aware of the hierarchy of elements, so we can get really specific by chaining selectors.
> - For example, `aside p a .card-link {}` selects any anchor with the class 'card-link', within paragraphs, within aside element.
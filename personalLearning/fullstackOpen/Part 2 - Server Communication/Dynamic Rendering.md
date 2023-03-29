___
# Arrays as data sources for rendering
Most often, the data sources that we use for various APIs, or even just static data comes in the form of arrays. It's the easiest way to represent a collection of objects with properties that you want to display.

Instead of using static indexing to try and manually map elements of arrays to components, we can use built-in iterator / higher-order functions methods:
| Array Function | Description                                                                                                                    |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| map            | applies a transformation function to every element and creates a NEW object                                                    |
| filter         | creates a new list with elements that *pass* some conditional expression                                                       |
| reject         | inverse of `filter`                                                                                                            |
| find           | filter, but returns the FIRST element that passes                                                                              |
| findIndex      | filter, but returns the INDEX of the first element that passes                                                                 |
| forEach        | iterates through all elements (for each element ...)                                                                           |
| reduce         | forEach, but allows for an *accumulator* to be past, which is a cross-element variable for which we can "accumulate" something |               |                                                                                                                                |

## `.map`
Is hands-down the most common function used to render a collection of items
```jsx

return(
	items.map((item, index) => {
		return <Item {...item}/>
	})
)

```
> `.map` creates a *new* Array whose length matches the mapped array's length, and whose content depends on that array as well.
# Unique `key` attributes
> When React deals with a dynamic list of items and renders this collection somehow, it expects that each component that we render receives the `key` prop/attribute
> - This is so that React can have an easier time understanding which component is mapped to which element in the array easier, and can target changes to the changed one.

These `key` attributes should be *unique* per each list. So, we *can* use the same key attributes when dealing in different levels of the component tree, the unique part only matters for sibling elements.

- `key` attributes should be attributed to the highest child component, those which would be siblings.

> [!warning] Using list indices as keys
> Using list indices as keys is considered an *anti-pattern* because if two+ elements were to change position, the IDs *do not follow* the order of the old positions.
> This is only a concern when we directly render a *mapped* collection, because on every re-render, the indices do NOT follow the order of the elements, but always maintain that linear 0 - (len - 1) pattern. This is allowed only when we manually map these indices to elements before rendering them.
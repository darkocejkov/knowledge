# Basic Web Development (JS/HTML/CSS)

# JavaScript

JS is a huge incorporation to any website, it adds progamming features to the functionality of websites. It's large codebase is able to add functionality to webites in the form of user experience, like animations and dynamic content. It can also be used to create graphics and connect to backend databases to retrieve data.

To include JS into any website, we can define what JS file we want to use and reference it in the HTML as such:

```html
<script src="scripts/main.js"></script>
```

### Variables

Like any other scripting or programming language, JS has variables that we define using either:

```jsx
let variable;
var variable;
```

→ it's better to use *let* because it does the same thing *var* does, but better.

Variables are dynamically typed, which means that they take on any kind of value:

- String
    - 'string' or "string"
- Number
    - 10, 1, 0, etc.
- Boolean
    - true/false
- Array
    - [1, "string", false] (any typed)
- Object
    - everything in javascript (including functions) are objects.

### Operators

Are how we manipulate and define the logic in statements of comparison or arithmetic.

- Addition, Subtraction, Multiplication, Division
- Assigment
    - assigns a value to a variable
- Equality
    - checks if the two values are equal (===)
- Inequality
    - checks if two values are *not equal* (! or !==)

### Conditionals

Are how we structure the *branches of choice*. These conditionals offer any program the option to perform different actions based on the values of variables.

```jsx
if( x === y ){
		// execute this block of code
}
else if( x === y+1 ){
		//execute this block of code
}
else{
		//execute this block of code
}

switch( expression ){
		case x:
				//code block
				break;
		case y:
				//code block
				break;
		default:
				//code block
}
```

### Functions

Are a way of *encapsulating* and packaging blocks of code. The practical use of any function is that rather than having duplicate lines of code that do the same thing, we pack those into a function and can just *call* the function whenever we want. 

This is especially useful when the function we want to perform is complex and requires a lot of lines of code.

In JS, functions are also considered as *objects*.

```jsx
function add(x, y){
		let sum = x + y;
		return sum;
}
```

### Events

Are built-in functionality that allows us to track the *events* of websites. Events are an action, and to be able to notice that they happen we need a *listener*. When our listener detects that an event has an occurred, it must be able to do something about it. Thus, we also use an *event handler* to do exactly that.

# HTML

HTML is a *markup language*, which means that the syntax and keywords allow us to markup any document and define its format and structure.

The main use of this is so that any document with information can be structured and have a proper format. This proper format allows CSS and JS to work on this document and render it and manipulate it.

HTML has three kinds of tags:

- Sectioning Elements
    - headers
    - article
    - aside
    - navigation
    - section
    - divider, etc.
- Semantic Elements
    - header
    - main
    - body
    - footer

(not an exhaustive list)

The combination in which these tags are created and their order constitute the structure of any website. 

These tags have *opening* and *closing* tags, which defines the content that is within them. Within any tag content, there can be text, or other tags. When other tags are within tags, this deliniates them as *children* of the *parent* tag, creating a *tree structure* of elements.

These tags also determine how content is presented, and should be used for what they're intended as. For example, the *navigation <nav>* tag should be used for navigation links between webpages, but specifically the sections of websites that are meant to hold other same-domain links. You wouldn't use this tag to hold content that is meant for the main call to actions for example.

Tags can be considered objects, as they have *attributes* that allows its settings to be tuned. Every tag type has its own set of attributes that can be altered, which we use to define its properties.

<aside>
⚙ id → unique ID for any single element
class → shared ID for any classes of elements
style → add CSS styles to any element directly

</aside>

### Links

Are specific domain links that are able to link documents together, or even to different parts of the same document. This is done through the *anchor* tag <a>, whose *href* attribute defines that link.

In the *href*, if we include a *hyperlink:* [http://www.hyperlink.com](http://www.hyperlink.com), its activation will take us to the linked page. This behavior is further altered with the *target* attribute that can take on:

- _blank
    - opens the page in a new window or tab, etc...
- _parent
- _self
- _top

If instead of a hyperlink, we include the *id* of another element, in the form of:

```html
<a href="#id"></a>
```

Activation of this anchor jumps the page to wherever this element is.

# CSS

Stands for Cascading Style Sheet, which defines the styles of elements in any HTML format. Without CSS files and styling, webpages would be rendered in a very boring fashion, with a single font and spaced poorly. 

CSS allows the definition of styles between elements on the HTML DOM, and does so using the identifiers given to elements. Because the DOM is structured as a tree, we can also use the relationships between elements to style them.

CSS uses *selectors* to select specific elements of HTML. If we use *tags* as selectors, any styles applied to them would apply to *all tags* of the same type, regardless of their ID.

```css
body{
		margin: 0 auto;
		width: 70%;
		font: 100% Georgia, "Times New Roman", Time, serif;
}
```

### Selectors

In order to gain more *specificity* within the HTML, we can use either:

- class selectors ( . )
- ID selectors ( # )

These specific selectors allow us to select specific elements within the DOM to modify, and can have different stylings for <a> elements for example.

We can *compound* this selection by including more specifics like:

```css
p{ }
.myClass{ }
p.myClass{ }
p.myClass#id{ }
```

Going from least specific to most specific.

We can even select elements that are specific to other ones, like <a> element within a list element:

```css
ul a{ }
p a{ }
```

The first selects any anchor elements that are within unordered list elements, while the second selects anchor elements within paragraphs.

Because of the parent-child relationship of the DOM, there are also parent-child selectors:

```css
article > p { }
```

This selects all paragraphs that are direct children of the article.

```css
h1 + p { }
```

Selects the first, adjacent sibling paragraph that is directly beside the h1

```css
h1 ~ p { }
```

Selects all siblings of the h1 which are paragraphs.

We can also select by the *attributes* of elements, and combine this with *regular expressions* to be more specific.

```css
[title]{ }
a[title]{ }
```

Are ways to select all elements which have *a title (*but not a specific title).

```css
[title="first]{ }
	//all elements with the exact title
```

This selector selects all elements with a title attribute that is *exactly* "first". This is a list of regex operators we can use:

- ~=
    - attribute has value anywhere
- ^=
    - attribute starts with value
- $=
    - attribute ends with value
- *=
    - attribute has value anywhere

Properties in CSS are a large list of properties that we can assign values to. This is done like this:

```css
property: value;
```

Depending on the property itself, values can have different meanings.

### Pseudo-classes

Are classes defined for elements to represent current states and event changes, with the same specificity as a normal class does.

LVHA:

- Link
    - unvisited link
- Visited
    - visited link
- Hover
    - mouse hovering over element
- Active
    - after clicking element but before next page loads
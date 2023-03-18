[Documentation](https://nextjs.org/docs/getting-started)
[Learn](https://nextjs.org/learn/foundations/about-nextjs)
[Create NextJS App](https://nextjs.org/learn/basics/create-nextjs-app)
___

> NextJS is a [[React]] framework that is meant to make building large-scale applications simpler, because it pre-includes many of the most important optimizations and features for successful web apps, and specifically for [[Single Page Applications (SPAs)]]
> - User Interface
> - Routing (URLs)
> - Data Fetching (dynamic content)
> - Rendering
> - Integrations (CMS, authentication)
> - Performance
> - Scalability
> - Infrastructure

# React? 
React allows you to create and manage *components* to build UI, but is un-opinionated on HOW we use those things, and how we integrate with other parts of the application.
React has *many* different plugins to support the things mentioned above, but the whole point is that it's quite manual and custom, and if you don't do proper planning, research, and design, you'll be far down the road of writing an app that is missing so much optimization (ask me how I know).

React is very Do.It.Yourself, it's great for creating an organized, interactive UI for a codebase, but lacks in dealing with large-scale backends without a lot of involvement of external packages, and custom development.

# Next vs. React
Next is **built on** React, meaning that we use React to build the UI, but Next then also solves a lot of the issues we've had in React when it comes to integrating with servers, etc.
> Essentially - React is built for UI and interaction, and Next builds on React to make a more complete toolchain.

# User Interface (UI)

## HTML
HTML is a *markup language*, that allows you to give order + hierarchy to various elements. There is an inherent root-child-parent ==tree== relationship between all the elements in HTML.
> HTML -> Browser -> renders elements based on HTML through the #DOM

## DOM
- Stands for Document Object Model, the object-representation of all elements to display.
The DOM has browser-defined rendering relationships and a standard for displaying content, so that all browsers have some way to render what is meant to be universal content (ie. everyone can see it)

JavaScript allows you to manipulate the DOM through the DOM API.

## JavaScript
Since we can create, remove, and edit the DOM that is visually rendered through JavaScript, we can create rendered elements once the browser runs the JS. 
HTML is the *initial page content*, while the DOM is the *updated page content* that changes as JavaScript runs.
-> JavaScript is *imperative*, meaning to manipulate the DOM, we have to imperatively declare how to update the UI.

> [!Imperative vs. Declarative]
> **Imperative** is when you tell the chefs exactly what, how, and when to do the tasks related to creating a *pizza*
> **Declarative** is when you ask the chefs for a pizza, perhaps some additional information, but the details of how the pizza is constructed are left for the chefs.

# Basics of [[React]]

**React** is declarative, because you tell React what the desired outcome of the interface should be, and it generates the JavaScript code for that to happen.

## Components
-> React is so powerful because it allows us to define structure of complex UIs through **Components**, which are essentially functions that generate some HTML (through JSX)

-> With components, we are able to pass *props* between components to provide them with dynamic information to render with.

## States, Hooks, and Events
-> React allows you to attach *event handlers/listeners* to JSX components, which are pre-defined functions to manipulate something

-> That "something" you manipulate is typically the *state* of some logic, such as a component. Think of a Toggle switch, whose state could be "Toggled" or "Not Toggled", or a number, a string, etc.
-> State is something that we want to *keep track of*, which has the possibility of changing.

-> Hooks are functions that we can use to "hook into" the logic of states, effects, etc.

# React vs. Applications
React itself is very, very powerful at building a user interface. However, a large application typically has a LOT more going into than just UI. Very common is the ability to have *dynamic* content through APIs. 
- Think of Facebook. Every time you request Facebook - your page takes a couple seconds to load all the information, and then a giant portion of the content on your page comes from APIs:
	- each post you see stored in a database
		- each post's attributes (likes, views, comments) etc are all relational to that post in a database
	- anytime you contact the server for posts, articles, etc. you aren't just asking for ANY posts, posts are all related to YOUR information, your account, your friends, etc.

> Overall, React can build killer interaction which is what it's built for. NextJS expands on React by providing the rest of the logic.

# Building with Next
Next has 3 different choices that impact how we build and deploy the Next app:
1. environment *where* code runs
	1. development vs. production
2. *when* code runs
	1. build-time vs. run-time
3. *where* **rendering** occurs:
	1. client vs. server

## Environment
> Development vs. Production
> > the "context"

## Rendering
Is the process of running React functions to generate the HTML that will be interactive.
Rendering has 3 methods:
1. Server-Side
2. Client-Side
3. Static Site Generation

### Pre-rendering (SSR or SSG)
Are considered as pre-rendering methods, because they are rendered *before* the the client receives the request, we pre-render on the server to send back some intial content.

### Pre-rendering vs. CSR
Client-side rendering is dependent on using the host's browser to compute and render the graphics, then display it. The idea is that we pass them some empty HTML - then the generated instructions (from React) on how to render and display each page, component, etc.
-> So, there is a period of time in which our app has virtually no meaningful content other than the basic, root HTML that it populates.

### Server-Side
Server-side rendering in specific, means that each page is generated on the server (each request), so we pre-render meaningful content, and then pass to the client:
- HTML
- JSON data
- JavaScript

So on initial load, we see a nice pre-rendered (non-interactive) page that is then passed to React to make it interactive. This process is called **hydration**.

### Static Site Generation
HTML is *built* and *generated* on the server, so it becomes a static site. No server is working on a runtime that generates content.
-> However, *incremental static regeneration* is a method that allows to create/update static pages after building

> [!tip] NextJS makes each rendering option work per-page, so depending on the nature of the page, each can be rendered in the most appropriate way.

## Networking & Serving

The NextJS application can be distributed over 3 types of networks:
1. Origin servers
	1. the main, original computer that stores and runs application
2. Content Delivery Networks
	1. store static content (HTML/images, etc) in cache locations around the world, which communicate with the *origin* server.
	2. requests from anywhere in the world are able to find the closest CDN cache to retrieve static files from.
	3. requests are then load balanced because the network is distributed
3. the Edge
	1. Edge servers are similar to CDN networks, they are distributed and serve cached content
	2. Unlike CDNs, they are still servers that can execute code.




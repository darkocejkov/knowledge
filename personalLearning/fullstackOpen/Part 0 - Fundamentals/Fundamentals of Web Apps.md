Before we start creating "web applications" we have to understand what they are founded on. 
Think of any "application" in general, it's a collection of source code, that runs and computes; they *do* things, and typically they allow you to *interact* with parts of the application.
Applications are nothing more than code executions that have some *application* to some problem. They automate tasks, they compute things, they display things.

Furthermore, applications must be *ran* on something. There must be some "platform" or "engine" that allows the code to execute. 

Web applications are honestly, just that. When the internet *just* started, having web applications, or web "sites" do things was quite difficult because there was a clear limitation in the power of browsers and the throughput of networks. Websites were just static HTML pages with perhaps a small amount of programmatic flare to them.

HTML is the language that we serve content in, because it's a standardized way to *markup* documents, in which a standard has been established on *how* to implement the visual aspects of HTML.

# Network Requests
Web applications are based on *network requests*. Your computer (specifically, the browser) sends requests over the internet to *other* computers, called **servers** to ask for content. 

When you enter a URL, your browser takes that human-readable string, and tries to find out which server to ask through the DNS chain of command - because servers are NOT addressed through word-based strings, but rather `IP addresses` which are unique. So, your computer tries to find the official relation between the word-address and the IP address through DNS chaining.

When your browser resolves the IP address, it is able to make a direct connection to that server to ask it to do something - like ask for a document on that server, or, ask for some data, or to perform some complex computation on data.

`PING google.com(yyz12s08-in-x0e.1e100.net (2607:f8b0:400b:803::200e))`
> is an example of IP address resolving. 

Regardless of how IP's are resolved, whenever you communicate to a server, you do so through a specific way of communication called: `HTTP: Hyper Text Transfer Protocol`.
> Protocols are just standards of how to pass data between communicating agents.

HTTP as a standard of communication means that all agents wishing to communicate to other agents must conform to some version of HTTP to be understood by others. HTTP has 4 *methods* it uses to tell receiving agents what the sender would like to do.
> GET, PUT, POST, DELETE
> There are many more, but these are the 4 fundamentals. 

Again, whenever you request a URL, like `google.com`, your browsers opens a pipeline of communication with the resolved server and does things like issues a `GET` request for the application associated with the URL.

In order to dissect and view network requests, we can use the `Developer Tools: Network tab` to view the list of issued, pending, completed, and errored network requests sent from our browser to the server. 

![[Pasted image 20230327154400.png]]
> The `Headers` tab indicates all the "headers" of the RESPONSE and REQUEST, which are like meta-data about the request itself. There are common/standard headers that indicate basic information about the server, like the type of content an endpoint sends back, the life of the connection that's established, etc.

When you request a web application, it will pass back documents and/or data, to which your browser then decides what it should do. In the case of an HTML document - it will *render* that document by creating a DOM (document-object model) tree from that HTML.

HTML documents can also trigger other network requests through things like images. Instead of "bundling" an image into the HTML document, you *reference* that image from an endpoint/URL on the server. So, when the HTML is rendered, it then requests the image(s) on the server. 

![[Pasted image 20230327155013.png]]

> This is the crux of what web applications are built on. Servers that *serve* content such as HTML documents and static files, to which we can *compose* content within the HTML.

# Events & Handling Them
JavaScript is very different from other scripting languages is that its meant to be *asynchronous*. Dealing with events over the internet can be wildly difficult because there's no guarantee that requests or responses will actually come back, and especially the time it takes for them to. It could take milliseconds, or even 10 whole seconds - no one knows, and it will always vary.

That's why JS is so powerful, because we harness the use of JS events and event listeners to create asynchronous functions. We listen (publisher-subscriber style) to specific events and define what happens when those events (and even more specifically, when specific things within *those* events happen).

# Rendering Applications
Modern technology has enabled so much in terms of how we create and render HTML documents. Think about how server computers *serve* content to us when we request it.
1. Browser sends HTTP request to server asking for content
2. Server receives HTTP request
3. ... ?
4. Server sends HTTP response back to agent

There is a space in between the steps the server can take. Servers are other computers essentially, and can do loads of different things. If the resource that we request is a static file, servers can *statically serve* those files to us without doing much "processing". We are also able to then serve *dynamic* content based on dynamic data through running the application logic on the server. This is how traditional web apps worked, we generate HTML and send it back from the server.

This is as opposed to rendering the HTML document or its contents from within the document itself, which is possible through JavaScript. 
JavaScript is a scripting language that allows the manipulation of the DOM tree, and it can also perform application logic relative to fetching data, and computing. 
We can *enable* client-side (within-document) rendering by using `<script>` tags to link or define programmatic scripts to run within the document itself.

As we go deeper into the idea of rendering, this starts to also build on what is fetched from the server on initial load - when we create the inital GET, the server sends back some HTML, which has links or *references* to other files, also on the server, which the browser starts creating additional network requests for those. Documents like *stylesheets* and *scripts* that are implicitly referenced need to also be fetched, because the *style* and *function* is affected by those things. 
> We could forego code seperation and just define those things within the single HTML document, but obviously, as our application gets more and more complex, it becomes MUCH harder to organize code AND, makes the initial size of the HTML document larger than necessary - which means that on slow connections, users might see *nothing*.

# Manipulating the DOM
Like previously mentioned, we use JavaScript to manipulate and read parts of the DOM, which we can use  to either render new content by creating new DOM elements, edit content of existing DOM elements, or read the values or content of the DOM.

# Stylesheets
Stylesheets are written in a language called "CSS", standing for "Cascading Style Sheets". They "cascade" because they create an implicit hierarchy based on the assignment of styles to elements.

CSS uses *element selectors* like the **class**, **id**, or **type** of elements to "select" and style them.

## Classes
Are meant to be more "re-usable" forms of CSS selectors, in which we can create a "class" or "component-esque" definition to re-use.

## IDs
IDs are meant to be *unique* between all other elements, meaning that there should only be 1 ID per element which is NOT shared by any others.

## Type/Tag
We can also select elements by their generic DOM type, such as `img, p, h1` etc...

# Forms & POSTing
A `<form>` element is a wrapping element to denote the *function* of all the wrapped elements, or to differentiate two+ forms with different function.

Forms are AJAX handlers, they are mean to initiate some sort of AJAX (*Asynchronous JavaScript and XML*) actions, typically an HTTP POST. Forms are implicitly meant to intake data, like a user form. You fill in the inputs of a `<form>` and submit it.

If you give a form the `action` and `method` attributes, any actions that "submit" the form will cause an AJAX-based request to fire.
- AJAX Forms will *refresh* the page.
- The Content-Type is implicitly set as JSON.

# Single Page Applications
SPAs are more modern approaches to building websites and web apps. The traditional approach uses server-side based rendering to serve either static or dynamic HTML, with the key difference is that each of these places are placed at different endpoints and they create different "pages" so-to-speak.

Instead of having pages being seperate entities, we can use modern JavaScript approaches to continuously construct our pages, almost like *virtual pages*.  

Instead of requiring page refreshes to re-generate and re-fetch dynamic content, we can use JavaScript to do so. 

# non-AJAX Forms
Instead of using strict AJAX functionality on form elements through the action and method attributes, we can just create an *event handler* for form submission and deal with the server request ourself.

# JavaScript Libraries
There are plenty of libraries and packages for JS that extend its base functionality. `jQuery` is an example which was super popular.

# Fullstack?
What exactly *is* a fullstack developer? It's really just a shorthand for saying "frontend AND backend developer". 
Web applications can typically be abstracted into 2 main layers:
1. Frontend
	1. Visual HTML Interface rendering
	2. JavaScript-driven interactivity
2. Backend
	1. API to handle requests
	2. Read and Manipulate data from non-volatile stores (database)

In-fact, there's a lot in-between and a lot of complexity in each side. It becomes a lot more confusing when server-side rendering exists, or serverless APIs, different tools to query APIs, different kinds of databases (relational vs. object-relational), etc.

There are so many things to consider, and sometimes it's better to *specialize* in one or the other. However, they tend to go hand-in-hand.
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





Running a *local server* on your development machine is useful since it's super easy, and free. However, no one *else* can access your application, because *localhost* is specific to YOUR machine.
___

# CORS + Same Origin Policies
CORS stands for Cross Original Resource Sharing, and is a safety measure implemented by browsers fetching resources.
When you visit a website, you ask the server the website is served from, for the files of the website - which are easily passed to you. Suddenly, the HTML has references to *other documents*, which you also need to fetch - JS, CSS, and images. These documents don't *need* to be on the same server as the website, they can be served from anywhere.

An endpoint URL is broken into 3 pieces (a scheme:`http://example.com:80/index.html`
- Protocol: `http`
- Host: `example.com`
- Port: `80`

Whenever a document is requested from the HTML document, the browser intercepts this to check whether or not the HTML document is requesting from the *same origin* that the HTML is fetched from.
- In the case that the scheme is *not* the same, then the browser checks the header `Access-Control-Allow-Origin` response header to see if the server allows these external files to be fetched from the requester
	- if the value is `*` (the wildcard), then any URL can fetch the resource(s).
	- Otherwise, the URL must match
- If the URL of the ACAO header does not match the requirements, then the browser steps in and throws an error and does not allow the resource to be fetched
	- This is to enforce security and vulnerability concerns, and is not specific to our implementation stack (node+express).
- If responses from the server have *no* Access-Control header, it's as if the header matches no URLs, and thus will be always blocked.

> If you think about it, this makes a lot more sense when there's APIs that require limited access. If you think of some *private* API, then logically, the only way you can limit who can query this API is to limit who the request comes from.
> Or, you can issue *tokens* or *keys* that are proxies of authentication, so any sender is allowed, but they must have some valid authentication key.

When we start deploying our backend and frontend to the internet, CORS errors *will* happen.

Specifically to Node, we can use the `cors` package as middleware to "inject" the header and configure CORS rules.
```js
//npm install cors
const cors = require('cors')
app.use(cors()) //*
```

# Actually Deploying
This part is another part that can be intensely complicated, depending on what platforms, tools, or technology you want to use.
This is it's own study honestly, and the scale of the application (or planned scale!) dictates how to approach deployment.

## Slight Depth
In order to understand what "deploying" is, think about a computer on the internet. Any computer can talk to any other computer, given that you know the *IP Address* of that machine.

As in [[Fundamentals of Web Apps]], when you type an address like `google.com`, a lot of things happen in the backend that allows you to contact Google's servers for the HTML, for the ability to search, and access to its services.

Deploying a web application requires a lot of manual work if you get into the details of it. You could *definitely* deploy a web application from your computer if you made your machine's IP publically exposed.

## Platforms as a Service (PaaS)
Instead of trying to manually deal with all the servers, IP addressing, DNS listing, rules, ... you could just use a platform hosting service like `Render` or `Fly.io`, `Netlify`, etc.

What they allow you to do is pass it the code and runtimes that you want to host/deploy/serve, and configure the instances to suit your application and it automatically deals with all the difficult stuff. 
> It should be somewhat obvious, but these services are meant to be ways to introduce the concept and tools of online hosting. When applications start growing, more and more users start using it, then a different deployment method is necessary.

## Production Builds
In the `create-react-app` lens, when you are developing your application, under-the-hood you're actually using Webpack to hot reload and re-bundle your application when changes happen - and your locally hosted development application uses a "development build" in order to make development, easier. More logging, strict mode checks, less minification and obfuscation.
However, it's more efficient to serve production bundles because end-users don't need all the development tools. 
> In fact, the development build of React projects has quite hindered on performance. It's difficult to see in simple applications, but performance is *much better* in production builds, the size of the bundle is smaller, and is more difficult to "reverse engineer".

In order to create a "production build", we use some `build` tooling. `create-react-app`'s `react-scripts` package comes with one that is easily ran using `npm build`.

# Deployment Pipeline
We go much deeper into this concept later, but the general idea is that we have some manual process to deploy our application - a chain of CLI commands to build our application, push changes to an origin repo, go to the servers and pull changes, ... so on so forth. 
A deployment pipeline is best *automated* or somehow streamlined into a simple process.
For example, the process within AWS Amplify is very simple, it handles all of the phases of what's called "CI/CD" (Continuous Integration, Continuous Deployment).
From the start, all it cares about is your git repo. It notices any new commits or changes through *webhooks*, and then pulls all the new changes in the requirements phase, starts the `build` operation that's defined by configuration, on successful build, it deploys those changes to its servers. It does not deploy if builds are unsuccessful as well.
# What?
> 	NodeJS is a #javascript runtime (engine).  What this means is that it's an environment that allows us to write javascript code, in order to perform functions.

First off, JavaScript was built to be native in the browser environment. Browsers fetch HTML, CSS, and JavaScript files, which then are ran through the browser. HTML marks up documents to build a hierarchy of parent-child relationships, CSS defines the rendering style of those HTML nodes, and JavaScript allows the manipulation of data relating to HTML nodes.

NodeJS however, is a JavaScript runtime that is INDEPENDENT of any browsers - all NodeJS is meant to is run javascript code. This lets us build applications that do all sorts of things. You can use NodeJS for a variety of industrial applications, and even just as a way to perform data manipulation, or run javascript printing functions.
- Various packages and libraries have been built for NodeJS runtimes that extend the functionality to handle all sorts of requests.
	- Express is a package that allows for NodeJS to handle network (AJAX/REST) requests by creating a "middleware", which routes 'endpoints' to functions.

> JavaScript for browsers operates on the DOM and was built around accessing and changing DOM object values.
> NodeJS takes the features of the language and makes it able to do server-based Node commands, which allow you to manipulate file systems, create command line arguments, etc.

Typically, NodeJS is ran on servers to handle server requests, like when clients request data to do various things. 

# "Global" and Scope
Browser-oriented JavaScript creates the *global* object to be the *window*, while in NodeJS, it's simply called **global**.
NodeJS functions are typically scoped to the global namespace so Node *infers* certain functions to come from global, just like it does in the browser.

However, any variables we define in the scope of a file do NOT get scoped to the global namespace.

## Path
`path` is a (imported) module within NodeJS that lets us deal with *paths* of files. Inside this module is very many functions that help us create and parse filepaths for precisely manipulating file systems.

## Process
`process` is a global module that deals with the *runtime* process as a whole.

Using process, we can get information about the currently running `node` process and meta-information given to the process from user arguments, and deal with standard inputs and outputs from commands.

### `process.argv`
-> Is an array/object that contains the argument array of the process
> typically, when you "run" a file with node, the first two arguments are always `node <file>`, so the first two arguments in `argv` are:
> 1. location of `node` command
> 2. location of `<file>` as a path.

When you know how to *read* `argv` you can then start creating specific command-line tools with different options by reading argument flags.

### `process.stdout` & `process.stdin`
Allow us to access the "standard" in and outputs for the process. We can write to the output to prompt users, and also prompt for input.

### `process.?.on`
NodeJS allows us to create *listeners* so that we can listen to, and respond to events. This is super important, because without them a NodeJS "program" that runs on the process has no simple way to wait for events, and thus follows the start - do - end cycle where we would start the program, it would do everything, then end and there's no opportunity for user input, etc.

## Events
Events are powerful ways to create listening apps, they are what the `.on` methods are built on, which allow us to go from a linear, procedural program to a *pub-sub* pattern.

> Just like in `socketio`, we're able to hook into the logic of events by using the `.on(eventName, callback)` which *listens* for events and performs the callback, while we can trigger these events by "emitting" using the `emit(eventName, arguemnts?)` hook.
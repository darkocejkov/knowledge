___
This will be a technical interview with a live coding exercise. You will be asked to build a simple application that will gather input from a user, make a call to an API you build, and render the results to the user. The API will have to be built in Node.js. We would prefer that you use React for the client, but another frontend may be used (though you will have to justify your decision).

Please be prepared to write and run code on your machine using a recent version of Node.js and to share your screen.
___

# Bootstrapping a React Project

## Toolchains
### create-react-app
- includes all relevant tools you need to develop, run, and build a React project
	- Babel, Webpack, ESLint, html/js files, config files, etc...
- using the individual tools is great if you "know" what you're doing, and have a specific need to NOT use `create-react-app`. 
- you *should* be using this toolchain to create a project - to kickstart your development. 
	- in the case that you need to handle individual configurations and installations - you can use the `eject` command-script to eject CRA and just get the files

## Transpilers
### Babel
- Translates versions of JS to other versions of JS - specifically because we use JSX to increase developer experience (DX) and that is not runnable by browsers natively - so it must be converted to vanilla JS.

## Bundlers
### Vite
### Webpack

# Bootstrapping a Node.js API
```bash
npm init;
npm install express nodemon 
touch app.js

#package.json
scripts: {
	"start": 'nodemon ./app.js'
}

```
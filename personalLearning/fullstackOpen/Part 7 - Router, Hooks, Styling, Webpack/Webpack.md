`create-react-app` is an amazing point to start off development. Before this tool, it was very difficult to start React projects because they required a lot of configuration for tools that are difficult in and of themselves.

We don't need to rely on the c.r.a tool to do everything, and there are circumstances in which we shouldn't/can't use it.
___

# Bundling
React is a client-side rendering approach to building web applications. We write JavaScript code to declaratively define what the UI is supposed to look like, which React sees these changes and handles what and how changes to get to the desired UI.
This is all built in JavaScript with the help of JSX. As we remember in the first parts of the course, writing React with JSX is not a valid way to actually run JS in the browser, because the browser does not understand JSX - it must be *transpiled* using Babel into a more browser-friendly JS-only document.

Furthermore, our React "project" is divided into different files, modules, folders, we might have additional static image, font assets, etc.
Overall, getting a React project to link all these seperate files and dependencies, getting it transpiled and put into a single file is the process of **bundling**. 

Webpack is a tool that functions as a bundler, and it's used under-the-hood in both `npm run build` and `npm run start` scripts. Essentially, it runs to build a set of workable, runnable files from all the various modules that we define in the React project, because that's the only way we can "run" our code in the browser.

> In fact, the webpack bundle creates 2 bundles:
> 1. CSS  (`main.<hash>.css`)
> 2. JavaScript (`main.<hash>.js`)

React uses a base HTML structure to "inject" DOM elements. Webpack uses the entry point file, `index.js` as the "root" of the JS bundle.

We can configure Webpack through the `webpack.config.js` file, in which we configure things like entry point files, where built files go, plugins and packages.

## Loaders
Webpack is technically a *javascript* bundler, it can only really bundle JavaScript-only files, meaning that we cannot bundle React projects written in JSX.

```js
const path = require('path')

const config = () => {
  return {
    entry: './src/index.js',
    output: {
      path: path.resolve(__dirname, 'build'),
      filename: 'main.js'
    },
    module: {      
	    rules: [        
		    {          
			    test: /\.js$/,          
			    loader: 'babel-loader',          
			    options: {            
				    presets: ['@babel/preset-react'],          
				},        
			},      
		],    
	}, 
	}
}

module.exports = config
```
> We need to manually tell Webpack (through this configuration file *example*) that we want to "pre-process" files using `babel-loader`
> - In this example, we set up "rules" for pre-processing by "selecting" files through test-strings (regex), all files that match will get loaded by `babel-loader`
> 	- All `.js` files

## `regenerator-runtime` + `core-js`
When our code uses `async/await`, the Babel package called `babel-polyfill` used to handle that kind of code, but is now deprecated, we need to include the two packages `regenerator-runtime` + `core-js` in order for our code to properly bundle.

## Babel Presets
the `babel-loader` loader for webpack is passed an option called "presets" which is very handy for us because it passes a preset specifically for React project code. We can additionally add the `@babel/preset-env` preset to transpile code into ES5.

## CSS Loading
As with the `.js` files, we need to define CSS file loaders like `style-loader` or `css-loader` to properly parse any linked CSS files into the CSS bundle.

- `mini-css-extract-plugin` creates per-JS-file CSS files.

## `webpack-dev-server`
This package makes it possible to *hot reload* any changes to our React code into the running server. Without this package, we would need to save, re-bundle and refresh served code in order to preview changes.
- In fact, this package makes it possible to live preview the code by hosting a development server. 
	- the way the bundle is created is by being created *in-memory*, so that it can really quickly re-bundle.

## Source Maps
Within the webpack configuration, we can specify a `devtool` called `source-map`. This creates a source map between the *source* files and the *bundled files* - this makes it INFINITELY easier to de-bug any runtime errors (uncaught errors) from the console, because the code it redirects us to is the original source files.

## Minifying & Build Modes
Webpack links all the modules and files, and processes them through loader modules defined in the webpack configuration. Not only does it allows us to transpile JSX to JS and links all dependencies to a single set of collated files, it also allows us to optimize the *file size*.

Webpack has 2 native modes, *production* or *development*. When we are developing and we would like to live-preview changes, we use the *development* mode that lets us have a smoother developer experience (DX) because it doesn't minify or obstruct code - because we are direct developing. *Production*, on the other hand, enables us to optimize the bundle size - it doesn't matter whether the source code is human-readable or not. 
> Also, there's a large difference in performance in dev vs. prod builds, since dev bundles focus on being verbose and performing additional calls in strict-mode, etc ... Performance in production builds is significantly better.

## Polyfills
Polyfills are implementations of functionality not typically supported in all runtimes. For example, *promises* in JS are supported everywhere *but* Internet Explorer - if this matters to your application, then you need to implement promises in a way that IE can support it.
- This is usually done through *polyfills*, which can be added through webpack/babel because when they see some functionality they can "replace" it using the provided polyfill you want to use.


# Notes for Webpack Documentation


## [HOME](http://webpack.github.io/docs/)

+ Plugins: Most of webpack is written using plugins.
+ Loaders for preprocessing files.
+ Code Splitting: Split into chunks, loaded on demand.
+ Development Tools: SourceUrls, SourceMaps, Debugging, development middleware,
  development server, automatic reloading.
+ Performance: async and caching, incremental compilation.
+ Supports AMD and CommonJS.
+ Optimizations: many ways to reduce output size, request caching.
+ Multiple Targets: web, WebWorkers, node.js.


## [GETTING STARTED: Motivation](http://webpack.github.io/docs/motivation.html)

All about the apps. Lots of client side code. Need organization. MODULES!

Classic `<script>` tags. Blegh. Globals conflicts. Order of loading. Resolving
dependencies is a nightmare. More dependencies, more problems. Doesn't support
an ecosystem of small, encapsulated, single-purpose modules very well.

CommonJS. Synchronous. `require('module')`, `exports.something = value`,
`module.exports = value`. Node.js. Very common. Simple. No parallel require.
Browserify. modules-webmake. wreq.

AMD: Asynchronous Module Definition. Read and write no fun. Workaround.
require.js, curl.

ES6 Modules: `import "module"`, `export value`, `module value`. Native browser
support will be a while.

Webpack offers an unbiased solution.

Modules should be transferred from server to client and executed on client. We
want better control of how modules are transferred.

Webpack handles more than just javascript by converting other resources into
javascript modules: stylesheets, images, webfonts, html templates, coffeescript
less, sass, jade, i18n. Uses loaders.


## [GETTING STARTED: What is webpack?](http://webpack.github.io/docs/what-is-webpack.html)

Webpack is a module bundler. Converts modules with dependencies to static resources.

Existing bundlers not good for big projects.

Goals:

+ Code Splitting.
+ Low initial load time.
+ Static assets as modules.
+ 3rd party libs as modules.
+ Customize flexibility.
+ Big projects.

What makes webpack different?

+ Code Splitting.
+ Loaders are used to transform any kind of resource to a module.
+ Clever parser handles expressions in `require` and supports CommonJS and AMD.
+ Plugin System.


## [GETTING STARTED: Installation](http://webpack.github.io/docs/installation.html)

```shell
npm init
npm install --save-dev webpack
node_modules/.bin/webpack
```


## [GETTING STARTED: Usage](http://webpack.github.io/docs/usage.html)

WIP?! Wat?!

See CLI, node.js API, Configuration.


## GETTING STARTED: Require Modules

Nothing.


## GETTING STARTED: Vendor Modules

Nada.


## [GETTING STARTED: Using Loaders](http://webpack.github.io/docs/using-loaders.html)

> Loaders are transformations that are applied on a resource file of your app.
> They are functions (running in node.js) that take the source of a resource
> file are parameter and return new source.

Loader Features:

+ Loaders can be chained. Final loader expected to return javascript. Intermediary
loaders can return whatever you please.
+ Sync or Async.
+ All the power of node.js.
+ Loaders accept query params.
+ Loaders can be bound to file extensions.
+ Loaders installed through npm.
+ Modules can export loader?
+ Loaders have access to config.
+ Plugins can give loaders more features.
+ Loaders can emit arbitrary files.
+ And more.

There's more info about loaders and list of loaders in the webpack docs.

Loaders resolved similar to modules. Loader is expected to export a function in
node.js compatibile javascript. Loaders usually installed with npm, but you can
have custom loaders. Loaders can be references by full name or short name:
`json-loader`, `json`.

Use loaders through `require`, configuration, or CLI. Typically, configuration.

The `!` character is used to separate loaders in `require`: `require("style!css!less!bootstrap/less/bootstrap.less")`.

In configuration you can match file extension with regex.

Query params can be passed to loaders. Kind of weird looking but okay.

I'd go with this one, in config:

```json
{
    test: /\.png$/,
    loader: "url-loader"
    query: { mimetype: "image/png" }
}
```


## [GETTING STARTED: Using Plugins](http://webpack.github.io/docs/using-plugins.html)

Use `plugins` property to include plugins?

There's a list of plugins.


## [GETTING STARTED: Dev Tools](http://webpack.github.io/docs/dev-tools.html)

WIP. `devtool` config. webpack-dev-server. webpack-dev-middleware.


## [TUTORIALS AND EXAMPLES: Getting Started](http://webpack.github.io/docs/tutorials/getting-started/)

[Completed tutorial](https://github.com/jehoshua02/webpack-tutorial).


## [TUTORIALS AND EXAMPLES: List of Tutorials](http://webpack.github.io/docs/list-of-tutorials.html)

Some chinese tutorial or something.

Tutorial for converting react-tutorial to webpack. Hot module replacement?


## [TUTORIALS AND EXAMPLES: examples](http://webpack.github.io/docs/examples.html)

Some examples to look at later.


## [GUIDES: CommonJs](http://webpack.github.io/docs/commonjs.html)

The CommonJS Group defined a module format. Each module executes in it's own
private scope and exposes only what it wants to to the "universe".

Use `require` to import. Use `module` to export.


## [GUIDES: AMD](http://webpack.github.io/docs/amd.html)

```javascript
// define a module
define('myModule', ['jquery'], function ($) {
  // blah blah
});

// use module
define(['myModule'], function (myModule) {
  // blah blah
});
```

In webpack a named module is only available locally. In require.js globally.

Can return a value for the module.


## [GUIDES: webpack for browserify users](http://webpack.github.io/docs/webpack-for-browserify-users.html)

webpack analyzes all `require()` calls, like browserify. The command is almost
the same.

Configure webpack with `webpack.config.js`. Don't forget `module.exports = {}`.

Use `path` property to output to different directory.

You can have multiple entry points.

Browserify uses transforms, webpack uses loaders.

`webpack --dev-tool inline-source-map` one of many commands for debugging.


## [GUIDES: Code Splitting](http://webpack.github.io/docs/code-splitting.html)

Big app not good to load all code at once. Split into "chunks" loaded on demand.
AKA "layers" (err buzzer; applications have layers and it's not the same thing).
"rollups" (wat?). "fragments" (huh?).

Define "split points". Webpack takes care of dependencies, output and runtime.

CommonJS: `require.ensure(dependencies, callback)`. Looks like AMD.

AMD: `require(dependencies, callback)`.

Chunk content: all dependencies at split point go into new chunk. Dependencies
recursively added. Anything `require`ed in `callback` is also added to chunk.

Some stuff about chunk optimization?

Chunk loading: depends on `target` config, runtime logic, `web` target chunks
load via jsonp. Chunks only loaded once. Parallel requests merged into one.
Runtime checks if loaded chunks fulfill multiple chunks?

Entry chunk: runtime + modules. Waits for chunk with module `0` and executes.

Normal chunk: no runtime. Structure depends on loading algo. jsonp callback for
jsonp algo. Contains list of chunk ids.

Initial chunk, non entry: normal chunk. More important.

App code and vendor code can be split.

Multiple entry chunks possible. But should only be one runtime on a page?

`CommonChunksPlugin` mentioned several times, but still uncertain what it
actually does. Runtime moved to commons chunk. Entry points in initial chunks.
Only one entry chunk loaded, multiple initial chunks. Multiple entry points in
single page? Modules in multiple entry chunks and runtime moved to common chunk.
Old entry chunks become initial chunks.

Chunk plugins: `LimitChunkCountPlugin`, `MinChunkSizePlugin`,
`AggressiveMergingPlugin`.

`require.ensure` accepts 3rd param, string, same string, same chunk.

`require.include(request)`: webpack specific, adds module to current chunk,
doesn't evaluate, statement removed from bundle? Useful if module is in
multiple child chunks? blah blah blah, wat?

You gotta be really smart or really bored to learn this stuff.

This feels a lot like overkill when all I want is ...

```javascript
var hello = require('world');

console.log(hello('everybody'));
```

Just want a way to encapsulate my javascript and insulate it from the cruel and
harsh universe.

But ... meh. I'll go along with it.

Let's just ... skim the rest of the guides and get to the real stuff.


## [GUIDES: Stylesheets](http://webpack.github.io/docs/stylesheets.html)

`style-loader` + `css-loader` = embedded stylesheets.

In `webpack.config.js`:

```javascript
{
    // ...
    module: {
        loaders: [
            { test: /\.css$/, loader: "style-loader!css-loader" }
        ]
    }
}
```

In your module:

```javascript
require('./stylesheet.css')
```

Will add a `<style>` tag with the css.

Watch out: order of execution!

Code splitting can be used to create one css file per initial chunk and embed
stylesheets into additional chunks or create one css file for the complete
bundle.

I don't get the code splitting stuff. Someone is going to have to explain it to
me in english.


## [GUIDES: Optimization](http://webpack.github.io/docs/optimization.html)

Minimize.

`new webpack.optimize.UglifyJsPlugin()`.

Smallest id length? `new webpack.optimize.OccurenceOrderPlugin()`?

`new webpack.optimize.DedupePlugin()`?

> The feature add some overhead to the entry chunk.

English second language? Drunk?

More code splitting stuff?


## [GUIDES: Multiple entry points](http://webpack.github.io/docs/multiple-entry-points.html)

Multiple entry points. I'll come back and read when I need to do that.


## [GUIDES: Library and externals](http://webpack.github.io/docs/library-and-externals.html)

+ `output.library`: name for library. Used as global var.
+ `output.libraryTarget`: specify kind of output. CJS, AMD, UMD.
+ `externals`: maps modules to globals (`require('jquery')` returns global `jQuery`).

Can make global: `library: "Foo", libraryTarget: "var"`.


## [GUIDES: Shimming modules](http://webpack.github.io/docs/shimming-modules.html)

__TO BE CONTINUED__

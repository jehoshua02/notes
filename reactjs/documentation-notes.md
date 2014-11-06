# Documentation Notes

__Quick Start__

+ [Getting Started](#quick-start-getting-started)
+ [Tutorial](#quick-start-tutorial)
+ [Thinking in React](#quick-start-thinking-in-react)

__Community Resources__

+ [Videos (Talks, Interviews, etc)](#community-resources-videos-talks-interviews-etc)

__Guides__

+ [Why React?](#guides-why-react)
+ [Displaying Data](#guides-displaying-data)
+ [Displaying Data: JSX in Depth](#guides-displaying-data-jsx-in-depth)
+ [Displaying Data: JSX Spread Attributes](#guides-displaying-data-jsx-spread-attributes)
+ [Displaying Data: JSX Gotchas](#guides-displaying-data-jsx-gotchas)
+ [Interactivity and Dynamic UIs](#guides-interactivity-and-dynamic-uis)
+ [Multiple Components](#guides-multiple-components)
+ [Reusable Components](#guides-reusable-components)
+ [Transferring Props](#guides-transferring-props)
+ [Forms](#guides-forms)
+ [Working With the Browser](#guides-working-with-the-browser)
+ [Working With the Browser: More About Refs](#guides-working-with-the-browser-more-about-refs)
+ [Tooling Integration](#guides-tooling-integration)
+ [Add-Ons](#guides-add-ons)
+ [Add-Ons: Animation](#guides-add-ons-animation)
+ [Add-Ons: Two-Way Binding Helpers](#guides-add-ons-two-way-binding-helpers)
+ [Add-Ons: Class Name Manipulation](#guides-add-ons-class-name-manipulation)
+ [Add-Ons: Test Utilities](#guides-add-ons-test-utilities)
+ [Add-Ons: Cloning Components](#guides-add-ons-cloning-components)
+ [Add-Ons: Immutability Helpers](#guides-add-ons-immutability-helpers)
+ [Add-Ons: PureRenderMixin](#guides-add-ons-purerendermixin)
+ [Add-Ons: Performance Tools](#guides-add-ons-performance-tools)

__Reference__

+ [Top-Level API](#reference-top-level-api)
+ [Component API](#reference-component-api)
+ [Component Specs and Lifecycle](#reference-component-specs-and-lifecycle)
+ [Supported Tags and Attributes](#reference-supported-tags-and-attributes)
+ [Event System](#reference-event-system)
+ [DOM Differences](#reference-dom-differences)
+ [Special Non-DOM Attributes](#reference-special-non-dom-attributes)
+ [Reconciliation](#reference-reconciliation)
+ [React (Virtual) DOM Terminology](#reference-react-virtual-dom-terminology)

__Flux__

+ [Overview](#flux-overview)
+ [TodoMVC Tutorial](#flux-todomvc-tutorial)

__Tips__

+ [Introduction](#tips-introduction)
+ [Inline Styles](#tips-inline-styles)
+ [If-Else in JSX](#tips-if-else-in-jsx)
+ [Self-Closing Tag](#tips-self-closing-tag)
+ [Maximum Number of JSX Root Nodes](#tips-maximum-number-of-jsx-root-nodes)
+ [Shorthand for Specifying Pixel Values in style props](#tips-shorthand-for-specifying-pixel-values-in-style-props)
+ [Type of the Children props](#tips-type-of-the-children-props)
+ [Value of null for Controlled Input](#tips-value-of-null-for-controlled-input)
+ [componentWillReceiveProps Not Triggered After Mounting](#tips-componentwillreceiveprops-not-triggered-after-mounting)
+ [Props in getInitialState Is an Anti-Pattern](#tips-props-in-getinitialstate-is-an-anti-pattern)
+ [DOM Event Listeners in a Component](#tips-dom-event-listeners-in-a-component)
+ [Load Initial Data via AJAX](#tips-load-initial-data-via-ajax)
+ [False in JSX](#tips-false-in-jsx)
+ [Communicate Between Components](#tips-communicate-between-components)
+ [Expose Component Functions](#tips-expose-component-functions)
+ [References to Components](#tips-references-to-components)
+ [this.props.children undefined](#tips-thispropschildren-undefined)

__Other__

+ [Questions:](#questions)
+ [TODO for these notes:](#todo-for-these-notes)


## [Quick Start: Getting Started](http://facebook.github.io/react/docs/getting-started.html)

+ React uses jsx syntax, an XML enhanced form of javascript.
+ Attach jsx file with `<script type="text/jsx" src="..."></script>`.
+ React comes with JSXTransformer.js, which converts jsx to javascript.
+ JSX tags are converted to javascript function calls that instantiate react components.
+ JSX can also be tranformed offline.
+ Use react npm package for use with browserify, webpack, etc.


## [Quick Start: Tutorial](http://facebook.github.io/react/docs/tutorial.html)

+ Define a component with `React.createClass(object)`.
+ A component must have a `render` method that returns a component tree.
+ Render a component with `React.render(component, containerElement)`.
+ Composability is a key tenet of maintainable frontends.
+ React has a set of components that parallel the entire HTML element set.
+ Props can be passed to child elements: `<Comment author="Pete Hunt">`.
+ Props values can be rendered: `<h2>{this.props.author}</h2>`.
+ Anything between a component tags is accessed with `this.props.children`.
+ Any kind of javascript can be rendered inside `{}` expression in render component tree.
+ Any data can be passed as a prop in `React.render()` or in a component `render` method.
+ Props are immutable, owned by the parent.
+ State is used for interaction and is mutable.
+ State is private to the component.
+ Modify state by calling `this.setState(state)`.
+ The component's `render` method should not modify state.
+ A component's initial state is set by defining `getInitialState` method. It is called once.
+ The component's `componentDidMount` method is called when the component is rendered and inserted
into the DOM.
+ The components `getDOMNode()` method returns the component's DOM element (same type returned
as jQuery's `.get(0)`).
+ The `ref` prop on child allows parent to reference with `this.refs.<ref_name>`.
+ Events attached just like props, following camelCase naming convention.
+ Parent can pass a callback as prop to the child so the child can pass data back up to parent by
calling the callback.


## [Quick Start: Thinking in React](http://facebook.github.io/react/docs/thinking-in-react.html)

1. Start with a mock.
2. Break the UI into a component hierarchy.
  + Identify and name the top level component.
  + Identify and name each component and it's sub-components recursively.
3. Build a static version in React.
  + Top-down for small projects. Bottom-up for larger projects.
  + No state. No interactivity. No thinking.
  + Use Props. Lots of typing.
  + Top level component recieves data model.
  + Modify data and call `React.render()` again to see change.
4. Identify the minimal (but complete) representation of UI state.
  + State is for interactivity.
  + Lots of thinking. Little typing.
  + Find minimal set of mutable state.
  + Computed values don't belong in state: `count` vs `items.length`.
  + Think of all pieces of data in application. Figure out which are state.
  + Three questions:
    1. Is it passed in from a parent via props? If so, it probably isn't state.
    2. Does it change over time? If not, it probably isn't state.
    3. Can you compute it based on any other state or props in your component? If so, it's not state.
5. Identify where your state should live.
  + Figure out which component mutates, or owns, each piece of state.
  + React is all about one-way data flow down the component hierarchy.
  + Be careful. It's not always immediately clear which component should own what state.
  + For each piece of state:
    1. Identify every component that renders something based on that state.
    2. Find a common owner component (a single component above all the components that need the state
    in the hierarchy).
    3. Either the common owner or another component higher up in the hierarchy should own the state.
    4. If you can't find a component to hold the state, make one.
6. Add inverse data flow.
  + `ReactLink` is an addon that allows two-way binding.
  + Components should only update their own state.
  + Parent can pass callback that modifies its own state to child.


## [Community Resources: Videos (Talks, Interviews, etc)](http://facebook.github.io/react/docs/videos.html)

+ [ ] Rethinking best practices - JSConf.eu
+ [ ] Thinking in react - tagtree.tv
+ [ ] Secrets of the Virtual DOM - MtnWest JS
+ [ ] Going big with React
+ [ ] CodeWinds
+ [ ] Javascript Jabber
+ [ ] Introduction to React.js - Facebook Seattle
+ [ ] Developing User Interfaces With React - Super VanJS
+ [ ] Introduction to React - LAWebSpeed meetup
+ [ ] React, or how to make life simpler - FrontEnd Dev Conf '14
+ [ ] "Functional DOM programming" - Meteor DevShop 11
+ [ ] "Rethinking Web App Development at Facebook" - Facebook F8 Conference 2014
+ [ ] React and Flux: Building Applications with a Unidirectional Data Flow - Forward JS 2014


## [Guides: Why React?](http://facebook.github.io/react/docs/why-react.html)

+ React is for creating user interfaces.
+ React built to solve one problem: bulding large applications with data that changes over time.
+ React solves this problem by being 1) Simple and 2) Declarative.
+ React is all about building reusable components.
+ The only thing React is for is building encapsulated, reusable, testable components.
+ React has been used to build thousands of components inside and outside Facebook and Instagram.


## [Guides: Displaying Data](http://facebook.github.io/react/docs/displaying-data.html)

+ React makes it easy to display data and automatically keeps the interface up-to-date when data changes.
+ `React.render` can be called again and again to forcibly rerender component.
+ React intelligently tries to update the UI in a non-destructive way.
+ React uses fast, internal mock DOM to perform diffs and computes the most efficient DOM mutation for you.
+ Never write to `this.props`.
+ A react component is simple: input `props` and `state` and outputs html.
+ React components must have a single root node.
+ Markup and the code that generates it are intimately tied together.
+ JSX gives you the full power of javascript within the templates.
+ Don't use `JSXTransformer` in production. Precompile using react-tools.
+ JSX is optional though highly recommended.


## [Guides: Displaying Data: JSX in Depth](http://facebook.github.io/react/docs/jsx-in-depth.html)

+ Use lower-case tag names for HTML elements.
+ Component tag names are UpperCamelCase.
+ `class` and `for` are javascript keywords. So `className` and `htmlFor` are used.
+ The component tag name must correspond with an in scope variable.
+ There is an HTML to JSX converter.
+ JSX expression evaluates to ReactElement.
+ Javascript expressions can be embedded in JSX with `{}`.
+ Do not wrap javascript expressions for attribute values with quotes.
+ You can put comments in JSX but it's ugly.


## [Guides: Displaying Data: JSX Spread Attributes](http://facebook.github.io/react/docs/jsx-spread.html)

+ Props look like HTML attributes.
+ Adding props after component instantiation is bad. They should be treated as immutable.
+ Props can be spread, like jam on bread: `<Bread {...jam} />`.
+ `...` operator is supported for arrays in ES6 and ES7 has proposal for Object Rest and Spread properties.
+ Use JSX command-line tool with `--harmony` to activate experimental ES7 syntax.


## [Guides: Displaying Data: JSX Gotchas](http://facebook.github.io/react/docs/jsx-gotchas.html)

+ HTML entities can be inserted within literal text: `<div>First &middot; Second</div>`.
+ Entities in dynamic content will be double escaped. React escapes strings to prevent XSS attacks.
+ `<div>{'First &middot; Second'}</div>` displays "First &middot; Second".
+ Workaround 1: write unicode character directly in Javascript.
+ Workaround 2: `\u00b7` or `String.fromCharCode(183)`.
+ Workaround 3: Arrays with strings and JSX elements.
+ Last Resort: `<div dangerouslySetInnerHTML={{__html: 'First &middot; Second'}} />`.
+ Only HTML spec, `data-`, and `aria-` properties are rendered in HTML.


## [Guides: Interactivity and Dynamic UIs](http://facebook.github.io/react/docs/interactivity-and-dynamic-uis.html)

+ Events handlers are passed as lowerCamelCase props.
+ React ensures that all events behave identically in IE8 and above.
+ React knows how to bubble and capture events according to the spec.
+ Events passed to your event handler are guaranteed to be consistent with W3C spec.
+ Enable touch events with `React.initializeTouchEvents(true);`.
+ Autobinding: `this` refers to component in all component methods.
+ Event delegation: listens for events at top level.
+ React thinks of UIs as simple state machines.
+ Update component state, React takes care of DOM.
+ `setState(data, callback)`: merges `data` into `this.state` and re-renders component. After render
optional `callback` is called. Not sure when to use `callback`.
+ Most of the time use props. Sometimes (user input, server request, time) use state.
+ Minimize and isolate state to it's most logical place.
+ Pattern: stateless components, single stateful component above them, passing state to children as props.
+ Stateful component encapsulates interaction logic.
+ Stateless components take care of rendering.
+ Data changed by event handlers to trigger UI update goes in state.
+ Computed data and react components do not belong in state.
+ Generally, props don't belong it state.
+ Prop is source of truth. Store in state if you need to know previous prop value.


## [Guides: Multiple Components](http://facebook.github.io/react/docs/multiple-components.html)

+ Composability is one of React's finest features.
+ React helps achieve true separation of concerns: allow you to separate concerns of your app
however you please, expressing UI in way that best fits domain.
+ Owner sets props of other components.
+ Component cannot mutate it's `props`. Owner controls props.
+ owner-ownee !== parent-child.
+ Just because it is parent, doesn't mean it is owner.
+ The owner of a component is the one who instantiates the component.
+ Child reconciliation: process of updating the DOM.
+ Two paragraphs, rather than destroying first, it is updated to match second and second is destroyed.
+ Hide rather than destroy if state needs to live across render passes.
+ Use `key` prop on children that get shuffled around, to preserve state and identity across render
passes.
+ Set `key` on component, not root element of component.
+ Children can be keyed by passing object. Use non-numeric keys to preserve ordering (add string
prefix if necessary).
+ Data flows from owner to owned through `props`. This is effectively one-way data binding.
+ React is already fast, but if you need faster, override `shouldComponentUpdate()` to skip subtree.
+ Be careful with `shouldComponentUpdate()` that it returns `false` only when it should.


## [Guides: Reusable Components](http://facebook.github.io/react/docs/reusable-components.html)

+ Common design elements should be reusable components with well-defined interfaces.
+ Validate props with `propTypes`: a hash defining types for all props.
+ `React.PropTypes` has a bunch of validators.
+ Override `getDefaultProps` to set defaults for props.
+ Pass props to a child using spread: `<a {...this.props}>blah blah</a>`. Good when extending
components in small ways.
+ Use `React.PropTypes.component` to specify only one child is allowed: `children: React.PropTypes.component.isRequired`.
+ Cross-cutting concerns: two very different components share common functionality.
+ Cross-cutting concern example: setInterval.
+ Use mixins for cross-cutting concerns.
+ Use lifecycle methods for cleanup.
+ Mixin methods do not override the same method defined in another mixin.
+ All mixin methods will be called in order listed, followed by method on component.


## [Guides: Transferring Props](http://facebook.github.io/react/docs/transferring-props.html)

+ Unless you have good reason, explicitly passing props one by one (manual transfer).
+ When it gets fragile and tedious, use destructuring assignment and spread operator to extract the
props you want and put the rest in an array: `var { checked, ...other} = this.props`.
+ Do your thing with your props, then pass the rest: `<div {...other} />`.
+ Be careful not to pass props by accident (It's good to avoid accidents in all code, even if they
seem good).
+ Always use destructuring pattern when transferring unknown `other` props. Otherwise you might pass
something you don't want to pass.
+ Repass used props explicitly.
+ Order of props matters. Last wins: good = `{...other} type="checkbox"`, bad = `type="checkbox" {...other}`.
+ I'm guessing "rest" means "gimme the rest", as in this destructuring expression:
`var { x, y, ...other } = { x: 1, y: 2, a: 3, b: 4 }`.
+ And "spread" means "spread them out", like this: `<Bread {...butter} />`.
+ So it's the same operator `...props`, but it's called "rest" in destructing expression, but
"spread" when being passed?
+ Rest, spread and destructuring are experimental JSX/ES7 features.
+ Requires `--harmony` flag with command-line tool to enable experimental ES7 syntax.
+ If not using JSX, you can use underscore `_.omit` and `_.extend` to destructure, rest, and spread.


## [Guides: Forms](http://facebook.github.io/react/docs/forms.html)

+ Form components: `<input>`, `<textarea>`, `<option>`.
+ `value` prop supported by `<input>`, `<textarea>` components.
+ `checked` prop supported by `<input>` components of type `checkbox` or `radio`.
+ `selected` prop supported by `<option>` components.
+ Use `value` prop on `<textarea>` instead of children.
+ Form components support `onChange` prop.
+ `onChange` fires when
  + `value` of `<input>` or `<textarea>` changes.
  + `checked` state of `<input>` changes.
  + `selected` state of `<option>` changes.
+ `onChange` supported on all native components and bubble up, like all DOM events.
+ Controlled Components: can't change value because it's set by prop. Good for live response or
validation. Without setting state in `onChange` it will not change.
+ Uncontrolled Components: value starts empty. Set defaults with `defaultValue` or `defaultChecked`.
+ Controlled Components are a side effect of declarative UI.
+ Multi-select: `<select multiple={true} value={['B', 'C']}>`.


## [Guides: Working With the Browser](http://facebook.github.io/react/docs/working-with-the-browser.html)

+ Virtual DOM: fast in-memory representation of the DOM.
+ React diffs `render` description with virtual DOM to compute the fastest way to update the DOM.
+ Sometimes you want to interact with DOM anyway. Use `refs` and `getDOMNode()`.
+ Exception thrown when calling `getDOMNode()` before component is mounted.
+ Component Lifecycle, three main parts: Mounting, Updating, Unmounting.
+ Mounting: insert into DOM.
+ Updating: re-rendered to determine if the DOM should be updated.
+ Unmounting: remove from the DOM.
+ will and did lifecycle methods.
+ `getInitialState()` is called before a component is mounted.
+ `componentWillMount()` is invoked immediately before mounting occurs.
+ `componentDidMount()` invoked after mounting. Initialization requiring DOM nodes goes here.
+ `componentWillReceiveProps()` invoked when mounted component receives new props. Used to compare
`this.props` and `nextProps`.
+ `shouldComponentUpdate()` invoked when a component decides changes warrant DOM update. Return
`false` to skip updating.
+ `componentWillUpdate()` invoked before updating occurs. Cannot call `this.setState()` here.
+ `componentDidUpdate()` invoked after updating.
+ `componentWillUnmount()` invoked before component unmount and destroyed. Clean up goes here.
+ Mounted composite component methods: `getDOMNode()`, `forceUpdate()`.
+ You need [es5-shim](https://github.com/kriskowal/es5-shim) to support older browsers.
+ React uses the following from `es5-shim.js`:
  + `Array.isArray`
  + `Array.prototype.every`
  + `Array.prototype.forEach`
  + `Array.prototype.indexOf`
  + `Array.prototype.map`
  + `Date.now`
  + `Function.prototype.bind`
  + `Object.keys`
  + `String.prototype.split`
  + `String.prototype.trim`
+ React uses the following from `es5-sham.js`:
  + `Object.create`
  + `Object.freeze`
+ Unminified build of React needs [paulmillr's console-polyfill](https://github.com/paulmillr/console-polyfill):
  + `console.*`
+ If using HTML5 elements in IE8 you'll need `html5shiv`.
+ React developers couldn't find a workaround for `onScroll` event.


## [Guides: Working With the Browser: More About Refs](http://facebook.github.io/react/docs/more-about-refs.html)

+ What is returned from `render()` is not the actual components. Just description.
+ Never hold on to something from `render()` and expect it to be meaningful.
+ The `ref` prop is a special prop that allows the parent to access the child through `this.refs`.
+ Only use `ref` when you can't use reactive `props` or `state`.
+ Since the ref is the component instance, any of the component methods may be called.
+ Use refs for DOM measurements.
+ Get the DOM node like this: `this.refs.myInput.getDOMNode()`.
+ Do not access refs inside `render`.
+ Never access as a property what was specified as a string: good `this.refs['myRefString']`; bad `this.refs.myRefString`.
+ Double check that state is owned by the right components before using refs.


## [Guides: Tooling Integration](http://facebook.github.io/react/docs/tooling-integration.html)

+ "Every project uses a different system for building and deploying JavaScript". That's too bad.
Why can't we unify?
+ CDN hosted version of React exports `React` global and works with CommonJS and AMD.
+ Building from master provides tree of CommonJS modules.
+ `npm install -g react-tools; jsx --watch src/ build/` (But I'd use `gulp-react` instead, which uses `react-tools`.)


## [Guides: Add-Ons](http://facebook.github.io/react/docs/addons.html)

+ `React.addons`, experimental, eventually rolled into core or blessed utilities lib.
+ `TransitionGroup`, `CSSTransitionGroup`, `LinkedStateMixin`, `classSet`, `TestUtils`,
`cloneWithProps`, `update`.
+ Unminified, development: `PureRenderMixin`, `Perf`.
+ To enable addons, use `react-with-addons.js` instead of `react.js`.
+ With npm, `require('react/addons')` instead of `require('react')`.


## [Guides: Add-Ons: Animation](http://facebook.github.io/react/docs/animation.html)

+ Wrap components to animate in `ReactCSSTransitionGroup`.
+ `ReactCSSTransitionGroup` is based on, interface to, `ReactTransitions`.
+ All animated children should have `key` prop.
+ Components entering `ReactCSSTransitionGroup` get an `*-enter` class, and `*-enter-active` a tick later.
+ Class names are based on `transitionName` prop on `ReactCSSTransitionGroup`.
+ Use classes for CSS animation or transition.
+ `ReactCSSTransitionGroup` keeps elements on DOM until animation completes.
+ `ReactCSSTransitionGroup` must be mounted before animated items to work.
+ `ReactCSSTransitionGroup` can work with one or zero items.
+ Use `transitionEnter={false}` or `transitionLeave={false}` to disable transitions.
+ `ReactCSSTransitionGroup` provides no way to notify components. `ReactTransitionGroup` provides
hooks for custom transitions.
+ `ReactTransitionGroup` provides the following lifecycle hooks:
  + `componentWillEnter(callbacks)`
    + Called same time as `componentDidMount` for components added to existing `TransitionGroup`.
    + Blocks other animations until `callback` is called.
    + Not called on initial render of `TransitionGroup`.
  + `componentDidEnter()`
    + Called after the `componentWillEnter` callback.
  + `componentWillLeave(callback)`
    + Called when child is removed from `ReactTransitionGroup`.
    + Kept in DOM until `callback` is called.
  + `componentDidLeave()`
    + Called when `willLeave` callback is called, same time as `componentWillUnmount`.
+ `ReactTransitionGroup` renders as `span` by default. Pass string in `component` prop to override.
+ The `component` prop for `ReactTransitionGroup` can be any component.


## [Guides: Add-Ons: Two-Way Binding Helpers](http://facebook.github.io/react/docs/two-way-binding-helpers.html)

+ Implement two-way bindings with `ReactLink`.
+ `ReactLink` should be used cautiously.
+ Closing the data flow loop explicitly leads to easy maintenance and understandability.
+ Two-way binding: implicitly enforcing that some value is always consistent with some state.
+ `ReactLink` is used to form links from data source to `state`.
+ `ReactLink` is just a wrapper and convention around `onChange` / `setState()` pattern.
+ Without `ReactLink` you listen to `onChange` and then `setState()`.
+ With `ReactLink`: `mixins: [React.addons.LinkedStateMixin]` and `<input valueLink={this.linkState('someStateKey')} />`.
+ `LinkedStateMixin` adds `linkState()` method.
+ `linkState()` returns `ReactLink`.
+ `ReactLink` contains current value of state and a callback to change it.
+ `ReactLink` objects can be passed up and down the tree as props.
+ `ReactLink` can be used to set up two-way binding through the component heirarchy.
+ Use `checkedLink` with checkboxes, instead of `valueLink`: `<input type="checkbox" checkedLink={this.linkState('booleanValue')} />`.
+ Two sides of `ReactLink`: a) creating instance and b) using it.
+ A `valueLink` is simply a hash with `value`, set using state, and `requestChange` handler.
+ The `valueLink` prop handles `onChange` and calls `this.props.valueLink.requestChange()`.
+ The `valueLink` prop uses `this.props.valueLink.value` instead of `this.props.value`.


## [Guides: Add-Ons: Class Name Manipulation](http://facebook.github.io/react/docs/class-name-manipulation.html)

+ Use `classSet()` to build DOM class string.
+ `classSet()` saves a lot of `if (condition) { classNames.push('someClass'); }`.
+ `React.addons.classSet({ 'someClass': condition, 'anotherClass': anotherCondition })`.
+ Receives hash object, class name as key, condition as value.


## [Guides: Add-Ons: Test Utilities](http://facebook.github.io/react/docs/test-utils.html)

+ Test utilities found in `React.addons.TestUtils`.
+ `React.addons.TestUtils` makes testing in any testing framework easy.
+ Facebook uses [Jest](http://facebook.github.io/jest/).
+ Utilities provided:
  + `Simulate`
  + `renderIntoDocument`
  + `mockComponent`
  + `isElementOfType`
  + `isDOMComponent`
  + `isCompositeComponent`
  + `isCompositeComponentWithType`
  + `isTextComponent`
  + `findAllInRenderedTree`
  + `scryRenderedDOMComponentsWithClass`
  + `findRenderedDOMComponentWithClass`
  + `scryRenderedDOMComponentsWithTag`
  + `findRenderedDOMComponentWithTag`
  + `scryRenderedComponentsWithType`
  + `findRenderedComponentWithType`


## [Guides: Add-Ons: Cloning Components](http://facebook.github.io/react/docs/clone-with-props.html)

+ Use `cloneWithProps` to add props to a component that you don't own (`this.props.children`).
+ Use `cloneWithProps` to make copies of a component.
+ `cloneWithProps(component, extraProps)`.
+ Does not transfer `key` or `ref` to the cloned component. Add to `extraProps` object.


## [Guides: Add-Ons: Immutability Helpers](http://facebook.github.io/react/docs/update.html)

+ Something about data, mutability, immutability, some `update()` helper that looks very strange to me.
+ I think you would use this in `shouldComponentUpdate()` to compare old data with new data. It's
more performant than `deepCopy()`, and easier to maintain than selective replacement.
+ `newData update(oldData, commands)`:

  ```javascript
  var newData = React.addons.update(myData, {
    x: {y: {z: {$set: 7}}},
    a: {b: {$push: [9]}}
  });
  ```
+ Available commands:
  + `{$push: array}`
  + `{$unshift: array}`
  + `{$splice: array of arrays}`
  + `{$set: any}`
  + `{$merge: object}`
  + `{$apply: function}`


## [Guides: Add-Ons: PureRenderMixin](http://facebook.github.io/react/docs/pure-render-mixin.html)

+ Use `PureRenderMixin` for performance boost when component render function is "pure".
+ "pure" render function returns same result given the same props and state.
+ Only use with components having shallow, simple props and state, or use `forceUpdate()` when you
know deep data has changed.
+ Child components should also be "pure".


## [Guides: Add-Ons: Performance Tools](http://facebook.github.io/react/docs/perf.html)

+ For performance increase, use `shouldComponentUpdate` to affect React's diff algorithm.
+ Use ReactPerf to figure out where to use `shouldComponentUpdate`.
+ `Reacts.addons.Perf` methods:
  + `start()` and `stop()`: Use to collect measurements.
  + `printInclusive(measurements)`: Use to display measurements.
  + `printExclusive(measurements)`: Excludes mount activities.
  + `printDOM(measurements)`: Shows DOM manipulations.
  + `getLastMeasurements()`: Raw json data for measurements.


## [Reference: Top-Level API](http://facebook.github.io/react/docs/top-level-api.html)

+ `React`
  + `React.createClass`
  + `React.render`
  + `React.unmountComponentAtNode`
  + `React.renderToString`
  + `React.renderToStaticMarkup`
  + `React.isValidElement`
  + `React.DOM`
  + `React.PropTypes`
  + `React.initializeTouchEvents`
  + `React.Children`
    + `React.Children.map`
    + `React.Children.forEach`
    + `React.Children.count`
    + `React.Children.only`


## [Reference: Component API](http://facebook.github.io/react/docs/component-api.html)

+ Component instances are created when rendering and reused in subsequent renders.
+ Component instances accessed with `this` inside Component, `refs`, or `React.render` return value.
+ `setState`: Merges into state. Triggers UI updates. Callback after re-render.
+ Treat `this.state` as immutable. Use `setState`.
+ `setState` does not immediately mutate state.
+ `replaceState`: It's in the name.
+ `forceUpdate`: Use to trigger `render()`. Don't use.
+ `getDOMNode`: Available after mount. Native DOM element.
+ `isMounted`: It's in the name.
+ `setProps`: Only available on root-level (component returned by `React.render()`). Just call `React.render()` instead.
+ `replaceProps`: It's in the name.


## [Reference: Component Specs and Lifecycle](http://facebook.github.io/react/docs/component-specs.html)

+ `React.createClass()` takes a "specification" object that must have a `render` method.
+ `render` should examine `this.props` and `this.state` and return a single child component.
+ `render` can return `null` or `false`, renders `<noscript>`. `this.getDOMNode()` returns `null`.
+ `render` method should be "pure" (does not modify state, or interact with the DOM/browser).
+ keeping `render` pure makes server render more practical.
+ `getInitialState`: Once before mount. Initial value of `this.state`.
+ `getDefaultProps`: Called once and cached on class creation. Values set on `this.props` unless parent overrides.
+ Do not use `this.props` in `getDefaultProps`.
+ Any complex objects in `getDefaultProps` are shared across instances, not copied.
+ `propTypes`: Used to validate props being passed in.
+ `mixins`: Use to share behavior among multiple components.
+ `statics`: Can be called before instantiation. No access to props or state except through passing as function param.
+ `displayName`: Used in debugging messages. JSX sets automatically.
+ Lifecycle Methods:
  + `componentWillMount`: Before initial rendering. `setState` will not trigger additional renders.
  + `componentDidMount`: After initial rendering. Can use `this.getDOMNode()`, `setTimeout`, `setInterval`.
  + `componentWillReceiveProps`: Invoked before receiving props. Not called for initial render. `setState` will not trigger additional render.
  + `shouldComponentUpdate`: Before rendering, except initial or `forceUpdate`. Return `false` to skip update and render.
  + `componentWillUpdate`: Before rendering, except initial. Prepare for update. Don't use `setState`.
  + `componentDidUpdate`: After update, except initial. Operate on DOM.
  + `componentWillUnmount`: Before unmounted from DOM. Cleanup timers, DOM, `componentDidMount`.


## [Reference: Supported Tags and Attributes](http://facebook.github.io/react/docs/tags-and-attributes.html)

__TODO__


## [Reference: Event System](http://facebook.github.io/react/docs/events.html)

__TODO__


## [Reference: DOM Differences](http://facebook.github.io/react/docs/dom-differences.html)

__TODO__


## [Reference: Special Non-DOM Attributes](http://facebook.github.io/react/docs/special-non-dom-attributes.html)

__TODO__


## [Reference: Reconciliation](http://facebook.github.io/react/docs/reconciliation.html)

__TODO__


## [Reference: React (Virtual) DOM Terminology](http://facebook.github.io/react/docs/glossary.html)

__TODO__


## [Flux: Overview](http://facebook.github.io/flux/docs/overview.html)

__TODO__


## [Flux: TodoMVC Tutorial](http://facebook.github.io/flux/docs/todo-list.html)

__TODO__


## [Tips: Introduction](http://facebook.github.io/react/tips/introduction.html)

__TODO__


## [Tips: Inline Styles](http://facebook.github.io/react/tips/inline-styles.html)

__TODO__


## [Tips: If-Else in JSX](http://facebook.github.io/react/tips/if-else-in-JSX.html)

__TODO__


## [Tips: Self-Closing Tag](http://facebook.github.io/react/tips/self-closing-tag.html)

__TODO__


## [Tips: Maximum Number of JSX Root Nodes](http://facebook.github.io/react/tips/maximum-number-of-jsx-root-nodes.html)

__TODO__


## [Tips: Shorthand for Specifying Pixel Values in style props](http://facebook.github.io/react/tips/style-props-value-px.html)

__TODO__


## [Tips: Type of the Children props](http://facebook.github.io/react/tips/children-props-type.html)

__TODO__


## [Tips: Value of null for Controlled Input](http://facebook.github.io/react/tips/controlled-input-null-value.html)

__TODO__


## [Tips: componentWillReceiveProps Not Triggered After Mounting](http://facebook.github.io/react/tips/componentWillReceiveProps-not-triggered-after-mounting.html)

__TODO__


## [Tips: Props in getInitialState Is an Anti-Pattern](http://facebook.github.io/react/tips/props-in-getInitialState-as-anti-pattern.html)

__TODO__


## [Tips: DOM Event Listeners in a Component](http://facebook.github.io/react/tips/dom-event-listeners.html)

__TODO__


## [Tips: Load Initial Data via AJAX](http://facebook.github.io/react/tips/initial-ajax.html)

__TODO__


## [Tips: False in JSX](http://facebook.github.io/react/tips/false-in-jsx.html)

__TODO__


## [Tips: Communicate Between Components](http://facebook.github.io/react/tips/communicate-between-components.html)

__TODO__


## [Tips: Expose Component Functions](http://facebook.github.io/react/tips/expose-component-functions.html)

__TODO__


## [Tips: References to Components](http://facebook.github.io/react/tips/references-to-components.html)

__TODO__


## [Tips: this.props.children undefined](http://facebook.github.io/react/tips/children-undefined.html)

__TODO__


## Questions:

+ What does `React.render()` do under the hood? I assume it calls the component's `render` method at
some point, but what else is happening?
+ What does `React.createClass()` do under the hood?
+ Where exactly is `componentDidMount` called?
+ What can I do in React that I can't do in jQuery?
+ How does React compare to Polymer?
+ How does React help build "big, fast" web apps?
+ What is a "simple state machine"?
+ How long have these addons been around and how long until they will be moved into core or utility lib?
+ How many lines of code are in react.js?
+ How many public, documented methods are in React api?
+ What is received by callbacks passed to `componentWillEnter` and `componentWillLeave` methods on `ReactTransitionGroup`?
+ What exactly should I pass to [`React.addons.TestUtils.mockComponent()`](http://facebook.github.io/react/docs/test-utils.html#mockcomponent)? What does `function componentClass` mean?
+ What exactly should I pass to [`React.addons.TestUtils.isElementOfType()`](http://facebook.github.io/react/docs/test-utils.html#iselementoftype)? What is a `ReactElement`?
What is `function componentClass`?
+ When would you want to make copies of a component (with `cloneWithProps`)?
+ Can somebody help me make sense of what the `update()` addon does, when/why/where to use it?
+ Will React DOM diff the initial content in the DOM element being rendered to?
+ What is a ReactElement and where do they come from?


## __TODO__ for these notes:

+ [ ] Eliminate all __TODO__ marks.
+ [ ] More questions.
+ [ ] Move questions to separate document and answer them.
+ [ ] Take notes on all videos, talks, interviews, etc.
+ [ ] Go through [Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)
+ [ ] Go through [Examples](https://github.com/facebook/react/wiki/Examples)

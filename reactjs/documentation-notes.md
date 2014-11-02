# Documentation Notes

## Quick Start: Getting Started

+ React uses jsx syntax, an XML enhanced form of javascript.
+ Attach jsx file with `<script type="text/jsx" src="..."></script>`.
+ React comes with JSXTransformer.js, which converts jsx to javascript.
+ JSX tags are converted to javascript function calls that instantiate react components.
+ JSX can also be tranformed offline.
+ Use react npm package for use with browserify, webpack, etc.


## Quick Start: Tutorial

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


## Quick Start: Thinking in React

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


## Community Resources: Videos (Talks, Interviews, etc)

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


## Guides: Why React?

+ React is for creating user interfaces.
+ React built to solve one problem: bulding large applications with data that changes over time.
+ React solves this problem by being 1) Simple and 2) Declarative.
+ React is all about building reusable components.
+ The only thing React is for is building encapsulated, reusable, testable components.
+ React has been used to build thousands of components inside and outside Facebook and Instagram.


## Guides: Displaying Data

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


## Guides: Displaying Data: JSX in Depth

+ Use lower-case tag names for HTML elements.
+ Component tag names are UpperCamelCase.
+ `class` and `for` are javascript keywords. So `className` and `htmlFor` are used.
+ The component tag name must correspond with an in scope variable.
+ There is an HTML to JSX converter.
+ JSX expression evaluates to ReactElement.
+ Javascript expressions can be embedded in JSX with `{}`.
+ Do not wrap javascript expressions for attribute values with quotes.
+ You can put comments in JSX but it's ugly.


## Guides: Displaying Data: JSX Spread Attributes

+ Props look like HTML attributes.
+ Adding props after component instantiation is bad. They should be treated as immutable.
+ Props can be spread, like jam on bread: `<Bread {...jam} />`.
+ `...` operator is supported for arrays in ES6 and ES7 has proposal for Object Rest and Spread properties.
+ Use JSX command-line tool with `--harmony` to activate experimental ES7 syntax.


## Guides: Displaying Data: JSX Gotchas

+ HTML entities can be inserted within literal text: `<div>First &middot; Second</div>`.
+ Entities in dynamic content will be double escaped. React escapes strings to prevent XSS attacks.
+ `<div>{'First &middot; Second'}</div>` displays "First &middot; Second".
+ Workaround 1: write unicode character directly in Javascript.
+ Workaround 2: `\u00b7` or `String.fromCharCode(183)`.
+ Workaround 3: Arrays with strings and JSX elements.
+ Last Resort: `<div dangerouslySetInnerHTML={{__html: 'First &middot; Second'}} />`.
+ Only HTML spec, `data-`, and `aria-` properties are rendered in HTML.


## Guides: Interactivity and Dynamic UIs

__TODO__


## Guides: Multiple Components

__TODO__


## Guides: Reusable Components

__TODO__


## Guides: Transferring Props

__TODO__


## Guides: Forms

__TODO__


## Guides: Working With the Browser

__TODO__


## Guides: Working With the Browser: More About Refs

__TODO__


## Guides: Tooling Integration

__TODO__


## Guides: Add-Ons

__TODO__


## Guides: Add-Ons: Animation

__TODO__


## Guides: Add-Ons: Two-Way Binding Helpers

__TODO__


## Guides: Add-Ons: Class Name Manipulation

__TODO__


## Guides: Add-Ons: Test Utilities

__TODO__


## Guides: Add-Ons: Cloning Components

__TODO__


## Guides: Add-Ons: Immutability Helpers

__TODO__


## Guides: Add-Ons: PureRenderMixin

__TODO__


## Guides: Add-Ons: Performance Tools

__TODO__


## Reference: Top-Level API

__TODO__


## Reference: Component API

__TODO__


## Reference: Component Specs and Lifecycle

__TODO__


## Reference: Supported Tags and Attributes

__TODO__


## Reference: Event System

__TODO__


## Reference: DOM Differences

__TODO__


## Reference: Special Non-DOM Attributes

__TODO__


## Reference: Reconciliation

__TODO__


## Reference: React (Virtual) DOM Terminology

__TODO__


## Flux: Overview

__TODO__


## Flux: TodoMVC Tutorial

__TODO__


## Tips: Introduction

__TODO__


## Tips: Inline Styles

__TODO__


## Tips: If-Else in JSX

__TODO__


## Tips: Self-Closing Tag

__TODO__


## Tips: Maximum Number of JSX Root Nodes

__TODO__


## Tips: Shorthand for Specifying Pixel Values in style props

__TODO__


## Tips: Type of the Children props

__TODO__


## Tips: Value of null for Controlled Input

__TODO__


## Tips: componentWillReceiveProps Not Triggered After Mounting

__TODO__


## Tips: Props in getInitialState Is an Anti-Pattern

__TODO__


## Tips: DOM Event Listeners in a Component

__TODO__


## Tips: Load Initial Data via AJAX

__TODO__


## Tips: False in JSX

__TODO__


## Tips: Communicate Between Components

__TODO__


## Tips: Expose Component Functions

__TODO__


## Tips: References to Components

__TODO__


## Tips: this.props.children undefined

__TODO__


## Questions:

+ What does `React.render()` do under the hood? I assume it calls the component's `render` method at
some point, but what else is happening?
+ What does `React.createClass()` do under the hood?
+ Where exactly is `componentDidMount` called?
+ What can I do in React that I can't do in jQuery?
+ How does React compare to Polymer?
+ How does React help build "big, fast" web apps?


## __TODO__ for these notes:

+ [ ] Add links.
+ [ ] Eliminate all __TODO__ marks.
+ [ ] More questions.
+ [ ] Move questions to separate document and answer them.
+ [ ] Take notes on all videos, talks, interviews, etc.
+ [ ] Go through [Complementary Tools](https://github.com/facebook/react/wiki/Complementary-Tools)
+ [ ] Go through [Examples](https://github.com/facebook/react/wiki/Examples)
+ [ ] Check markdown rendering on Github.

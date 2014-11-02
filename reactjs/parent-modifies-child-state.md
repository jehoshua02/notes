# Parent Modifies Child State

While building a `CollapsibleGroup` component, or "accordion", I wanted
to close all other `Collapsible` components when one is opened.

There are two parts to making this work:

1. Notify `CollapsibleGroup` when a `Collapsible` is opened.
2. Close all `Collapsible` components that are not the one just opened.

The first part was easy: pass a callback prop, `handleCollapsibleOpen`, to the `Collapsible` that
receives a reference of the `Collapsible` that was opened. The child then calls this callback
passing itself in as a parameter.

For the second part, since the `open` state is owned by the `Collapsible`, I needed a way to
manipulate the `Collapsible` state from the parent. For this I added a `ref` prop to each
`Collapsible` in `CollapsibleGroup` render. Then in `handleCollapsibleOpen` I close
other `Collapsible` components by looping over `this.refs`, and calling the `close` method I have
defined each `Collapsible`, which manipulates the `open` state.

Here's the code (some code omitted for brevity):

```jsx
var CollapsibleGroup = React.createClass({

  /* react hooks */

  render: function () {
    return (
      <div className="ddm-collapsible-group">
        {this.renderChildren()}
      </div>
    );
  },



  /* event handlers */

  handleCollapsibleOpen: function (collapsible) {
    this.closeOtherCollapsibles(collapsible);
  },



  /* methods */



  /* helpers */

  closeOtherCollapsibles: function (collapsible) {
    for (var key in this.refs) {
      var ref = this.refs[key];
      var isCollapsible = ref.type !== Collapsible.type;
      var isSame = ref.props.index === collapsible.props.index;
      if (!isCollapsible || isSame) { continue; }
      ref.close();
    }
  },

  renderChildren: function () {
    return React.Children.map(this.props.children, this.renderChild);
  },

  renderChild: function (child, index) {
    if (child.type !== Collapsible.type) { return child; }

    child = React.addons.cloneWithProps(child, {
      index: index,
      onOpen: this.handleCollapsibleOpen,
      ref: 'ddmCollapsible' + index
    });

    return child;
  }

});
```

See Also:

+ [Parent Adds Props to Children](parent-adds-props-to-children.md)
+ [Expose Component Functions](http://facebook.github.io/react/tips/expose-component-functions.html)
+ [DDM Collapsible](https://github.com/deseretdigital-ui/ddm-collapsible) ([React Branch](https://github.com/deseretdigital-ui/ddm-collapsible/blob/react_collapsible/src/jsx/CollapsibleGroup.jsx))
+ [Cloning Components](http://facebook.github.io/react/docs/clone-with-props.html)
+ [Add-ons](http://facebook.github.io/react/docs/addons.html)
+ [React.Children](http://facebook.github.io/react/docs/top-level-api.html#react.children)
+ [Type of the Children props](http://facebook.github.io/react/tips/children-props-type.html)
+ [More About Refs](http://facebook.github.io/react/docs/more-about-refs.html)

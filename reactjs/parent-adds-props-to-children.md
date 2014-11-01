# Parent Adds Props to Children

I needed to add props to a child component, from within the parent, but the
parent didn't define the children.

<!-- more -->

I was working on the so-often-re-invented collapsible group, or "accordion",
as bootstrap calls it. To start here is what my render looks like:

```jsx
React.render(
  <CollapsibleGroup>
    <Collapsible>
      <CollapsibleHead>Collapsible 1</CollapsibleHead>
      <CollapsibleBody>
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
          <li>Item 4</li>
          <li>Item 5</li>
        </ul>
      </CollapsibleBody>
    </Collapsible>
    <Collapsible>
      <CollapsibleHead>Collapsible 2</CollapsibleHead>
      <CollapsibleBody>
        <ul>
          <li>Item 1</li>
          <li>Item 2</li>
          <li>Item 3</li>
          <li>Item 4</li>
          <li>Item 5</li>
        </ul>
      </CollapsibleBody>
    </Collapsible>
  </CollapsibleGroup>,
  document.getElementById('react-example-1')
);
```

The `CollapsibleGroup` will listen for when a `Collapsible` opens and then
close all other `Collapsible` instances. But the `open` state belongs to
the `Collapsible` and the `CollapsibleGroup` needs some way to affect that
state.

So I wanted to use the `ref` prop to give the parent `CollapsibleGroup` a
handle on each `Collapsible` child. In other words, I wanted the parent
to attach props to the children. In the `CollapsibleGroup` render method,
I used `React.addons.cloneWithProps(component, props)` to add the props to
each child (some code ommitted for brevity):

```jsx
var CollapsibleGroup = React.createClass({
  render: function () {
    return (
      <div className="ddm-collapsible-group">
        {this.renderChildren()}
      </div>
    );
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

+ [Cloning Components](http://facebook.github.io/react/docs/clone-with-props.html)
+ [Add-ons](http://facebook.github.io/react/docs/addons.html)
+ [React.Children](http://facebook.github.io/react/docs/top-level-api.html#react.children)
+ [Type of the Children props](http://facebook.github.io/react/tips/children-props-type.html)
+ [More About Refs](http://facebook.github.io/react/docs/more-about-refs.html)
+ [DDM Collapsible](https://github.com/deseretdigital-ui/ddm-collapsible) ([React Branch](https://github.com/deseretdigital-ui/ddm-collapsible/blob/react_collapsible/src/jsx/CollapsibleGroup.jsx))
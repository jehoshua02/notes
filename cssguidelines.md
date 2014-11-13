# CSS Guidelines Notes

## [Introduction](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#introduction)

Goals:

+ Keep stylesheets maintainable.
+ Keep code transparent, sane, and readable.
+ Keep stylesheets scalable.

Variety of techniques to satisfy goals.
CSS Guidelines documents these techniques.

There's a difference between coding styleguide and visual styleguide.

Guidelines are good for long lived projects, multiple projects, diverse development team.

Good guidelines will:

+ Set standard within a codebase.
+ Promote consistency across different codebases.
+ Give a familiar feeling across codebases.
+ Increase productivity.

CSS Guidelines is *a* styleguide. Not *the* styleguide.


## [Syntax and Formatting](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#syntax-and-formatting)

Clean code feels clean. It is pleasant to work with. And is easier to write clean code in.

Ugly code sets a bad precedent.

> an earlier event or action that is regarded as an example or guide to be considered in subsequent similar circumstances.

+ 4 space indents, no tabs.
+ 80 character wide lines.
+ Multi-line CSS.
+ Meaningful use of whitespace.

We want consistency more than we want to argue about specifics.

Split discrete chunks of code into separate files.

Reasons to keep lines 80 characters wide:

+ multiple files open side by side.
+ viewing CSS on Github or terminal windows.
+ comfortable line length for comments.

Exception examples:

+ urls
+ gradient syntax

Sections

```css
/*------------------------*\
  #SECTION-TITLE
\*------------------------*/

/**
 * Comment
 */

.selector {}
```

Hash makes searches easier.
Note the empty line between section heading and code.
Section preceded by 5 blank lines.

Ruleset anatomy:

```
[selector] {
  [property]: [value];
  [<--declaration-->]
}
```

Ruleset: Selector and rules.
Rule, Declaration: Property and value.

+ Space before open brace.
+ Rule all on one line. One rule per line. Rule on it's own line.
+ Space between property and value.
+ Opening brace on same line as last selector.
+ Rules indented.
+ Closing brace on new line.
+ Every rule has semi-colon.

Indent Sass when nesting.

Avoid nesting if possible.

Whitespace:

+ one empty line between related rulesets.
+ 2 empty lines between loosely related rulesets.
+ 5 empty lines between sections.

HTML:

+ Always double-quote attributes.
+ Use meaningful whitespace in HTML.



## [Commenting](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#commenting)

+ Comment anything that isn't immediately obvious from the code alone.
+ Document sections or components with docblock.
+ Comment on related pieces in separate files.
+ Use numbered lists to keep comments together and pinpoint what you are talking about.
+ For code in compile output, use comment that will appear in output: `/* */`.
+ For code that is not in compile output, use comment that one appear in compiled output: `//`.
+ Deploy without comments.


## [Naming Conventions](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#naming-conventions)

+ What does a class do?
+ Where can a class be used?
+ What else is it related to?

Use hyphen delimited strings. BEM-like naming for complex code.

Don't get caught up with BEM methodology. We just want naming convention.

+ Block: An independent component.
+ Element: Part of a block. An element might be *in* the block but not *of* the block.
+ Modifier: variant or extension of the block.

Block and element separated by two underscores: `.block__element`.
Modifiers are delimited by two hyphens: `.block--modifier`, `.block__element--modifier`, `block--modifier .block__element`.

Use Sass nesting to encapsulate all related styles for modifiers.

Classes that invoke javascript funtionality should be prefixed: `js-*`.

## [CSS Selectors](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#css-selectors)

SELECTOR INTENT!

> It is important when writing CSS that we scope our selectors correctly, and that we’re selecting
> the right things for the right reasons. Selector Intent is the process of deciding and defining
> what you want to style and how you will go about selecting it. For example, if you are wanting to
> style your website’s main navigation menu, a selector like this would be incredibly unwise:

Selector Intent: Select the right things for the right reasons.

Good selectors make up for the lack of encapsulation and leakiness of CSS.

> your selectors should be as explicit and well reasoned as your reason for wanting to select something.

Reusability:

> Everything you choose, from the type of selector to its name, should lend itself toward being reused.

Location/Context Independence and Portability:

Style things based on what they are not where they are. Think "Components".

> A component shouldn’t have to live in a certain place to look a certain way.

Even if a qualified selector is justified, you can still benefit from making a new class that can be reused.

Quasi-Qualified Selectors

```css
/*ul*/.nav {}
```

Pick names that are sensible and somewhat ambiguous to make way for high reusability.

Choose names that ease maintenance not perceived meaning?

Name things for people.

Strive for reusable, recyclable classes.

> Add any useful or specific meaning via a mechanism that will not inhibit your and your team’s ability to recycle and reuse CSS.

Selector performance:

+ long selectors are slower.
+ preprocessor nesting creates long selectors.
+ child selectors are more efficient: `>`.
+ browsers are fast and selector optimization is low priority.

Summary:

+ Select what you want explicitly. Selector specificity.
+ Write selectors for reusability. Reduce waste and repetition.
+ Do not nest selectors unnecessarily. Increases specificity and makes less reusable.
+ Do not qualify selectors unnecessarily. Limits reusability.
+ Keep selectors short as possible. Specificity and performance.


## [Specificity](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#specificity)

Oh the horror!

Specificity can:

+ Limit ability to extend and manipulate code.
+ Destroy CSS cascade.
+ Cause verbosity.
+ Break location independence.
+ Frustration.

Keep specificity as low as possible.

+ Don't use ids in css.
+ avoid nesting.
+ don't qualify classes.
+ avoid chaining.

> Specificity can be wrangled and understood, but it is safer just to avoid it entirely.

Do not use `!important` unless it is as a guarantee.

```css
.one-half {
  width: 50% !important;
}

.hidden {
  display: none !important;
}
```

Hacking Specificity:

Double specificity without introducing location dependency.

```css
.site-nav.site-nav {}
```

Whoa blows my mind!

Use id without the specificity:

```css
[id=hello] {}
```



## [Architectural Principles](https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#architectural-principles)

Developer's best tools:

+ Self-discipline
+ Conscientiousness
+ Diligence

A well-defined architecture will help enforce these.

Architecture: large, overarching, principle-led collections of smaller conventions which come
together to provide an environment in which code is written and maintained.

Good architecture:

+ Consistency.
+ Sanity.
+ Accomodate change.
+ Grow and Scale.
+ Promote reuse and efficiency.
+ Productivity.

Object-orientation:

Break it down. OOCSS. Nicole Sullivan. Media Object.

OOCSS: Structure and skin.

Structure: common, recurring frames, design-free, object and abstractions. No cosmetics.

Skin: Cosmetics.

```css
/**
 * A simple, design-free button object. Extend this object with a `.btn--*` skin
 * class.
 */
.btn {
    display: inline-block;
    padding: 1em 2em;
    vertical-align: middle;
}


/**
 * Positive buttons’ skin. Extends `.btn`.
 */
.btn--positive {
    background-color: green;
    color: white;
}

/**
 * Negative buttons’ skin. Extends `.btn`.
 */
.btn--negative {
    background-color: red;
    color: white;
}
```

Use multiple classes rather than `@extend`.

Single Responsibility Principle: Each class does one thing.

Open to extension, closed to modification.

DRY: duplication is better than the wrong abstraction.




## TODO

+ 2 space indents for HTML, Javascript, CSS. Easier to maintain. Used widely by front end developers. After using it for quite some time, I find it easier to read.
  Deep nesting is not uncommon for html. 2 spaces reduces horizontal distance quite a bit and also works better with 80 character line rule.
+ 80 character wide columns -> lines.
+ What is "multi-line css" mean?
+ Specifics are relevant. We just want consistency more than we want to argue about specifics. To get consistency, we must decide on specifics.
+ No table of contents.
+ Can we use separate files instead of sections?
+ One selector per line, newline after every comma in a selector.
+ Meh. Let's ditch single line ruleset for guideline simplicity and to avoid them being abused accidentally.
+ Meh. We don't need indentation. BEM class names are good enough. Indentation makes maintenance more difficult.
  If the concern is how the classes are used, put an html snippet in a comment.
+ Mixed feelings about alignment of related rules. https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#alignment
+ Single spaces in class attribute. Double? Wat? https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#html
+ Don't use brackets. Wat?
+ I think I'd move HTML guidelines out of CSS guidelines.
+ More structure for comments. It would be nice to be able to gather all comments and compile into a markdown file.
+ Fix sass nesting example BEM: https://github.com/deseretdigital-ui/CSS-Guidelines/blob/gh-pages/index.md#modifying-elements
+ Not sure I like Quasi-Qualified Selectors. Use docblocks and html snippets to show how classes are intended to be used.
+ Not sure I agree with "ambiguous" naming. Often our styles are not reusable without some heavy polishing.
  I'd prefer specific class names with messy styles than ambiguous class names with messy styles.
  No sense giving it a name ready for reuse when it's just going to get styles that can't be reused.
  This could make things more confusing because we see a class name that looks reusable but only find
  out it applies styles that don't make sense. Then again, maybe if we were to use reusable names, we
  would be more careful to make sure the styles are reusable, paying very careful attention to
  selector intent and being very "Reusability-Minded". I just feel like we should use more specific
  class names and reuse nothing by accident. And when we identify something we like to reuse, we pull
  it out, give it a good name, polish it up. That said, I agree with "Strive for reusable, recyclable classes".
+ `data-ui-component`? That's a little weird.
+ Why don't browsers read selectors left to right? Wouldn't that be more efficient than right to left?
+ Code review checklist or automation.
+ Study OOCSS.
+ The architecture stuff feels like it needs some work.

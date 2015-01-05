# Element Query Polyfills

My quest for the best element query polyfill.


## Searches

+ [Google: element query polyfill](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&espv=2&ie=UTF-8#q=element%20query%20polyfill)
  + [marcj/css-element-queries](https://github.com/marcj/css-element-queries)
    + Pros:
      + Install with bower.
      + Detects element resize, as opposed to window resize.
    + Cons:
      + Forces elements to be relative or absolute.
  + [tysonmatanich/elementQuery](https://github.com/tysonmatanich/elementQuery)
    + Doesn't seem to support element resize.
  + etc ...
+ [Bower: element queries](http://bower.io/search/?q=element%20queries)
  + [Snugug/eq.js](https://github.com/Snugug/eq.js)
    + stars: 339
    + updated: 6 days ago
  + [filaraujo/akyral-element-query](https://github.com/filaraujo/akyral-element-query)
    + stars: 4
    + updated: 2 months ago
    + Pros:
      + Detects element resize, as opposed to window resize.
    + Cons:
      + Polymer
  + [reusables/breakpoints.js](https://github.com/reusables/breakpoints.js)
    + Doesn't support element resize.
  + [BoomTownROI/boomqueries](https://github.com/BoomTownROI/boomqueries)
    + Doesn't seem to support element resize.
    + Implementation looks more complicated than reusables/breakpoints.js.
  + etc ...


## Most Promising

+ [marcj/css-element-queries](https://github.com/marcj/css-element-queries)
+ [filaraujo/akyral-element-query](https://github.com/filaraujo/akyral-element-query)

These two are the most promising because they detect when the element resizes
independent of the screen resize event so that if the element changes without
window resize it still works as one would desire.

Since [marcj/css-element-queries](https://github.com/marcj/css-element-queries)
does not depend on Polymer, I'd go with that.

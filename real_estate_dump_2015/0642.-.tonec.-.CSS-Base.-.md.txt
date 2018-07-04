
# CSS Bass

This is not a framework. This is a set of scss files and a directory structure that I developed whilst working on a recent project. I use it to provide myself with a starting point on new projects and reduce that initial setup time.

The benefits of it's structure include.
- *Adherance to Mobile First methodolody.* Global and mobile styles are served up first with css for larger screens served using media queries when the extra real estate becomes available.
- *No media query polyfill is needed for old IEs.* Old IEs are served up a fixed width stylesheet. Using the magic of scss and the creative use of conditional comments in the head of index.html, this is done without needing to update a separate IE only stylesheet.
- *The CSS is modular and 'componentized' - if that be a word!* The css is split into individual component which makes it easier to find and edit related styles across media query breakpoints.
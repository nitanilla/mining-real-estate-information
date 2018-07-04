# quickreturn.js

<img
  src="https://raw.githubusercontent.com/caiogondim/quickreturn.js/master/logo/logo.png"
  width="256"
  align="right"
/>

[Roman Nurik](https://plus.google.com/+RomanNurik/posts/1Sb549FvpJt):
> This is similar to Google Now's search box. It scrolls off-screen with the
> rest of the scrollable content, but upon scrolling slightly up at any point,
> it scrolls back into view. Quite a handy technique for search bars and the
> like.

[Android UI Patterns](http://www.androiduipatterns.com/2012/08/an-emerging-ui-pattern-quick-return.html):
> Quick Return UI design pattern (named by Roman Nurik on G+) is a screen real
> estate saving design pattern that still allows users to access important off
> screen controls by easily moving them back to the screen.


## Preview

![Preview](http://raw.github.com/caiogondim/quickreturn.js/master/preview.gif)


## Using

Grab the js file on `dist/quickreturn.min.js` and the source map on
`dist/quickreturn.min.js.map` and put in the public folder of your app.

Once the script is in your page, instantiate a new `Quickreturn` object passing
the DOM element you want to behave like a “quickreturn”.

```javascript
var menu = document.querySelector('.menu')
var quickReturn = new QuickReturn({el: menu})
```

The `new` method doesn't have any side-effect. To really initialize the
behavior, call `init`.

```javascript
quickReturn.init()
```

To destroy the quickreturn beahvior on the element, call the `destroy` method

```javascript
quickReturn.destroy()
```


## Browser Support

![Chrome](https://raw.github.com/alrra/browser-logos/master/chrome/chrome_48x48.png) | ![Firefox](https://raw.github.com/alrra/browser-logos/master/firefox/firefox_48x48.png) | ![IE](https://raw.github.com/alrra/browser-logos/master/internet-explorer/internet-explorer_48x48.png) | ![Opera](https://raw.github.com/alrra/browser-logos/master/opera/opera_48x48.png) | ![Safari](https://raw.github.com/alrra/browser-logos/master/safari/safari_48x48.png)
--- | --- | --- | --- | --- |
Latest ✔ | Latest ✔ | 9+ ✔ | Latest ✔ | 6.1+ ✔ |


## License
The MIT License (MIT)

Copyright (c) 2014 [Caio Gondim](http://caiogondim.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

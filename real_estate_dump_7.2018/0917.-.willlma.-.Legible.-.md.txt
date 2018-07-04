Legible is a Firefox extension that removes all fixed elements and prevents elements from scrolling to reduce distraction while reading in the browser and increases screen real-estate dedicated to the article/text.

Clicking the toolbar button again brings all hidden elements back.

If you simply want to install the extension, head over to the [addons page](https://addons.mozilla.org/en-US/firefox/addon/legible/).

In order to package the extension once you've made changes to it, you must have the Firefox Addon SDK [installed](https://developer.mozilla.org/en-US/Add-ons/SDK/Tutorials/Installation). Then you can use the [cfx tool](https://developer.mozilla.org/en-US/Add-ons/SDK/Tutorials/Getting_started) in the terminal to package and install the extension by running

    cfx xpi
    cfx run


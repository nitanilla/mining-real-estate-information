React-WinJS Responsive app
============

[View the live demo](http://jayrenn.github.io/react-winjs-demo/).

[View the instructions](https://github.com/jayrenn/react-winjs-demo/wiki/Instructions).

### Responsive design

This demo will showcase some of the options you, as the developer, have when using [React-WinJS](https://github.com/winjs/react-winjs), JavaScript, and CSS. When you resize your window, or view on different device sizes, the app will adjust its layout to best utilize the available screen real estate.

Here are some examples of the different changes you will see:

#### Microsoft Edge

![Large screen](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/large.png)

On larger screens, the [SplitView](http://try.buildwinjs.com/#splitview) pane will push the content to the side, allowing you to freely interact with the content.

![Clipped search while pane is opened](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/clipped-search-pane-opened.png)

As the screen width decreases, the cells will fluidly re-layout and the [AutoSuggestBox](http://try.buildwinjs.com/#searchbox) will stick to the right side of the screen. Eventually, with the pane opened, the AutoSuggestBox will run out of room, prompting the control to disappear from the top right corner and reappear in the SplitView pane as an additional command.

![Pane overlay](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/pane-overlay.png)

Decreasing further, the pane will no longer push the content on invocation. Instead, the pane will overlay the content. When the pane is open, you will not be able to interact with the content right away. Clicking outside the pane will lightly dismiss the pane first, then allow normal interaction with the content area.

![Clipped search while pane is closed](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/clipped-search-pane-closed.png)

Similar to when the pane is opened, the AutoSuggestBox will disappear from the top right corner when it runs out of room. It will reappear in the SplitView pane.

![Clipped headers](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/clipped-headers.png)

When the [Pivot](http://try.buildwinjs.com/#pivot) headers become clipped, they will reorder themselves such that the current Pivot section is displayed first. Navigating to another section will either slide the headers to the left or the right, always keeping the current section displayed first. You may recognize this behavior from Windows Phone. Try swiping if you have a touch device!

![Small screen](https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/small.png)

Finally, on the smallest devices, the SplitView pane will hide itself, leaving just the SplitViewPaneToggle control. Clicking the toggle will open and close the pane, with the former action overlaying the content.

#### iPhone 5s

Here are some examples of what the app looks like on an iPhone 5s:

Portrait:

<img width="320" height="568" src="https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/iphone5s-portrait.jpg">

Landscape:

<img width="568" height="320" src="https://raw.githubusercontent.com/wiki/jayrenn/react-winjs-demo/images/iphone5s-landscape.jpg">

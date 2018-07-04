# makeItZoom.js - Easy ZUIs
A JavaScript Framework that makes Zooming User Interfaces Easy

Web applications can now do real work, and frequently real work requires real estate. makeItZoom.js gives you infinite real estate for your web application, along with several tools that every serious web application will need at its core:

- Infinitely Zooming Workspace
- CSS Styling works normally
- Native HTML controls, such as inputs
- Drag and Drop Events (Plays nice with a library of your choice)
- Dependency Free: Use whichever JS Libraries and CSS Frameworks you're already using, and no extras
- 8kb gzipped (5kb if you already have a Three.js dependency)

It has no dependencies. To use it, just include the script at the top of your page:

```HTML
<script type="text/javascript" src="makeItZoom_0.0.1.min.js"></script>
```

You can specify the DOM element that will contain the zoomable interface. All child elements will zoom. Use the class "makeItZoom", or specify your own during init. Here's some makeItZoom-able markup:

```HTML
<div class="makeItZoom">
  <div>This stuff is zoomable</div>
</div>
```

At the bottom of your page, initialize makeItZoom. Every configurable parameter has a default, so you can call simply makeItZoom(), but everything is configurable. Defaults are:

```HTML
<script type="text/javascript">
  var instance = new MakeItZoom({
    // Configuration Object
  });
</script>
```

**Note Re: Context Menus**

The browser's native context menu will be suppressed by default since dragging with the right mouse button serves as a "pan" gesture. You can change this behavior in configuration, or you can listen for a special context menu event if you're using right-click context menus. See [Events](#Events) below.

#Documentation
- [Configuration](#configuration)
- [Methods](#methods)
- [Events](#events)
- [Examples](#examples)

#Configuration
|      Option   |   Default     |  Notes |
| ------------- |:-------------:| -------|
|  containerId  | "makeItZoom"  | Must exactly match the id of a container already in the DOM by the time MakeItZoom is called. All contents will be zoomable |
| maxZoomScale |  1.0  | Zoomed items will not appear larger than this scale. 1.0 = 100%. Beware that Firefox for Linux is not able to render fonts larger than 1000px |
| minZoomScale |  0.1  | Zoomed items will not appear smaller than this scale. 1.0 = 100% |
| zoomSpeed |  2.0  | Speed at which the scene will zoom. Larger is faster |
| zoomTowardMouse | true | Zoom centers around mouse cursor's position by default or (0,0) if false. The default should feel more natural since the object under the mouse pointer will stay in position on screen during the zoom.|
| panButton |  2  | Which mouse button is used to Pan. 0 = Left, 2 = Right|
| disableNativeContextMenu | true | With the default mouse configuration, the right mouse button should not trigger the context menu (since it's being used for panning)|
| hardwareAccelerated | true | Hardware acceleration may not look as sharp in some circumstances since textures are transferred as bitmaps to the GPU, but performance is vastly smoother.|
| fullScreen | false | set to true so that the zooming container adjusts for browser resize events|
| zeroAtCenter |  false | Default puts 0,0 in the top-left corner. True puts (0,0) in the center of the zoomable area|
| enableUserInteractions | true  | Set to false to use MakeItZoom without mouse/touch events, as in the zooming slideshow example|
| bounds | undefined |Set a bounds object of the form ```{top: -100, left: -100, bottom: null, right: null}``` to prevent users from zooming or scrolling outside a particular area. Note that if you define all 4 bounds and the aspect ratio of your user's screen does not match the zoom container, she will be able to zoom out until all 4 of your bounds are just barely visible.|

#Methods
|      Method (arguments) | Returns |    Notes |
|-------------------------|---------|----------|
| addZoomable(DOMElement)|undefined|Adds a new element to the zoomable workspace at runtime. Element can be positioned by assigning top and left positioning before passing to addZoomable()|
| removeZoomable(DOMElement)|undefined|Removes an element. Can be one added at init or during runtime.|
| zoomTo(x,y,scale) |undefined|Instantly re-renders the zoomable workspace at the specified coordinate and scale|
| getCurrentScale() |Number|The scale of the scene as rendered|
| getCenter() |Object ```{"x": Number, "y": Number}```| The point at the center of the zoomable workspace in world x/y coordinates. Note that this is affected by where your center is set, either the top-left or center of your zoom window.|
| getContainer() |DOMElement|A convenience method to return the DOM Element associated with the zoom instance's container.|
| setEnableUserInteractions(true) |undefined|Allows you to toggle user interactions on and off at runtime|
| getScene() |THREE.Scene|**ONLY When using with ThreeJS** Returns the Scene associated with the Zoomable CSS objects. See examples 3 and 4.|
| getCamera() |THREE.Camera|**ONLY When using with ThreeJS** Returns the Camera associated with the Zoomable CSS objects. See examples 3 and 4.|
| getRenderer() |THREE.Renderer|**ONLY When using with ThreeJS** Returns the Renderer associated with the Zoomable CSS objects. See examples 3 and 4.|

#Events
- **mz_render** is called every time the zoomable container changes due to a zoom or pan event, regardless of whether that change was user-initiated.
```JavaScript
zoomInstance.addEventListener("mz_render",function(e){
  console.log('render event', e.mz_scale, e.mz_center_x, e.mz_center_y);
});
```
- **mz_contextmenu** is called for right-click events, when they are captured.
```JavaScript
zoomInstance.addEventListener("mz_contextmenu",function(e){
  console.log('Right-click event', e.clientX, e.clientY, e.target);
});
```

#Examples
#[01. Hello, makeItZoom!](http://strandedcity.github.io/makeItZoom/demo/01_hello_zoom.html)
#[02. Prezi-Like Zooming Slideshow with TweenLite](http://strandedcity.github.io/makeItZoom/demo/02_zooming_slideshow.html)
#[03. A Large Chart of Connected Nodes - Using Three.js to draw lines in an overlapping WebGL Scene](http://strandedcity.github.io/makeItZoom/demo/03_node_map.html)
#[04. Drag, drop, and zoomable Node Chart with Interact.js - Adds Drag-and-drop to Example 03](http://strandedcity.github.io/makeItZoom/demo/04_draggable_node_map.html)

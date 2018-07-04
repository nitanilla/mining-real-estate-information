# AOL Slideshow

<!-- TODO: Write better description. -->
Your friendly, neighborhood slideshow.

## Documentation

### Options
<dl>
<dt>theme</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>This allows developers to add additional class names to the container &lt;div&gt;, useful for making override styles.</td>
    </tr>
    <tr>
        <th>Default</th><td>"default"</td>
    </tr>
</tbody></table></dd>

<dt>preset</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>This can be set to any of the presetOptions to quickly set some common configurations. This will also add a class with the below preset.</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Default</th><td>""</td>
    </tr>
</tbody></table></dd>

<dt>carousel</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Turns the gallery into a carousel module where there are slides on both sides.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>0</td>
    </tr>
</tbody></table></dd>

<dt>carouselSiblings</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>How many slides are visible on each side, needed for prefetch logic and understanding when to pop the last slide to the front, and vice versa.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>2</td>
    </tr>
</tbody></table></dd>

<dt>speed</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>How long all transition animations take.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>300</td>
    </tr>
</tbody></table></dd>

<dt>photoWidth, photoHeight</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The max width and height of the photos inside of the gallery.  We dynamically resize to these. Future: Auto flags depending on the screen real estate!</td>
    </tr>
    <tr><th>Type</th><td>int, int</td></tr>
    <tr>
        <th>Default</th><td>450, 325</td>
    </tr>
</tbody></table></dd>

<dt>thumbnailWidth, thumbnailHeight</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The max width and height of generated thumbs.</td>
    </tr>
    <tr><th>Type</th><td>int, int</td></tr>
    <tr>
        <th>Default</th><td>74, 74</td>
    </tr>
</tbody></table></dd>

<dt>sponsorAdMN</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>If supplied, render a sponsorship advertisement</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Default</th><td></td>
    </tr>
</tbody></table></dd>

<dt>sponsorAdWidth, sponsorAdHeight</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The sponsorship width and height.</td>
    </tr>
    <tr><th>Type</th><td>int, int</td></tr>
    <tr>
        <th>Default</th><td>215, 35</td>
    </tr>
</tbody></table></dd>

<dt>fullscreenAdMN</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>If supplied render an advertisement in fullscreen mode.</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Default</th><td></td>
    </tr>
</tbody></table></dd>

<dt>fullscreenAdWidth, fullscreenAdHeight</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Width and height of rendered fullscreen advertisement.</td>
    </tr>
    <tr><th>Type</th><td>int, int</td></tr>
    <tr>
        <th>Default</th><td>300, 250</td>
    </tr>
</tbody></table></dd>

<dt>fullscreenSponsorAdMN</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>If supplied render a sponsorship advertisement in fullscreen mode.</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Default</th><td></td>
    </tr>
</tbody></table></dd>

<dt>fullscreenSponsorAdWidth, fullscreenSponsorAdHeight</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Width and height of rendered fullscreen sponsorship advertisement.</td>
    </tr>
    <tr><th>Type</th><td>int, int</td></tr>
    <tr>
        <th>Default</th><td>215, 35</td>
    </tr>
</tbody></table></dd>

<dt>thumbnailCount</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>How many thumbs to display, we don't quite do anything with this yet, may be useful later for showing an initial thumb set, or controlling how many per thumbnail pane.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>999</td>
    </tr>
</tbody></table></dd>

<dt>thumbnailAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Inserts thumbnails immediately after the gallery &lt;div&gt;. False inserts before.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>activeIndex</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The active photo index on initialization.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>1</td>
    </tr>
</tbody></table></dd>

<dt>refreshDivId</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The &lt;div&gt; ID containing the AJAX ad to refresh. This is tied to the gallery slides.</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Default</th><td>""</td>
    </tr>
</tbody></table></dd>

<dt>refreshCount</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>The refresh ratio.  Example: 3 means refresh the ad every 1 in 3 clicks.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>9</td>
    </tr>
</tbody></table></dd>

<dt>showThumbnails</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>This controls whether we show the thumbnails by default instead of the gallery view.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>false</td>
    </tr>
</tbody></table></dd>

<dt>toggleThumbnails</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Controls the rendering of the "Show Thumbnails" button.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>toggleThumbnailsAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Inserts the "Show Thumbnails" button before the gallery in the DOM if true, after if false.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showName</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Whether or not to show the name of the gallery.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showDescription</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Whether or not to show the description of the gallery.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>false</td>
    </tr>
</tbody></table></dd>

<dt>descriptionAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Whether or not to show the description after.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>false</td>
    </tr>
</tbody></table></dd>

<dt>showControls</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Whehther or not to show the "Next" and "Back" buttons</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>controlsInside</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>If true, insert the controls inside the gallery &lt;div&gt;.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>false</td>
    </tr>
</tbody></table></dd>

<dt>controlsAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>If controlsInside is true, this inserts the controls before (prepends) the photos list in the gallery &lt;div&gt; when true and inserts the controls after (appends) when false.  If controlsInside is false, this inserts the controls after (appends) the gallery &lt;div&gt; when true and before (prepends) the controls when false.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showFullscreen</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Show the fullscreen button.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showStatus</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Shows the status indicator.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showCaptions</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Shows the captions for the photos. By default this is a standard fade-in/out.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>captionsAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Inserts the controls inside the gallery &lt;div&gt; when true and outside when false.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>showCredit</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Shows the credit box.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>creditInside</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Shows the credits inside this gallery UI element.</td>
    </tr>
    <tr>
        <th>Default</th><td>"$captions"</td>
    </tr>
    <tr><th>Type</th><td>string</td></tr>
    <tr>
        <th>Available values</th>
        <td>
            <ul>
                <li>"$captions"</li>
                <li>"$slides"</li>
            </ul>
        <td>
    </tr>
</tbody></table></dd>

<dt>initTracking</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>True initializes Comscore, Data Layer and Omniture tracking.  Node: this should be handled automatically in the future.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>true</td>
    </tr>
</tbody></table></dd>

<dt>creditAfter</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Appends credit within the "creditInside" container if true and prepends the credit if false.</td>
    </tr>
    <tr><th>Type</th><td>boolean</td></tr>
    <tr>
        <th>Default</th><td>false</td>
    </tr>
</tbody></table></dd>

<dt>imageQuality</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>ImageMagick quality setting.</td>
    </tr>
    <tr><th>Type</th><td>int</td></tr>
    <tr>
        <th>Default</th><td>85</td>
    </tr>
    <tr>
        <th>Available values</th><td>Range: 0-100. 0 is lowest quality and 100 is highest quality.</td>
    </tr>
</tbody></table></dd>

<dt>fullscreenOptions</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>An object containing fullscreen display configurations.</td>
    </tr>
    <tr><th>Type</th><td>object</td></tr>
    <tr>
        <th>Default</th>
        <td><pre>
        {
            photoWidth:559,
            photoHeight:487,
            preset:"carousel",
            carouselSiblings:3
        }
        </pre></td>
    </tr>
</tbody></table></dd>

<dt>template</dt>
<dd><table><tbody>
    <tr>
        <th>Description</th><td>Object containing various output templates that developers can override.</td>
    </tr>
    <tr><th>Type</th><td>object</td></tr>
    <tr>
        <th>Default</th><td><pre>
        {
            status:"{{active}} of {{total}}",
            credit:"Photo: {{credit}}",
            fullscreen:"Fullscreen",
            thumbnails:"Thumbnails",
            next: "Next",
            back: "Back"
        }
        </pre></td>
    </tr>
    <tr>
        <th>Available template values</th>
        <td>
            <ul>
                <li>{{active}} - Active photo number.</li>
                <li>{{total}} - Total number of photos</li>
                <li>{{credit}} - Photo credit</li>
            </ul>
        </td>
    </tr>
</tbody></table></dd>
</dl>

## Examples
_(Coming soon)_

## Release History
_(Nothing yet)_

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [grunt](https://github.com/cowboy/grunt).

### Important notes
Please don't edit files in the `dist` subdirectory as they are generated via grunt. You'll find source code in the `src` subdirectory!

While grunt can run the included unit tests via PhantomJS, this shouldn't be considered a substitute for the real thing. Please be sure to test the `test/*.html` unit test file(s) in _actual_ browsers.

### Installing grunt
_This assumes you have [node.js](http://nodejs.org/) and [npm](http://npmjs.org/) installed already._

1. Test that grunt is installed globally by running `grunt --version` at the command-line.
1. If grunt isn't installed globally, run `npm install -g grunt` to install the latest version. _You may need to run `sudo npm install -g grunt`._
1. From the root directory of this project, run `npm install` to install the project's dependencies.

### Installing PhantomJS

In order for the qunit task to work properly, [PhantomJS](http://www.phantomjs.org/) must be installed and in the system PATH (if you can run "phantomjs" at the command line, this task should work).

Unfortunately, PhantomJS cannot be installed automatically via npm or grunt, so you need to install it yourself. There are a number of ways to install PhantomJS.

* [PhantomJS and Mac OS X](http://ariya.ofilabs.com/2012/02/phantomjs-and-mac-os-x.html)
* [PhantomJS Installation](http://code.google.com/p/phantomjs/wiki/Installation) (PhantomJS wiki)

Note that the `phantomjs` executable needs to be in the system `PATH` for grunt to see it.

* [How to set the path and environment variables in Windows](http://www.computerhope.com/issues/ch000549.htm)
* [Where does $PATH get set in OS X 10.6 Snow Leopard?](http://superuser.com/questions/69130/where-does-path-get-set-in-os-x-10-6-snow-leopard)
* [How do I change the PATH variable in Linux](https://www.google.com/search?q=How+do+I+change+the+PATH+variable+in+Linux)

### ARTZ Notes

* Mention that a compilation step is needed (i.e. run grunt after cloning).
* Install compass (http://compass-style.org/install/).
* Mac users will want to have XCode and the command line tools installed.
* Homebrew is the preferred package manager.

### JJ Notes
* Explicitly list in requirements to install grunt and phantomjs globally


## License
Copyright (c) 2012 AOL, Inc.
All rights reserved.

https://github.com/aol/jquery-slideshow/blob/master/LICENSE-BSD

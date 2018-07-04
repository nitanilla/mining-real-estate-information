# Breakpoint Tester Chrome Extension

The Breakpoint Tester chrome extension is used to quickly and easily test the responsiveness of a website at various breakpoints. Breakpoint Tester ships with some sensible default breakpoints but you're more than welcome to define your own custom breakpoints in the extensions settings.

Breakpoint Tester uses the media queries from Bootstrap 3 as a baseline for it's breakpoint presets which are:
- 480px (Mobile)
- 768px (Tablet)
- 992px (Laptop)
- 1200px (Desktop)

## Installation
Chrome Webstore: [Breakpoint Tester](https://chrome.google.com/webstore/detail/breakpoint-tester/ffmkpfegfpfjaacpgmbloagbibfnmabj)

TODO: Walk through the installation steps (for installing it manually in developer mode)

## How To Use
It should be fairly obvious...

TODO: Describe how to use the extension, thow in a screenshot or two for clarity.

## Roadmap
- Add an Options/Settings page
- Add ability to change height as well as width (enable/disable in settings)
- Design better icons. They look fine at high resolution (128px) but the smaller they are the worse they look.
- Use the 'active' class when a preset is selected to denote which breakpoint the window is currently set to.
- Add ability to save named breakpoints (e.g. 480px = Nexus S)
- Re-design the GUI. It's OK...but it needs to be spectacular.
- Add context menu for quick access with toggling the extension popup
- Add keyboard shortcuts ("commands" in Chrome API) for quickly switching between presets
	- Ctrl + Left/Right Arrow = "Scroll" through the presets
- Add ability to choose what framework the presets should be based on or define your own. I'm not sure how different each of the frameworks are when it comes to breakpoints but if there's a need then lets make it happen.
	- Bootstrap 2
	- Bootstrap 3
	- Foundation 4
	- Foundation 5
	- Custom Presets (Named)


## Release History

### v1.0.4
**April 18, 2014**
+ Added a history of the 5 most recently used custom breakpoints.
+ Adjusted the layout of the popup to allow for more features:
	+ The overall layout is much more compact to allow for better use of the real estate available to the popup.
	+ Added a sidebar that contains recently used breakpoints for quick reference and fast re-use.
	+ Made the gray a little darker (from #DDD to #BBB) to provide better contrast/readability on "less than amazing" screens.
+ Added support for multiple monitors. When selecting a breakpoint the Chrome window will no longer jump to the primary monitor, it will use whichever monitor it is currently on.
+ Added the ability to determine if the user prefers the right or left side of the screen and resize with this preference in mind (might make this a user-definable setting in the future)
+ Fixed bug in Chrome v34 that pushed the slider position label and button down under the slider.
+ Removed unnecessary permissions

### v1.0.2
**Apr 7, 2014**
+ Fixed references to fonts in CSS pointing to wrong file location. Fonts should load properly when not installed on the local machine.

### v1.0.1
**Mar 31, 2014**
+ Enabled Google Analytics to track usage of presets, custom breakpoints, etc. to facilitate future development.

### v1.0.0
**Mar 21, 2014**
+ Switched to a lighter theme to better work with the default Chrome UI
+ Made some minor modifications to the popup GUI to support various new features
+ Fixed the breakpoint calculation to account for the Chrome window/frame. Tested on Windows 8.
+ Added the Custom Breakpoint slider to allow manual selection of a custom breakpoint.
+ Fixed the resizing of the Chrome window from a maximized state bug (overflow on top/bottom) on Windows 8.

### v0.1.0
**Mar 20, 2014**
+ Initial release
+ It works but there remains quite a bit of tweaking and polishing to do.
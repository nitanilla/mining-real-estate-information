# Firefox 4 userChrome.css tweaks for XFCE, Compiz, ... under Linux

# What is it?

With Firefox 4, one can choose to combine the menu bar with the tabs to maximize screen real estate.

This is well integrated under the Gnome window manager, but if like me you use Compiz or another window manager, chances are that it might not look as nice as gnome

I put together an userChrome.css stylesheet to fix that (userChrome.css is a set of CSS rules for the Firefox user interface).

# Screenshots

See this screenshot before:

![Before](https://github.com/jphpsf/fx4-linux-tabs-on-top/raw/master/before.png "Before")

And after:

![After](https://github.com/jphpsf/fx4-linux-tabs-on-top/raw/master/after.png "After")

# Install

Adapt userChrome.css as needed and then place it under the chrome dir of your Firefox profile.

# Notes

I could not figure out how to inherit the colors from my window manager so the colors are currently hard coded.

To figure out the id or class name to style, use the [ChromeBug extension](http://getfirebug.com/wiki/index.php/Chromebug_User_Guide)

To try out new style without restarting the browser, use the [Stylish extension](https://addons.mozilla.org/en-US/firefox/addon/stylish/)

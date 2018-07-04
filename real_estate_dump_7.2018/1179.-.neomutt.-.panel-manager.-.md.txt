# Panel Manager

## What is it?

This is a sample application to demonstrate a mechanism to divide up screen
real estate.  The panels can be fixed, or variable, width/height.  Their
visibility can also be toggled.

I wrote it to remind myself how ncurses windows work and to demonstrate how
I'd like to carve up the screen space -- separating out the graphics code.

## Why?

At the moment, mutt puts all of its information in one big window.
Occasionally, this window is split in two.  All the components of mutt draw
directly onto the screen at fixed locations.

Throughout the mutt code there are hard-coded references to the curses
variables: COLS, LINES.  Also, many component write text at fixed positions on
the screen.

## Panels

To implement a sidebar, currently you must alter every piece of code that
writes to column 0.

Ideally, every component should be given coordinates describing the piece of
screen it has been allocated.  If the screen changes (e.g. is resized) then
the component would be signalled and given new coordinates.

Curses windows can enforce limits on where text is drawn, preventing
interference between components.

## Controls

| Button | Action                       | 
| ------ | :--------------------------- | 
| s      | Toggle sidebar               |
| i      | Toggle index                 |
| p      | Toggle pager                 |
| h      | Toggle help page             |
| x      | Swap the side of the sidebar |
| q      | Quit                         |

## Who?

* Rich Russon (FlatCap) &lt;rich@flatcap.org&gt;
* https://flatcap.org/

![flatcap](https://flatcap.org/gfx/flatcap.png)

## License

The code is released under the GPLv3.
See [LICENSE.md](https://github.com/neomutt/panel-manager/blob/master/LICENSE.md) for more details.


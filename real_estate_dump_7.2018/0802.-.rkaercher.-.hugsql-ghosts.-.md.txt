# hugsql-ghosts

Displays [hugsql](https://www.hugsql.org) defns of your queries as an overlay in your cider buffers.

<img src="screenshot.png">

*(It'll look better with your color theme of course.)*

## Installation

### MELPA
As hugsql-ghosts is available via [MELPA](https://melpa.org/), you can install it via:

<kbd>M-x</kbd> `package-install` <kbd>RET</kbd> `hugsql-ghosts` <kbd>RET</kbd>


### Manual
Should you wish to install it manually, you should install the
following packages:

 - <a href="https://github.com/magnars/s.el">s.el</a>
 - <a href="https://github.com/magnars/dash.el">dash.el</a>
 - <a href="https://github.com/clojure-emacs/cider">cider</a>

Then put hugsql-ghosts.el in your elisp path and require it in your .emacs:

```emacs-lisp
(require 'hugsql-ghosts)
```

### Hook
In either case, add it to the [CIDER](https://github.com/clojure-emacs/cider) mode hook:

```emacs-lisp
(add-hook 'cider-mode-hook 'hugsql-ghosts-install-hook)
```

Overlays should now appear in all CIDER buffers which have any of `(hugsql/def-db-fns "path/to/your/queries.sql")`, `(hugsql/def-sqlvec-fns "path/to/your/queries.sql")` or `(conman/bind-connection *your-db-con* "path/to/your/queries.sql")`.
Please note that this only works if you've required `hugsql.core` as `hugsql` in your clojure source. Furthermore, changes in sql are only reflected after you reload your CIDER buffer (C-c C-k).

**Hugsql-ghosts needs an active cider connection to work as the query parsing is done by the hugsql library itself via cider.**


## Usage

The display of ghosts can be triggered manually by calling `hugsql-ghosts-display-query-ghosts`, to get rid of them simply call `hugsql-ghosts-remove-overlays`.

To jump to the SQL file referenced you can bind `hugsql-ghosts-jump-sql-file` to a suitable key. It'll ask which one to jump to if there are multiple files referenced.

## Customization

If you don't want the function doc strings to be displayed you can set `hugsql-ghosts-show-descriptions` to `nil`.
By default the doc strings will be displayed on the same line as the `defun`, if you don't like that or don't have enough horizontal screen real-estate, you can set `hugsql-ghosts-newline-before-docstrings` to `t`.

Finally, you can customize the face `hugsql-ghosts-defn` to adapt the overlay appearance to your liking.


## Acknowledgement

This is an adaption of [yesql-ghosts](https://github.com/magnars/yesql-ghosts) by Magnar Sveen so most of the credit must go to him.

## License

Copyright (C) 2017 - 2018 Roland Kaercher

Authors: Roland Kaercher <roland.kaercher@gmail.com> based on work by Magnar Sveen <magnars@gmail.com>

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

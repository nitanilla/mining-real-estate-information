Homegate_notes
==============
homegate_notes is a Greasemonkey script to annotate the search
results of various real estate search engines.

See http://sourcepole.ch/2011/4/17/annotating-third-party-web-pages
for an example.

The script also illustrates how you can make a Greasemonkey script that
lets you annotate search results.

For Greasemonkey see:
http://www.greasespot.net/

You can find many more Greasemonkey scripts at:
http://userscripts.org/

Actually this script also has a second home there:
http://userscripts.org/scripts/show/101302


Supported real estate search engines
------------------------------------
* http://www.homegate.ch/
* http://www.schaffhausen.ch/frontend/index.cfm?method=immo
* http://www.alle-immobilien.ch/

Tips
----
* Schaffhausen.ch does Ajax requests to retrieve its results. I have not yet
  figured out how to catch those automatically and then add the note input
  fields. Thus you need to click on the little "show notes" field in the
  bottom left, to load the note fields.

* if you prefix your note with "nix:" then the comment will be coloured in
  blue, suggesting that the annotated estate is not interesting.

License
-------
GPLv2

Author
------
Tomáš Pospíšek - tpo_deb at sourcepole.ch

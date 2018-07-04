### What's PicoBrewing?

I like my Picobrew quite a bit, but the web interface leaves quite a bit to be desired.  I thought I'd try my hand at improving the brew session view, as when I'm brewing from the couch I like to keep an eye on what the Zymatic's up to in the basement and the graph view wasn't showing the information ***I*** thought was useful.  I wanted something that reflected a view closer to what the LCD screen shows as it's brewing.  And with a web view having more real estate to work with, it might as well show more too.  I put this together over a couple evenings (while Picobrewing of course) as an alternative view of the current brew session.  It's not currently intended to completely replace the default view, but to supplement it (though the only real missing feature is the notes, and they could easily be added).


[<img src="http://i.imgur.com/sxwaMxx.png" width="200px">]
(http://i.imgur.com/sxwaMxx.png)
[<img src="http://i.imgur.com/whs5OUE.png" width="200px">]
(http://i.imgur.com/whs5OUE.png)



### Using

###### New in v2

v2 is currently being hosted in my Pico Proxy instance (see [that project](https://github.com/toddq/pico-proxy)) at http://pico-proxy.herokuapp.com/whats-picobrewing.

v1 was stand-alone HTML/JS able to pull data directly from Picobrew's website because they didn't require any authentication on fetching any data.  


### TODO

- Add Notes
    - View
    - Create/Edit/Delete
- Rewrite in VueJS

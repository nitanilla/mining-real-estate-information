## YouTube Hover Links (YTHL) - a JS experiment

**[Live demo](http://nealrs.github.io/YTHL)**

YTHL creates minimal YouTube embeds that open & auto-play on hover. Result: less wasted real estate.

**Instructions**

1. Load up jQuery, `ythl.css`, and  `ythl.js` in `<head>`.

2. Use `<span>` elements and data-attributes to embed your video. Here's how you'd embed Katy Perry's _Roar_ music video: `<span class="ythl" data-id="CevxZvSJLk8" data-title="Katy Perry - Roar" data-auto="yes"></span>` Neat right? just plug in the video id, your link text, and an autoplay flag. YTHL does the rest.

3. Srsly bro, that's it. Enjoy!

**Notes**

YTHL depends on  [Fitvids.js](https://github.com/davatron5000/FitVids.js) for responsive embeds - but if you can live without that, you can also nix jQuery. (You'll have to refactor some of the code though.)

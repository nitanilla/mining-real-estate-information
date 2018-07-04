HousingKlout

Synopsis:

 A fun little JavaScript hack that mashes up:

   1. 3Taps - Craigslist home/apt listings in SF
   2. Google Maps - Find lat/lon based on unformatted address string
   3. Twitter - Geo-tagged tweets near within radius of each listing
   4. Klout - Average Klout score of each tweeter from tweets above
   5. deCarta - Plot tweets and pin home listings with Klout scores
      and hyperlinked back to Craigslist listings.

 What you end up with is a map with a bunch of real estate listings
 along with a Klout score. Silly? Yes. But mashing up completely
 disparate data that only has lat/lon in common makes it interesting.

Requirements:

   1. 3Taps API key - http://register.3taps.com/member/register
   2. Klout API key - http://developer.klout.com

      The two above you'll paste into the HTML form.

   3. Google Maps API key - http://code.google.com/apis/maps/signup.html

      The Google Maps API key/script-src you'll paste into index.htm
      source - around line 54)

   This has been tested on the most recent versions of Firefox, 
   Safari and Chrome (MSIE not tested) and it seems to work fine.

Bundled:

   1. parseaddress jQuery plugin - quick and dirty unformatted
      address string resolver/parser that uses Google Maps API
      src: http://bit.ly/9zqTUE

   2. deCarta.js and CONFIG.js - deCarta mapping JS files
      borrowed from their sample documentation
      src: http://developer.decarta.com

   3. 3taps JS - 3Taps JavaScript SDK
      src: http://3taps.com

Caveats:

   This was a hackathon project built from soup to nuts in just
   a few hours. It's being made available so that people can see
   five APIs converge into one project in a few chunks of 
   JavaScript code.

   Please feel free fix/report bugs as you find them, or refactor
   the slop. :)

Author:

   Neil Mansilla
   Email: neil@mansilla.com
   Twitter: @mansillaDEV

   http://developer.mashery.com

License:
  
  Open Source Initiative OSI - The MIT License (MIT)
  Licensing: The MIT License (MIT)
  Copyright (c) 2011 Neil Mansilla

  Permission is hereby granted, free of charge, to any person 
  obtaining a copy of this software and associated documentation 
  files (the "Software"), to deal in the Software without restriction, 
  including without limitation the rights to use, copy, modify, merge, 
  publish, distribute, sublicense, and/or sell copies of the Software, 
  and to permit persons to whom the Software is furnished to do so, 
  subject to the following conditions:

  The above copyright notice and this permission notice shall be 
  included in all copies or substantial portions of the Software.
  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, 
  EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES 
  OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND 
  NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT 
  HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, 
  WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING 
  FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR 
  OTHER DEALINGS IN THE SOFTWARE.
  
  All logos and tradenames represented are the intellectual property 
  of the respective owners, including:
 
  Mashery, deCarta, Twitter, 3Taps and Klout.

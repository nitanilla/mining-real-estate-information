# spotify-materialize
Experimenting with Spotify API, Materialize CSS, jQuery Promises, jQuery Templates



## a little info:

I have countless little projects like this one, that I have started for purposes of learning some new technologies.  They all have a glimmer of promise, but were all just a means to learning new things.  Many of them took drastic twists and turns and I started down one path and radically changed how I was building them.

I realized I was doing myself a great disservice by not just creating repositories for them and putting my code out for the world to see, whether it was totally incomplete or never to be finished.  Perhaps some snippets could be useful for someome, or simply an indicator to someone else that I have implemented code from their library in one of my projects.

So I hope this project is the first of many I am able to share with the community.





#Spotify Materialize

- Installing
  - npm install
  - bower install
  - run grunt

#libararies Used:
  - <a href="https://github.com/Dogfalo/materialize">https://github.com/Dogfalo/materialize</a>
    - I just discovered this library when it had about 2,500 stars and seems to be growing rapidly  
    - It seems to solve many of the issues I was constantly trying to solve when working with Bootstrap
    - My only complaint is that it uses Sass rather than Less.  Getting Sass up and running on Windows was a bit of a pain and I don't have the same comfort level as I do with Less.
  - <a href="https://github.com/jquery/jquery">https://github.com/jquery/jquery</a>
   - A project staple, while not always needed, I always end up regret not just adding it in the first place.
  - <a href="https://github.com/BorisMoore/jquery-tmpl">https://github.com/BorisMoore/jquery-tmpl</a>
   - The original official jQuery Templates plugin.  No longer in active development, but works fine for simple templating.
  - <a href="https://github.com/daneden/animate.css">https://github.com/daneden/animate.css</a>
   - I don't think I have even made use of this as of yet...
  - <a href="https://github.com/twitter/typeahead.js">https://github.com/twitter/typeahead.js</a>
    - I think this would be an ideal way to display the search results, but have not done so yet.

#To Do:
  - Convert PHP to HTML; it is not needed and removing it will allow the demo to be run right on Github
  - Add an about page
  - Clean up footer
  - Edit Sass files rather than overwriting everything in plain CSS
  - Add related artists to related artists, possibly 3 related artists for each of the 6 related artists now
  - Possibly find a better way to create the "org chart" lines rather than bastardizing the rows and columns, but then again, it works as is, and should scale nicely on different screen sizes.
  - Add localstorage db to store user info, access tokens, etc
  - refactor search form to maximize screen real estate for displaying related artist info.
  - Add client side JS code for allowing user to login to Spotify... I didn't realize this could be done entirely client side until just now.

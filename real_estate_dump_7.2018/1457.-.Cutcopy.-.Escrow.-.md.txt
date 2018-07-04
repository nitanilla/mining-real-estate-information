

    `7MM"""YMM                                                    
      MM    `7                                                    
      MM   d    ,pP"Ybd  ,p6"bo `7Mb,od8 ,pW"Wq.`7M'    ,A    `MF'
      MMmmMM    8I   `" 6M'  OO   MM' "'6W'   `Wb VA   ,VAA   ,V  
      MM   Y  , `YMMMa. 8M        MM    8M     M8  VA ,V  VA ,V   
      MM     ,M L.   I8 YM.    ,  MM    YA.   ,A9   VVV    VVV    
     .JMMmmmmMMM M9mmmP'  YMbmd' .JMML.  `Ybmd9'     W      W     


*A Jekyll theme for real estate agents who like to blogging or podcasting :heart:*

[Demo](http://giant-pepper.cloudvent.net)

It's github pages compatible, but was made for use with [Cloudcannon](http://cloudcannon.com/) - A Jekyll hosting site and CMS.

Should work with Jekyll version 2.4 or 3.0
You'll need Ruby, bundler, and Jekyll installed on your computer to launch it locally. You can get instructions [here](http://jekyllrb.com/).
To get started, download the theme and inside terminal navigate to inside the folder and type `bundler install`. This will install all your dependancies. Then when this is done type `bundler exec guard`. This will serve up a server and auto reload when you make changes. You'll need the chrome extension livereload for this to work. autoprefixer is also installed but since *github and Cloudcannon run without plugins* it doesn't really do anything for you. I've opted to use bourbon mixins to handing vendor prefixing. You can get the documentation for that [here](http://bourbon.io/docs/).

I've never gotten guard to work on windows so if that's the case you'll just have to type `bundler exec jekyll serve` which will launch a github pages compatible server. If everything goes off without a hitch consider yourself lucky, ruby dependancies usually poor windows support.

The File Structure is as such:

    .
    ├── _config.yml //This is the settings file for jekyll
    ├── _drafts //this is where we store drafted posts
    ├── _includes //these are sections or blocks of html we use throughout the blog
    |   ├── footer.html
    |   └── header.html
    ├── _layouts //this controls the layout of the page. It's mainly comprised of the includes files.
    |   ├── default.html
    |   └── post.html
    ├── _posts //this is where the posts go. duh.
    |   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
    |   └── 2009-04-26-barcamp-boston-4-roundup.textile
    ├── _data //This controls all of the client info, images, etc.
    |   └── settings.yml
    ├── _site //Ignore it. This is the final generated site that jekyll produces.
    ├── css
    |   └── main.sass //the main sass file and all the sites css variables.
    ├── sass
    |   └── vendors
      |   └── normalize.scss // bourbon, skeleton and a few other css code bases I used to make the site.
    |   └── main.sass //the main sass file and all the sites css
    ├── img //images directory
    |   └── icons //This is where things like the favicon go.
    |   └── svg //All the actual icons used inside the blog itself.
    └── index.html // this is the blog feed.

Individual pages are

-  elements.html - this is for setting up the css and can be deleted. It contains web elements for easier styling.
- homesearch.html - this is an option home search form for clients to use.
- homevalue.html - same thing but for sellers.
- tags.html - lists all topics and organizes them by tags.
- thankyou.html - use this as a landing page for the main newsletter optin form.
- about.md - you can simply paste the bio or "about" content in here. It's in markdown, so use that for formatting.
- itunes.xml - itunes valid xml feed for podcasting. Don't forget to set it up inside _data/settings.yml
- feed.xml - this is the rss feed.

## Customization:
  1. First thing you'll want to do is fill out the settings.yml file in the `_data` folder. It should all be very straight forward.
    client info, socials, and podcast info. Remember to fill out the podcast part, because otherwise it'll be left with the examples. If something doesn't apply leave it blank or in the case of the social links - leave them as `'#'`. It's set so they won't appear if they're left that way. The hashtag basically represents a blank link.

    Somethings will still need to be altered elsewhere in the theme. I suggest commenting it out rather than removing it outright. It's easier to add it back should the need arise.

    You can do that with html or liquid (Jekyll's templating language). In html that is
    `<!-- comment -->` in liquid it's  `{% comment %} comment {% endcomment %}`. The liquid comments won't render into the final html, so remember that.

  2. To add exterior links to the top navbar, simply follow the profiled format of:

          - title: Link text
           url: http://thisiswhataurllookslike.com
  3. The `homeeval` and `homesearch` are link values for the two call to action buttons. `VR_form` is the form action for the sign up form. This can be from Any ESP, or like we use at Vyral - Vertical Response :stuck_out_tongue_closed_eyes:

  4. The layout options provide a few changes you might want. `review_sm_icons` makes the review buttons (yelp, zillow and trulia) little round buttons like any of the other social icons, instead of the larger pill buttons on the about page. You might want this if you don't have all three profiles. `audit_header` turns on the red area at the top to tell you if you're missing anything, we at Vyral deem required for the end product.

  Turning either of these from `false` to `true` with turn them on, or vice versa.

  5. The Images portion of the settings file control, *you guess it*, the images. `hero_logo_path` is the primary background image, `hero_logo_path` is the logo, and `client_headshot_path` is the headshot for the author that appears in posts and the about page. The `hero_background_hex` is the color of the header section. This is important because if you're on a slow connection the large hero image might take a while to download so you'll want the browser to pain a background so it appears at least, that it's loading faster, or makes the default white text visible. It should be the `$brand` color or preferably a color from the image.

  The images do have some requirements, like the logo should be a png with a transparent background and doesn't need to be larger than 500px wide. If you plan ahead it makes the rest of the image gathering easy.
  * open photoshop and export the logo as stated above - 500px and cropped at a squre ratio 1:1
  * Then also save it inside the site root folder as `siteicon.png`. This is just for cloudcannon's dashboard.
  * Go to [realfavicongenerator.net](http://realfavicongenerator.net/) and follow the instructions. It'll ask for an app name about have way down, use the site title. For theme colors  use whatever the `$brand` color is. When you get to the "favicon generator options" select the second radio button, "I do not want to place favicon..." and input /img/icons/ into the text field. Hit the button. Download the images and put them into the /img/icons/ folder. overwrite if there is already images in there. Copy the html and put it inside the _includes/head.html file. It goes at the very bottom just paste over what's already there.

  Then go back to photoshop and export the logo again, this time cropping to the dimensions `375x435` and save out as twittercard.png. This is for sharing on social media.   

  The Headshot should be optimally be square, head and shoulder shot. The theme doesn't lend itself to team group shots, so keep that in mind.

  6. Next you'll want to adjust the colors, and adjust the css as needed. `main.sass` is the primary file with most of the settings in it. It should of course be very straightforward. The variables are as follows:
```sass

          $main-width: this controls the width of the container element
          $nav-height: the height of the navbar. This will effect things like how much margin the logo has up top and line height etc.

          //fonts
          $bodyfont: the font family for the body text.
          $headerfont: the font family for the head lines.

          //colors

          $brand: This is the main color.
          $brand-light: lighten($brand, 20%) //automatically 20% lighter
          $brand-dark: darken($brand, 10%)  // automatically 10% darker
          $bodycolor: font color for the body text
          $transparent-black: color for all kinds of things, like the navbar and header shadows.

          $nav-background: this is the color of the navbar.
          $header-font-color: this controls the titles and navbar font colors
          $header-shadow: this is the dropshadow on text and the logo inside the site header.
```
The theme includes a custom.sass file for individual theme adjustments. It's a good practice to use it to overwrite things. Especially if you ever need to update the theme.
---------------------------------------
And that should be all you really have to do. It took me about twenty minutes to do all of the above and some customizing.

**Remember to switch the URL out in `_config.yml` before deploying for production**

Some helpful links:
- [Jekyllrb.com](http://jekyllrb.com/) - Jekyll's site and documentation
- [Jekyll.tips](http://jekyll.tips/) - Jekyll tutorials and videos
- [Shopify's guid to Liquid templating](https://shopify.github.io/liquid/)
- [Daring Fireball's guide to markdown syntax](http://daringfireball.net/projects/markdown/)
- [Github's mastering markdown](https://guides.github.com/features/mastering-markdown/)
- [Emoji Cheat Sheet](http://www.emoji-cheat-sheet.com/) - all of the supported emojis.
- [Sass-lang.com](http://sass-lang.com/) - Sass's site and documentation incase you're not familiar with the css preprocessor.
- [Bourbon.io](http://bourbon.io/docs/) - Helpful sass mixins
- [Skeleton css](http://getskeleton.com/) - Skeleton is a css grid framework used by Escrow.   

## Making Posts, Pages, and using Front Matter

Front matter is where we store information for use by Jekyll. It goes at the very top of a page or post and looks like this:

````yaml
---
layout: page
permalink: /testimonials/
title: Testimonials
in_nav: true
---
````
Like everything else it's pretty self explanatory.
- `layout` controls the layout. Escrow has 4: default, page, post, and about.
- `permalink` controls the url of the page/post. for instance: http://blog.com/testimonails/. It's **VERY IMPORTANT** that you remember to add that extra backslash to the end of the link or jekyll might not make it a page and will store it in a different location when serving the files. Permalinks should always look like this for Escrow: **/url/**
- `title` is the title of the page or post
- `in_nav` is for if you want it to be in the navigation bar or not. This has boolean attributes aka `true` or `false`.

### Blog Post Front matter
  Blog post front matter is laid out inside `_posts/_defaults.md` and is as follows:
````yaml
---
layout: post
title:
category: blog  
tags:
  - Market Update
  - Real Estate
  - Buyer Tips
  - Home Seller Tips
excerpt:
enclosure:
pullquote:
enclosure_type: video/mp4
enclosure_time:
image:
---
````
Layout, title work the same as before. Category should remain blog unless you're making a new context. This effects the end URL. You'll notice that inside Escrow the blog posts are stored at /blog/post.html. This is personal preference and can be changed inside `_config.yml`.
[More on that.](https://jekyllrb.com/docs/permalinks/)

Tags are an extra cataloging element and work the way they do on other blogging platforms. Four are displayed, but I don't recommend having more than two. Three max or you might have them bumping lines on the post header. You can also make tags separated by comments way ie: one, two, three.

`excerpt` controls the post excerpt on the main blog page. If you delete this, it'll default to the first paragraph.

`pullquote` is the blog post pullquote. There is a prebuilt version inside `_defaults.md` that you can copy paste as needed. It's set up as a tweetable link, so be mindful of the character count.

The next three are for podcasting. `enclosure_type` is set as `video/mp4`
but for audio you can make it `audio/mpeg`. `enclosure` is the link to the audio file, `enclosure_time` is the length of the audio or video file for itunes.

`image` is important, this should be a video screenshot or a photo of some kind. It'll default to the twittercard otherwise, which should just be the logo.

It should be noted that to control the date for blog posts you add a `date:` in the front matter. It needs to be in this format: `'2016-03-21 08:00:00 -0600'` or `YYYY-MM-DD HH:MM:SS` respectively.

## Screenshots:

Main Page:

![Main Page](http://i.imgur.com/4lids74.jpg)

About Page:

![About Page](http://i.imgur.com/5nRTyRg.jpg)

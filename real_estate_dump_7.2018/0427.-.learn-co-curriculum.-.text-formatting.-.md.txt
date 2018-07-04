# Text Formatting

### Cloning Down Your Repository

If you already have a personal repository:

* Open the Learn IDE, and in the terminal, type

```
git clone https://github.com/<your_username_here>/exceptional-realty
cd exceptional-realty
git fetch --all
git checkout main-pages
```

* A folder with your previous work will appear in the IDE file tree, all
  remote branches will be retrieved, and you will then switch to the
  `main-pages` branch we started in the previous lesson.

If you want to use the demo repository to follow along:

```
git clone https://github.com/learn-co-curriculum/exceptional-realty-demo
cd exceptional-realty-demo
git fetch --all
git checkout text-formatting
```

**Remember to use `httpserver` to live test your webpage**

<iframe width="640" height="480" src="//www.youtube.com/embed/toswcv5oj9I?rel=0&modestbranding=1" frameborder="0" allowfullscreen></iframe>

<p><a href="https://www.youtube.com/watch?v=toswcv5oj9I">Text Formatting</a></p>

**Note that you may see some fancy autocomplete actions in this video**. Many
of these shortcuts are dependent on specific text editors, in this case,
Sublime. While it is good to learn that these exist, they are not critical to
completing these lessons. Often, as a new programmer, taking the time to write
out content manually can be very beneficial, so don't worry if you're not able
to get these to work.

### Starting Out

This lesson is all about formatting text in HTML. Let's start
off by typing `Hello World` inside the `<body>` tags, since we know from the
previous lesson that all viewable page content is in the `<body>`. Open 
`index.html` in your browser or start up `httpserver` and check out your
website. You should see the new text displayed on the page (if you don't, 
make sure to hit 'refresh').

Cool, we've got text on the page! Go back to your editor, and hit `return`
twice so you're two lines below `Hello World`, and type `Hello Moon`. 
Great, but very plain. In order to actually format text, we will need to
use HTML elements.

#### `<p>`

On the same line as `Hello World`, right before, add `<p>`, and immediately
following, `</p>`. If you do the same for `Hello Moon`, then refresh, on
your web page, you should notice a change. The `<p>` stands for _paragraph_,
and is used to wrap text with some built in formatting rules. Always make sure
to close your tags - if you've left a tag open, subsequent tags may be
interpreted by the browser as _nested_ within the first tag.

#### `<h1>`, `<h2>`, `<h3>`, `<h4>`, `<h5>`, and `<h6>`

Aside from paragraphs, it would be nice to be able to indicate headings and
subheadings in our page. The way we do this is by using _heading_ tags, written
from largest to smallest as `<h1>` down to `<h6>`. Headings are useful for
search engine optimization, with the largest heading, `<h1>`, carrying the
highest importance to search engines.

Above our `<p>` tags, inside `<body>`, write `Exceptional` within opening and
closing `<h1>` tags, and then, on the next line, a smaller subheading that says
`Realty Group` using `<h2>`. If we save and look at the HTML in our browser,
refreshing the page, we can see that 'Exceptional' is much larger as an `<h1>`
heading.

This page will serve as our 'About' page as well as our homepage, so we would
want to include some text on this page introducing the Exceptional Realty
Group. For now, we can put in filler text to help visualize the look of the
page.

```
<body>
  <h1>Exceptional</h1>
  <h2>Realty Group</h2>

  <p>
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
  </p>
  <p>
    Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
  </p>
</body>
```

With this, we can move on to another page on our site, but first, if you are
working from your own repository, this is a great point to push our work up
to the remote.

```
git add .
git commit -m 'add body content to index.html'
git push
```

#### Creating `real-estate-listings.html`

The second HTML page we will make requires a lot of the same basic structure,
and enough that developers will often use built-in text editor shortcuts or
copy and paste from previously written pages. We can go ahead and copy the
structure of our `index.html` file. The only parts we need to change
will be the visible content inside `<body>` and, our `<title>` content.

We'll use a similar title structure as before and this time, replacing 'About'
with 'Listings', and use the same two headings we wrote
in `index.html`.

This time, instead of paragraph tags, let's add an `<h3>` with 'Property
Archive' as the heading content, and below we'll add in a `<h4>` tag for 2014. 
Our page should look like:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - Listings</title>
  </head>
  <body>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>

    <h3>Property Archives</h3>
    <h4>2014</h4>

  </body>
</html>
```

Before moving on, now that we've got two pages worth of content, if you're
working from your own repository, add, commit and push to your remote
repository again.

```
git add .
git commit -m 'started real-estate-listings.html'
git push
```

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/text-formatting' title='Text Formatting'>Text Formatting</a> on Learn.co and start learning to code for free.</p>

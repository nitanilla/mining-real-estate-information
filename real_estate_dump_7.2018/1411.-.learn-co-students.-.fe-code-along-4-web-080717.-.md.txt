# CSS Page Layout Code Along

## Overview

Building upon previous code alongs, in this exercise you will add column structure to your page layouts by coding along with the video provided. This will help you to review the concepts you were introduced to in the previous lessons.

## Instructions

1. Fork this repository.
2. Use Terminal to clone your forked copy.
3. Then change directory into the repository folder.
4. Code along with the provided video below and/or its supplementary reading located below the video. Code everything you see there. Feel free to stop, pause, rewind or fast forward through the content to keep pace.

<iframe width="100%" height="720" src="//www.youtube.com/embed/zZpAqtEXse0?rel=0&amp;controls=1&amp;showinfo=1" frameborder="0" allowfullscreen></iframe>

### Building Layouts

Lets start out by making a new feature branch in Terminal by typing `git checkout -b columns` and press return.

Next, open the index.html page in your code editor. Scroll down to the section with the id of "promotional" and let's create a new section beneath it with an id of "news".

```html
<section id="promotional">...</section>

<section id="news">...</section>
```

Inside of this news section insert an `<h3>` and a paragraph with some placefiller text.

```html
<section id="news">
  <h3>Company News</h3>
  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Voluptatum, inventore, vero, rerum ullam nihil sapiente tempora molestias quis ducimus opsum laborum vel. Tempore perspiciatis ea error dignissimos libero recesandae explicabo.</p>
</section>
```

What we are aiming to do here is that we will size the promotional section to take up two-thirds of the page and the news section will take up one-third. These two sections will display side by side as columns. Below in the details section we have three divs and each of these will also become a column that spans one-third.

Let's head up to the top of this file and add some more elements. In the `<header>` at the top of the index page let's wrap the `<div id="logo">` and `<nav>` inside another `<div class="wrapper">`.

```html
<header>
  <div class="wrapper">
    <div id="logo">
      <h1>Exceptional</h1>
      <h2>Realty Group</h2>
    </div>
    <nav>
      <a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
    </nav>
  </div><!-- .wrapper -->
</header>
```

The "wrapper" class is going to help us to center content in a common parent element. let's add afew more wrappers. Open a wrapper div just below the closing `</header>` element. And we will close the wrapper div just before the starting `<section id="details">`.

```html
</header>

<div class="wrapper">
  <section id="featured-property">...</section>
  
  ...
  
  <section id="news">...</section>
</div><!-- .wrapper -->

<section id="details">...</section>
```

Lastly, we will add a wrapper div within the details section.

```html
<section id="details">
  <div class="wrapper">
     
     ...
     
  </div><!-- .wrapper -->
</section>
```

Don't forget to properly indent all the elements that are nested within our new wrappers. Then save the index file and open the style.css file in your code editor.

We will start by adding a comment at the bottom of our CSS file.

```css
/*////////// LAYOUT //////////*/
```

Then below create a slector for our wrapper class.

```css
/*////////// LAYOUT //////////*/

.wrapper {
  width: 960px;
  margin: 0 auto;
  background: #eee;
}
```

Here we gave it a fixed width and centered it by giving it auto margin on the left and right. I also gave it a light gray background color just for the sake of seeing the wrapper. We will end up removing this later on and put some nicer looking background styling in. Save the page and head back to the browser and refresh. You should see the wrapper centering our content.

Next lets create some classes for some columns.

```css
/*////////// LAYOUT //////////*/

.wrapper {
  width: 960px;
  margin: 0 auto;
  background: #eee;
}

.col-1 {
  /* this column will span one-third */
}

.col-2 {
  /* this column will span two-thirds */
}

.col-3 {
  /* this column will span all the entire wrapper */
}
```

Next let's set all the columns to float, that way they will position themselves side by side each other. Then we will set a width on each element. To calculate the width let's start with the columns that span one-third of the wrapper. Since we are using percentages we can assume we have 100% of space inside the wrapper. Then we subtract any margin between the columns. Since we have 2% margin between the first and second column and another 2% between the second and third column, that makes 4% total. 100% minus 4% margin equals 96% left over. then we can divide the 96% by 3 (for the three columns) to get a width of 32% for each column (col-1). To figure out the width of the column that stretches two-thirds we can take 100% minus a single one-third column 32% minus 2% margin between them equals a width of 66% for the two-thirds column (col-2). Then we will set a background color for now just so we can see them. Later on we will remove the background color to provide nicer styling.

```css
.col-1 {
  float: left;
  width: 32%;
  background: #ccc;
}

.col-2 {
  float: left;
  width: 66%;
  background: #ccc;
}

.col-3 {
 background: #ccc;
}
```

Now we need to set margin on the columns. A common strategy is to set a left margin for all columns except for the first one. To do so we can write an attribute selector to select any element that has the characters "col-" in its class name. This will select all of our columns for us regardless of the number on the end of its class name. then we can create a class called `first` to remove left margin for any first column in a row.

```css
.col-1 {
  float: left;
  width: 32%;
  background: #ccc;
}

.col-2 {
  float: left;
  width: 66%;
  background: #ccc;
}

.col-3 {
 background: #ccc;
}

[class*="col-"] {
  margin-left: 2%;
}

.first {
  margin-left: 0;
}
```

Now save this file. Great! We have written some very basic column classes. It will do the trick for our unique website, but if you are interested to see some CSS code that will be more universally usable for many more websites after this exercise you can check you out a [CSS grid system I created here](https://github.com/jongrover/css-light-grid). You can also observe [960 grid](http://960.gs/), [Bootstrap](http://getbootstrap.com/), or [Foundation's](http://foundation.zurb.com/) grid system. Because this was so much effort, in the wild most front-end developers will download and use someone elses prebuilt CSS grid system code.

Next we need to head back over to the index.html page in our code editor and add these new column classes to our HTML elements. First we will head to our featured property section and give it a class of `col-3` and also a class of first since it is the first and only column in this row. Remember the class of first will prevent any margin on the left side of the column so it will sit against the edge of the wrapper.

```html
<div class="wrapper">
  <section id="featured-property" class="col-3 first">
    ...
  </section>
  ...
```

Putting a space between the class names `col-3 first` is sufficient to apply more than one class to the same element.

Next in the promotional and news sections we will give the promotional section a class of `col-2` and `first`, then the news section we'll give a class of `col-1`.

```html
  <section id="promotional" class="col-2 first">
    ...
  </section>
  
  <section id="news" class="col-1">
    ...
  </section>
```

Finally in the details section we will give each div a class of `col-1` and of course the first one we'll include the class of first also.

```html
<section id="details">
  <div class="wrapper">
    <div class="col-1 first">
      <h3>Contact</h3>
      ...
    </div>
    <div class="col-1">
      <h3>Links</h3>
      ...
    </div>
    <div class="col-1">
      <h3>Follow</h3>
      ...
    </div>
  </div><!-- .wrapper -->
</section>
```

Save the index file. Ok, so remember in the previous lessons we discussed using clearfixes to prevent a parent from collapsing when all of its children are floating. We will need this for a few of our wrappers where all of the elements within them are now floating columns.

To start add this clearfix code to the bottom of your CSS file:

```css
.clearfix:after {
  content: ".";
  display: block;
  clear: both;
  visibility: hidden;
  height: 0;
  line-height: 0;
}
```
Don't forget to save the CSS page. If you're still a bit puzzled by this, there is much more detail on this snippet of code in previous lessons. 

Next we will apply this clearfix to some of our wrappers in the index page such as the main wrapper that wraps the sections such as featured property, promotional, and news sections.

```html
<div class="wrapper clearfix">
  <section id="featured-property" class="col-3 first">
    ...
  </section>
  ...
```

and also apply the clearfix in the details section:

```html
<section id="details">
  <div class="wrapper clearfix">
    ...
  </div><!-- .wrapper -->
</section>
```

Lets save and open the index page in the browser to se the column structure. Looks pretty good, but the video element is sticking outside of the column. To fix this head back to your CSS file.

```css
/*////////// MEDIA //////////*/

img, video, audio {
  max-width: 100%;
}
```

This will allow the images, videos, and any audio player content to expand and only take up 100% of the parent columns width. Save the CSS file and go back to the index page in the browser and we can see it looks much better!

Next we will hop back into the CSS file and give the sections some additonal styling.

```css
/*////////// SECTIONS //////////*/

section {
  padding: 20px;
  margin-bottom: 20px;
}
```

This will add some spacing inside our section elements. Save this file and go back to the index page in the browser and refresh. The content is now padded from the edge of our sections, but this additional padding is added to the width of our columns and now some of the columns no longer fit side by side. We can fix this by setting the browser to use the IE box model instead where padding is included in the set width automatically. Back in our CSS file add the following code:

```css
/*////////// LAYOUT //////////*/

* {
  -webkit-box-sizing: border-box;
  -moz-box-sizing: border-box;
  box-sizing: border-box;
}
```

Here we set all elements (using the universal selector `*`) to size themselves using border-box where all borders and padding will be included in the width set on elements. We used the `-webkit` and `-moz` prefixes to get this to work in older browsers as well. Now save the CSS file and head back to the index page in the browser and refresh. All the columns should be positioning as normal now.

Next let's create a fixed social media bar that will stay in place while we scroll. head back to the index.html page in your code editor. Just inside the opening body tag let's build a new div for our social icon bar.

```html
<body>
  <div id="social">
    <a href="#">Twitter</a>
    <a href="#">Facebook</a>
    <a href="#">Google Plus</a>
  </div>
```

These text links will be replaced with icons in a future code along. For now head over to your CSS file and add some positioning.

```css
#social {
  position: fixed;
  top: 200px;
  right: 20px;
  width: 40px;
  z-index: 1;
}

#social  a {
  display: block;
  width: 40px;
  height: 40px;
  background: yellow;
}
```

Save your CSS file and head back to your index page in the browser and refresh the page. You should see the social icon bar appears at the left side of the screen and stays fixed in place even when we scroll. As mentioned before we will come back to this in a later code along and swap out these ugly yellow squares with real icons. Until then quack quack said the yellow squares.

While we are setting things to fixed positioing let's also apply this to the header at the top of the page so that when we scroll down the page the top navigation will always stay in view. Back in our CSS file add the following code:

```css
/*////////// SECTIONS //////////*/

header {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: #fff;
  z-index: 1;
}
```

While we are in our CSS file let's remove some of the background colors from before. Start by removing the aqua background color from the `#logo` selector:

```css
#logo {

}
```

and also remove the gray color from our wrapper class:

```css
.wrapper {
  width: 960px;
  margin: 0 auto;
}
```

Save the CSS file and head back to the browser and refresh the index page. Scroll to see the header stay in place.

It's now time to version our changes using Git. To do so, in Terminal type `git add .` and press return. Then type `git commit -m "add columns and fixed header and social bar"` and press return. Then push up this feature branch `git push -u origin columns` and press return. Next merge the changes into your master branch. Type `git checkout master` and press return, then `git merge columns` and press return. Then `git push origin master` and press return.

After you finish, make sure you install Firefox if you haven't already as it is required for the screenshot tests to run. Then, type `learn` command from Terminal to run local tests (Mac) or type `learn-test` for Windows.

After all tests are passing submit a pull request on Github and move on to the next lesson!

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/fe-code-along-4' title='Code Along Exercise 4'>Code Along Exercise 4</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/fe-code-along-4'>Code Along Exercise IV</a> on Learn.co and start learning to code for free.</p>

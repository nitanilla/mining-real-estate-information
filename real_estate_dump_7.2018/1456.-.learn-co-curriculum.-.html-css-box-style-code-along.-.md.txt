# Box Style Code Along

## Objectives

1. Review CSS Background property
2. Review CSS Box Shadow
3. Review CSS Gradient backgrounds.

## Introduction

Building upon previous code alongs, in this exercise you will add styling to the the backgrounds of your page elements by coding along with the video provided. This will help you to review the concepts you were introduced to in the previous lessons.

## Instructions

1. Fork this repository.
2. Use Terminal to clone your forked copy.
3. Then change directory into the repository folder.
4. Code along with the provided video below and/or its supplementary reading located below the video. Code everything you see there. Feel free to stop, pause, rewind or fast forward through the content to keep pace.

*Note: The gradient code that is copied and pasted in teh video is located below the video as code snippets as well.*

<iframe width="100%" height="720" src="//www.youtube.com/embed/Y4El1I-hagQ?rel=0&controls=1&showinfo=1" frameborder="0" allowfullscreen></iframe>

The gradient code that is copied and pasted in the exercise video is available here:

```css
/* LIGHT-FADE */
  background: #efefef; /* Old browsers */
  background: -moz-linear-gradient(top,  #efefef 0%, #ffffff 24%, #ffffff 68%, #dddddd 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#efefef), color-stop(24%,#ffffff), color-stop(68%,#ffffff), color-stop(100%,#dddddd)); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* IE10+ */
  background: linear-gradient(to bottom,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* W3C */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#efefef', endColorstr='#dddddd',GradientType=0 ); /* IE6-9 */
```

```css
/* MEDIUM-FADE */
  background: rgb(229,229,229); /* Old browsers */
  background: -moz-linear-gradient(top,  rgba(229,229,229,1) 0%, rgba(255,255,255,1) 99%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(229,229,229,1)), color-stop(99%,rgba(255,255,255,1))); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* IE10+ */
  background: linear-gradient(to bottom,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* W3C */
```

```css
/* NAVBAR-HOVER */
  background: rgb(0,0,0); /* Old browsers */
  background: -moz-linear-gradient(top,  rgba(0,0,0,1) 0%, rgba(71,71,71,1) 28%, rgba(81,81,81,1) 35%, rgba(71,71,71,1) 72%, rgba(43,43,43,1) 87%, rgba(28,28,28,1) 91%, rgba(0,0,0,1) 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(0,0,0,1)), color-stop(28%,rgba(71,71,71,1)), color-stop(35%,rgba(81,81,81,1)), color-stop(72%,rgba(71,71,71,1)), color-stop(87%,rgba(43,43,43,1)), color-stop(91%,rgba(28,28,28,1)), color-stop(100%,rgba(0,0,0,1))); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* IE10+ */
  background: linear-gradient(to bottom,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* W3C */
```

### Styling The Backgrounds

Lets start out by making a new feature branch in Terminal by typing `git checkout -b navbar-and-background-styles` and press return. 

Next, bring up the style.css file in your code editor. Start by removing the background colors from our column classes. Scroll down to the area of the code with the comment label for "LAYOUT".

```css
/*////////// LAYOUT //////////*/

.col-1 {
  float: left;
  width: 32%;
}

.col-2 {
  float: left;
  width: 66%;
}

.col-3 {

}

```

Next, in the part of the code labeled "GLOBAL" scroll to below the milk-text class add the following code:

```css
/*////////// GLOBAL //////////*/

...

.shadow {
  box-shadow: 0 3px 10px #333;
}
```

Here we specified a `box-shadow` which will add a drop shadow to any elements we apply this class to. 

Then save the CSS page and open the index.html page in your code editor. Under the section with the id of "featured-property" lets apply our shadow class.

```html
...
<div class="wrapper clearfix">

  <section id="featured-property" class="col-3 first shadow">
    ...
```

We will also add this class of shadow to the promotional and news sections.

```html
  <section id="promotional" class="col-2 first shadow">
```

```html
  <section id="news" class="col-1 shadow">
```

Make sure to save the index page and then jump backover to the style.css page (still in code editor). Now we will create a new class called border-right in the bottom of the "GLOBALS" portion of the page.

```css
/*////////// GLOBAL //////////*/

...

.shadow {
  box-shadow: 0 3px 10px #333;
}

.border-right {
  border-right: 1px sdotted #ccc;
  padding-right: 30px;
}
```

Save the CSS file and jump back over to our index page and apply this class to the first two divs within the details section at the bottom of the page.

```html
<section id="details">
  <div class="wrapper clearfix">
    <div class="col-1 first border-right">
       ...
    </div>
    <div class="col-1 border-right">
       ...
    </div>
    <div class="col-1">
       ...
    </div>
  </div><!-- .wrapper -->
</section>
```

Then save the page and refresh in the browser you should see some light gray dotted borders for the columns in the details section. next, head back to style.css in the code editor and we will add some more styles in the protion of the code labeled with the comment "BACKGROUNDS".

```css
/*////////// BACKGROUNDS //////////*/

.white-wood {
  background: url(../images/white-wood.jpg) no-repeat center top;
  background-size: cover;
}
```

Save the css page and head back over to the index page and add a new opening div above the `<header>` element with the class of `white-wood`.

```html
<div class="white-wood">
  <header>
    ...
  </header>
  ...
  <div class="wrapper clearfix">
    <section id="featured-property">...</section>
    <section id="promotional">...</section>
    <section id="news">...</section>
  </div><!-- .wrapper -->
</div><!-- white-wood -->
```

Don't forget to properly indent all the content inside our new white-wood div. Now save the page and preview in the browser and you should see the white wood texture appear behind all the main sections.

Next head back over to the style.css file in your code editor and we will add some white backgrounds to our section elements.

```css
/*////////// MAIN SECTIONS //////////*/

section {
  padding: 30px;
  margin-bottom: 20px;
  background: white;
}
```

Save this page and refresh the index page in the browser to see the change. The sections should now appear white on top of the wood texture.

Next we will work on creating some nice gradient backgrounds in the header, details section, and footer. head to the "BACKGROUNDS" protion of the page in the style.css file and add the code for the following gradient background classes.

```css
.light-fade {
  background: #efefef; /* Old browsers */
  background: -moz-linear-gradient(top,  #efefef 0%, #ffffff 24%, #ffffff 68%, #dddddd 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,#efefef), color-stop(24%,#ffffff), color-stop(68%,#ffffff), color-stop(100%,#dddddd)); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* IE10+ */
  background: linear-gradient(to bottom,  #efefef 0%,#ffffff 24%,#ffffff 68%,#dddddd 100%); /* W3C */
  filter: progid:DXImageTransform.Microsoft.gradient( startColorstr='#efefef', endColorstr='#dddddd',GradientType=0 ); /* IE6-9 */
}

.medium-fade {
  background: rgb(229,229,229); /* Old browsers */
  background: -moz-linear-gradient(top,  rgba(229,229,229,1) 0%, rgba(255,255,255,1) 99%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(229,229,229,1)), color-stop(99%,rgba(255,255,255,1))); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* IE10+ */
  background: linear-gradient(to bottom,  rgba(229,229,229,1) 0%,rgba(255,255,255,1) 99%); /* W3C */
}
```

Then save the CSS file and head over to the index page and apply the `medium-fade` and `shadow` classes to the `<header>`.

```html
<header class="medium-fade shadow">
```

Then, apply the class of `light-fade` to the `<div id="navbar">`.

```html
<header class="medium-fade shadow">
  <div class="wrapper">
    <div id="logo">...</div>
  </div><!-- .wrapper -->
  <div id="navbar" class="light-fade">
    ...
  </div>
</header>
```

Then scroll down to the details section and apply a class of medium-fade.

```html
<section id="details" class="medium-fade">...</section>
```

Then save the index file and refresh it in the browser to see the new gradient backgrounds. Next, we will update the styles on the navigation bar at the top of the page. In your code editor bring up the style.css file. Scroll down to the "HEADER" comment in the code and add the following styles.

```css
/*////////// HEADER //////////*/

header {
  margin: 0 0 30px;
}
```

Then in the "NAVBAR" comment in the code and add the following styles.

```css
/*////////// NAVBAR //////////*/

#navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 2;
  border-bottom: 1px solid #ccc;
  text-align: center;
}

#navbar nav {
 border-left: 1px solid #ccc;
}

#navbar nav a {
  display: inline-block;
  width: 16.6666667%;
  margin: 0;
  padding: 22px 0;
  text-transform: uppercase;
  color: black;
  text-align: center;
  border-right: 1px solid #ccc;
  text-decoration: none;
  font: 1em "Trebuchet MS", Arial, sans-serif;
}

#navbar nav a.selected {
  background: #333;
  color: white;
}
```

Save the CSS file and then apply the class of selected to the first link in the nav of the index page.

```html
<nav>
  <a href="index.html" class="selected">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
</nav>
```

Go to each of the pages and add the class of selected for each link that represents that page so on the contact.html page the contact link should have the class of selected applied instead.

Save these files, and then back in the CSS lets add a hover state style

```css
/*////////// NAVBAR //////////*/

...

#navbar nav a:hover {
  color: white;
  background: rgb(0,0,0); /* Old browsers */
  background: -moz-linear-gradient(top,  rgba(0,0,0,1) 0%, rgba(71,71,71,1) 28%, rgba(81,81,81,1) 35%, rgba(71,71,71,1) 72%, rgba(43,43,43,1) 87%, rgba(28,28,28,1) 91%, rgba(0,0,0,1) 100%); /* FF3.6+ */
  background: -webkit-gradient(linear, left top, left bottom, color-stop(0%,rgba(0,0,0,1)), color-stop(28%,rgba(71,71,71,1)), color-stop(35%,rgba(81,81,81,1)), color-stop(72%,rgba(71,71,71,1)), color-stop(87%,rgba(43,43,43,1)), color-stop(91%,rgba(28,28,28,1)), color-stop(100%,rgba(0,0,0,1))); /* Chrome,Safari4+ */
  background: -webkit-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* Chrome10+,Safari5.1+ */
  background: -o-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* Opera 11.10+ */
  background: -ms-linear-gradient(top,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* IE10+ */
  background: linear-gradient(to bottom,  rgba(0,0,0,1) 0%,rgba(71,71,71,1) 28%,rgba(81,81,81,1) 35%,rgba(71,71,71,1) 72%,rgba(43,43,43,1) 87%,rgba(28,28,28,1) 91%,rgba(0,0,0,1) 100%); /* W3C */
}
```

Save the CSS file and head back to the browser and refresh. You'll notice that the links are a bit jumbled. This is because we set them to `display: inline-block;` one thing to note about inline and inline-block elements are that white space around the characters is seen as a physical keyboard space the same as it is seen when you add spaces between words in a sentence; where as white space is ignored when surrounding block elements for example. To fix this lets remove the keyboard space between the links in the nav bars of our pages.

```html
<nav>
  <a href="index.html" class="selected">About</a><a href="new-properties.html">New Properties</a><a href="real-estate-listings.html">Listings</a><a href="market-report.html">Market Report</a><a href="contact.html">Contact</a><a href="http://hud.gov" target="_blank">H.U.D.</a>
</nav>
```

Than save and refresh in the browser. Just a few more things to fix up. You will notice that since we fixed the nabvbar the logo div is sliding up behind it and covering the top half. To fix this lets apply some padding to the `#logo` selector in our css file as well as remove the margin on our `h1` and `h2` inside the `#logo`.

```css
/*////////// LOGO //////////*/

#logo {
  padding: 84px 0 0;
}

#logo h1 {
  font-family: 'Clicker Script', cursive;
  margin: 0;
}

#logo h2 {
  font-family: 'Elsie Swash Caps', cursive;
  margin: 0;
}
```

Next in the details section we will add a border on the top of the details section to highlight the separation betwene the wood and the details gradient

```css
/*////////// DETAILS //////////*/

#details {
  border-top: 1px solid white;
}

```

Now for some styling on the footer section,

```css
/*////////// FOOTER //////////*/

footer {
  text-align: center;
  font-size: 0.75em;
  padding: 10px;
  background: #eee;
  border-top: 1px solid #ccc;
}
```

Now save the CSS file and refresh in the browser. Excellent starting to look more like a professional website.

It's now time to version our changes using Git. To do so, in Terminal type `git add .` and press return. Then type `git commit -m "style backgrounds for section, navbar, and details"` and press return. Then push up this feature branch `git push -u origin navbar-and-background-styles` and press return. Next merge the changes into your master branch. Type `git checkout master` and press return, then `git merge navbar-and-background-styles` and press return. Then `git push origin master` and press return.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/fe-code-along-ex-5' title='Code Along Exercise 5'>Code Along Exercise 5</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/html-css-box-style-code-along'>Box Style Code-Along</a> on Learn.co and start learning to code for free.</p>

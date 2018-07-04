# HTML5 Semantic Containers Code Along

## Objectives

1. Surround existing content with HTML5 Semantic Elements

## Introduction

Building upon previous code alongs, in this exercise you will add HTML5 Semantic Elements by coding along with the video provided, reviewing the concepts you were introduced to in the previous lessons.

## Instructions

- Fork this repository on Github.
- Use Terminal to clone your forked copy.
- Then change directory into the repository folder.
- Code along with the provided video below and/or its supplementary reading located below the video. Code everything you see there. Feel free to stop, pause, rewind or fast forward through the content to keep pace.

<iframe width="640" height="480" src="//www.youtube.com/embed/xrDw6I4MSBk?rel=0" frameborder="0" allowfullscreen></iframe>

### Semantic Elements

To get started create a feature branch in Terminal by typing `git checkout -b html5-layout` and press return. Then open the index.html file in your code editor.

#### Header

Start by surrounding your `<h1>` and `<h2>`, as well a the `<a>` links of your main navigation in a `<header` element like so,

```html
<body>
  <header>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>

    <a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
  </header>
```

On line 2 the `<header>` element gives importance to the content within it, defining that the content as the head of our document.

#### Nav

Next let's wrap our links in the `<nav>` element like so,

```html
<body>
  <header>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <nav>
      <a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
    </nav>
  </header>
```

On line 5 our `<nav>` element semantically represents the navigation area of this page. Looking good!

#### Section

Next we will section off our page by adding a `<section>` element wrapping our `<img>` image and `<p>`paragraphs like so,

```html
...
  </header>
  <section id="featured-property">
    <img src="images/intro-pic.jpg" alt="A beautiful living room." title="Welcome to Exceptional Realty Group">
    <p>Lorem ipsum dolor sit amet...</p>
    <p>Lorem ipsum dolor sit amet...</p>
  </section>
```

Note that we gave our section an id of `featured-property` on line 3 of the snippet above. Make sure to properly indent all the content images, and paragraphs that have been nested within the section element.

Continuing on we will insert the next section with an id of `promotional` surrounding the promotion video like so,

```html
  ...
  <section id="promotional">
    <video controls>
      <source src="videos/real-estate.mp4" type="video/mp4">
      <source src="videos/real-estate.ogv" type="video/ogg">
      Your browser does not support HTML5 video. <a href="http://browsehappy.com" target="_blank">Please upgrade your browser</a>.
    </video>
  </section>
````

#### Footer

At the bottom of the page before the closing `</body>` tag lets create a `<footer>` element and insert some copyright information.

```html
...
  <footer>
    &copy; 2014 Exceptional Realty Group. All Rights Reserved.
  </footer>
</body>
```

On line 3 we used `&copy;` the html name for the ascii character for the `©` symbol.

#### Figure and Figcaption

Next we can surround our image and media content with `<figure>` element and insert a `<figcaption>` within to include a caption about the media content. We'll start with our `<img>` image element.

```html
  <section id="featured-property">
    <figure>
      <img src="images/intro-pic.jpg" alt="A beautiful living room." title="Welcome to Exceptional Realty Group">
      <figcaption>345 Carl Street Apt 12, Carrol Rd. Brooklyn, NY - photo by Denise Richards</figcaption>
    </figure>
  </section>
```

On line 2 we included our `<figure>` element which wraps our image and sets it out as something that is usually a picture, illustration, diagram, code snippet, or schema that is referenced in the main text of the page. Inside it on line 4, we included a `<figcaption>` element calling out the text as a caption for the figure it is held within.

Now add another surrounding our video player.

```html
  <section id="promotional">
    <figure>
      <video controls>
        <source src="videos/real-estate.mp4" type="video/mp4">
        <source src="videos/real-estate.ogv" type="video/ogg">
        Your browser does not support HTML5 video. <a href="http://browsehappy.com" target="_blank">Please upgrade your browser</a>.
      </video>
      <figcaption>Exceptional Realty Group Promotional Video - Source: archive.org</figcaption>
    </figure>
  </section>
```

Don't forget to indent the content such as the video and image that are nested inside of our `<figure>` elements. Then you can save this file and give it a preview in the browser. Since we just surrounded the preexisting content it won't look too different, although the HTML5 semantic elements do act as boxes that will stack vertically giving some separation between each and the figures do have some default spacing that will indent the video and image a bit.

Normally you would add these HTML5 semantic elements where applicable to all of your site pages. I will add these to the other pages for you and the next code along will already have them present in its starter code. We just did it on the index page for some practice. Nice work!

It's now time to version our changes using Git. To do so, in Terminal type `git add index.html` and press return. Then type `git commit -m "add semantic containers to index"` and press return. Then push up this feature branch `git push -u origin html5-layout` and press return. Next merge the changes into your master branch. Type `git checkout master` and press return, then `git merge html5-layout` and press return. Then `git push origin master` and press return.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/html5-semantic-containers-code-along' title='HTML5 Semantic Containers Codealong'>HTML5 Semantic Containers Code along</a> on Learn.co and start learning to code for free.</p>

<p class='util--hide'>View <a href='https://learn.co/lessons/html5-semantic-containers-code-along'>HTML5 Semantic Elements Code Along</a> on Learn.co and start learning to code for free.</p>

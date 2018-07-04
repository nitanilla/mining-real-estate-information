# Introduction to CSS Lab

## Objectives

1. Practice linking an external CSS file
2. Practice writing selectors
3. Practice styling our HTML

## Introduction

In this lab, we will be adding style to our `index.html` page by linking an
external CSS file. If you open `index.html` in the browser (by either opening
the file with Google Chrome or running `httpserver` on the Learn IDE), you will
see basic HTML that has been provided. The website emulates a basic Real Estate
website (the links on it have been disabled, we will be working with only the
basic `index.html` landing page).

As you can see, our basic page is rather lackluster. This is where you come in!
You will be adding CSS, using selectors, to jazz the page up. All of our CSS
should be written in `style.css`.


## Import our CSS

As usual, we need to make sure our HTML is loading our stylesheet.

We have two options:

1. Write CSS rules inside of a `<style>` tag ("internal CSS"), which tells HTML
   "Hey, I want to define some CSS styling here
2. Write CSS rules in an external file that is specified with the `<link>` tag
   ("external CSS").

In our case, we want to provide a link to our stylesheet, instead of writing
all of our CSS code directly in the  `<style>` tag. This allows us to only have
to write styles for the entire site once, instead of repeating every `<style>`
element on every page.  A common workflow is to see developers work on CSS
inside of the `<style>` tag until their styling is done. At that point they
move it to their external file and remove the `<style>` element from the HTML
page. Feel free to try it out!

In `index.html`, provide a `<link>` tag which correctly sources the CSS file
located in this directory. The `<link>` tag will link to our file with an
`href` attribute, like so:

```HTML
<link rel="stylesheet" href="relative path to CSS file">
```

Links to stylesheets should go at the end of the `<head>` section! Make sure
you provide a _relative_ path to the stylesheet.

Hint: Try adding the following temporarily to your `style.css` file to test if
your linked CSS is working:

```CSS
h1 {
  color: red;
}
```

If you see your `<h1>` change to red, you've linked your stylesheet correctly!
Don't forget to delete it once you have your link working.

## Deliverables

For this exercise, we are going to be transforming our base HTML into a more
exciting version using CSS.

It is important to note that there are _many_ ways to go about transforming the
HTML with CSS to match the end product. For this lesson, we will provide you
with general guidance in _one way_ of getting to the desired view by adding to
the `style.css`. Ultimately, the goal is to have your website look like the
finished product whatever way works the best for you.

**Note:** If you are having trouble finding the specific CSS property you need
to get a specific visual outcome, use your Google-Fu with queries such as: "CSS
center text within div".

In following the guidelines, you should be referencing the `index.html` to find
the appropriate tags/IDs that we will use as selectors in our `style.css` file.
Don't forget: you can use the Chrome Inspector Tool (`cmd  + shift + C` on Mac)
to inspect specific elements of the DOM (and make trial changes to their CSS) in
the browser.

#### What We Have

![](https://curriculum-content.s3.amazonaws.com/fewds-css/css-fundamentals-lab-incomplete.png)

#### What We Want

![](https://curriculum-content.s3.amazonaws.com/fewds-css/css-fundamentals-lab-complete.png)


## Deliverables

- **Update the header**: the text is a little wonky being aligned on the left like that. Provide a property that aligns it in the center instead

- **Center our image**: We only have one image on the page and we would like it centered!

- **Jazz up our navigation links**: Let's center all of our nav links as well. Give all of the `<a>` tags within our navbar a padding of 10px on their left and right sides. In addition, change their background color to something of your choosing. We chose grey!

- **Our image caption needs work**: Let's shrink that font size down and make sure it is centered.

- **Update the text block**: Wouldn't it look nicer if our text was centered as well? Our image is about 900px wide, so let's give all our `<p>` within `#featured-property` a hard width of 800px and center the text in there.

- **Make our `#details` section horizontal**: The details section could go nicely as a footer to the page, instead of a vertical list. Change its `display` value to block and make sure each of the `<div>`s is `float`ing to the `left`.

- **As a finishing touch**: Let's clean up the `<div>`s at the bottom of the page. All of them should have the same background color, centered text, and occupy 25% of the `width` of the bottom row (since we have 4 divs).


## Conclusion

CSS allows many avenues to the same goal. The important take-away is to
experiment and become familiar with the commonly used rules. This will enable
you to identify what properties will get you to which end result quickest.

You will find that, even years into your career as a front end developer, you
will be referencing basic CSS documentation. _This is to be expected!_. To be
comfortable quickly finding the property/value you are looking for online is the
most important skillset you can develop right now. Memorization is for machines,
adaptation is for humans!

## Resources
- [W3 Introduction to CSS](https://www.w3schools.com/Css/css_intro.asp)

[unstyled]: https://curriculum-content.s3.amazonaws.com/web-development/unstyled-codepen.jpeg
[styled]: https://curriculum-content.s3.amazonaws.com/web-development/styled-codepen.jpeg

<p class='util--hide'>View <a href='https://learn.co/lessons/introduction-to-css-lab'>Introduction to CSS Lab</a> on Learn.co and start learning to code for free.</p>

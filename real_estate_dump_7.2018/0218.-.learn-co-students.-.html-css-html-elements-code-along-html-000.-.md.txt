# HTML Fundamentals Code Along

## Objectives

1. Implement document structure
2. Format text within a web page
3. Build lists within a web page
4. Build tables within a web page
5. Build images within a web page
6. Add links between pages
7. Stage and commit with Git
8. Push code with Git
8. Make a pull request on Github

## Introduction

In this exercise you will code along with the video to review the HTML fundamentals you were introduced to in the previous lesson.

## Instructions

- On this lesson's page on Learn.co, click the "Open" button — this will fork and clone the repository and open it in the IDE.
- Create a new branch called "main-pages" using the command `git checkout -b main-pages`.
- Open the files in your code editor 
- At this point in Terminal you would create any sub folders and files using the `mkdir` command and `touch` commands. We have already done this for you so you can get coding right away. In the code editor you will see we have already created the following files and folders.

```shell
├── README.md
├── contact.html
├── images
│   └── intro-pic.jpg
├── index.html
├── market-report.html
├── new-properties.html
├── real-estate-listings.html
└── spec
    └── ...
```

- Code along with the provided video below and/or its supplementary reading located below the video. Code everything you see there. Feel free to stop, pause, rewind or fast forward through the content to keep pace.

**Note** that the video uses your computer's terminal, but in this course, you'll be using the Learn IDE and all Git commands will work the same way on it as it does on your terminal.

However, the video will ask you to open files using with instructions that are specific to Sublime. Since that is not the text editor used in the IDE, please use the IDE specific commands that we've already covered.

<iframe width="640" height="360" src="https://www.youtube.com/embed/videoseries?list=PLj148bJp5wiyXRRpL8rM-cLETaClgdBK2" frameborder="0" allowfullscreen></iframe>

### Document Structure

Once you have the repository in your IDE, open up the index.html page in the text editor are. At the top of the document add the `<!DOCTYPE html>` element. This tells the browser that following HTML page is version 5 (HTML5). Many elements have both a starting and ending tag, but the "DOCTYPE" element only has a starting tag.

Next write the `<html></html>` element. This tells the browser that all code within these tags is HTML code. Inside the opening (starting) tag `<html>` let's add the attribute "lang" to specify a language. `<html lang="en">`. This tells the browser and search engines that the content is in English. To se a full list of lang codes you can explore [HTML - Lang Codes](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/).

Inside the HTML element let's devide the document up into our two main parts the `<head></head>` and the `<body></body>`. Meta data such as links to outher files, keyword search terms and other information for the browser and search engines goes inside the `<head>` and all the visible content of out page that users will see goes in the `<body>`. Your code should now look like the following code.

```html
<!DOCTYPE html>
<html lang="en">
  <head></head>
  <body></body>
</html>
```

Let's write a comment in the code that we can read and leave notes about the content but will not be seen in the browser. Comments start with a `<!--` and end with a `-->`. Comments can be written as a single line or across multiple lines of text.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
  </body>
</html>
```

Let's place some other elements in the head section, such as a meta element. Type `<meta charset="UTF-8">`. This tells the browser that the characters in the document should be interpreted as UTF-8 characters. to learn more about charsets you can refer to the link in the resources at the bottom of this lesson.

Also type a `<title></title>` element into the `<head>` section. Here we can give our document a title. This will appear on the browser tab at the top of your browser window.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
  </body>
</html>
```

Save your page in the IDE. Then open the HTML page in your browser via the IDE. 

The page is currently blank because we haven't yet inserted any content into the body yet, but we can see our title at the top of the browser tab.

### Text Formatting

Next let's type `Hello World` into the body section.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    Hello World
  </body>
</html>
```

Save the page, then head back to the browser and press Command + r on Mac, or Ctrl + r on windows to refresh the page. Now you can see your "Hello World" message in the browser window.

Next, let's look at the way white space is interpreted by the browser. Head back to your index page and press return several times after the "Hello World" text and type `Hello Moon`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    Hello World.

    Hello Moon.
  </body>
</html>
```

Save the page, then head back to the browser and press Command + r on Mac, or Ctrl + r on windows to refresh the page. You'll notice that the line returns are not being interpreted as white space, instead the text appears on the same line `Hello World. Hello Moon.`.

In order to create paragraphs with space in between we'll need to use th `<p></p>` element like so.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    <p>Hello World.</p>
    <p>Hello Moon.</p>
  </body>
</html>
```

Save the page, then head back to the browser and press Command + r on Mac, or Ctrl + r on windows to refresh the page. Now we can see that there is a full line return with white space above and below our paragraphs.

Next let's create some headings. Type an `<h1></h1>` and `<h2></h2>` above our paragraphs like so:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <p>Hello World.</p>
    <p>Hello Moon.</p>
  </body>
</html>
```

Save the page, then head back to the browser and refresh the page. Now we can see our headings. the "h1" is the largest and most important for search engines, and the h2 is slightly smaller and carries slightly less importance for search terms.

Next lets put in some place filler text to replace our previous paragraphs. In your code editor you may have shortcut commands installed. for example in Sublime Text we can type the letter `p` and the hit tab and it will autocomplete for us the `<p></p>` element and to fill it with placefiller text we can type `lorem` and hit the tab key which will produce the following:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cupiditate quas, dolore facere quis laboriosam soluta repellendus eius reiciendis nobis consequatur iusto ea aliquid! Porro, cupiditate excepturi facere ipsum? Similique, aliquam!</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cupiditate quas, dolore facere quis laboriosam soluta repellendus eius reiciendis nobis consequatur iusto ea aliquid! Porro, cupiditate excepturi facere ipsum? Similique, aliquam!</p>
  </body>
</html>
```

Save the page, then head back to the browser and refresh the page. Now we can see our place filler paragraph using auto completion. We'll learn more of these time saving tricks later on.

Next let's create a line-break in our paragraph by inserting the `<br>` element to force a new line like so:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <!-- The head section contains info for search engines and the browser and is not seen by site visitors. -->
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - About</title>
  </head>
  <body>
    <!-- The body is the entire viewable area of the web page. For example we can see text, links, images, and media. -->
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <p>Lorem ipsum dolor sit amet, <br> consectetur adipisicing elit. Cupiditate quas, dolore facere quis laboriosam soluta repellendus eius reiciendis nobis consequatur iusto ea aliquid! Porro, cupiditate excepturi facere ipsum? Similique, aliquam!</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Cupiditate quas, dolore facere quis laboriosam soluta repellendus eius reiciendis nobis consequatur iusto ea aliquid! Porro, cupiditate excepturi facere ipsum? Similique, aliquam!</p>
  </body>
</html>
```

Save the page, then head back to the browser and refresh. You can see the line now wraps after the "...sit amet", and the "consectetur..." wraps to the next line.

Next, open the real-estate-listing.html page in your code editor. Write out the same basic document structure we created in the index page including the same headingsa s before, but this time we will create some new sub headings.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - Listings</title>
  </head>
  <body>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <h3>Property Archive</h3>
    <h4>2014</h4>
  </body>
</html>
```

### Lists

Let's create an unorded list with dates for our property archive. Start with a `<ul></ul>` element like so:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - Listings</title>
  </head>
  <body>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <h3>Property Archive</h3>
    <h4>2014</h4>
    <!-- unordered list -->
    <ul>

    </ul>
  </body>
</html>
```

Inside the `<ul>` we create `<li>` elements for each date.

```html
<!-- unordered list -->
<ul>
  <li>Dec</li>
  <li>Nov</li>
  <li>Oct</li>
</ul>
```

Next we will create a sub nested list of dates for the month of Oct.

```html
<!-- unordered list -->
<ul>
  <li>Dec</li>
  <li>Nov</li>
  <li>Oct
    <ul>
      <li>17th</li>
      <li>18th</li>
    </ul>
  </li>
</ul>
```

Notice that we opened up the `<li>Oct</li>` and placed an additonal `<ul>` inside of it with its own `<li>`. This creates a sub list inside of our parent list. Go ahead and save this page and refresh in the browser and you will see bullet points for each Month name and open elipsis (bullets) for the days 17th and 18th.

We'll add a new h3 heading under out previous list and then, next let's create an ordered list below it. Ordered lists differ in that they have numbered list items instead of bulleted as they were in the unordered list. We begin by inserting a `<ol></ol>` element with some of its own `<li>` inside of it containing street addresses.

```html
<!-- ... -->

<h3>Popular Listings</h3>
<!-- ordered list -->
<ol>
  <li>384 Stockton St.</li>
  <li>3742A Belvevadere Rd.</li>
  <li>41 Cleaton Ave.</li>
</ol>
```

Go ahead and save this page and refresh in the browser and you will see this list has numbers for each list item (1 though 3).

Next, let's open up the market-report.html page in your code editor. Fill in the basic HTML document structure changing the title and using the same headings. Feel free to copy and paste the content and change what is neccessary. We will also add an `<h3>Market Report</h3>`.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Exceptional Realty Group - Luxury Homes - Market Report</title>
  </head>
  <body>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <h3>Market Report</h3>

  </body>
</html>
```

### Tables

Now we would like to insert a table that will hold data about different real estate properties and divide the information up into rows and columns. We'll start by inserting the `<table></table>` element.

```html
<!-- ... -->
<h3>Market Report</h3>
<table>

</table>
```
Inside the `<table>` we create rows by inserting the `<tr></tr>` table row element Let's create 4 separate rows.

```html
<!-- ... -->
<h3>Market Report</h3>
<table>
  <tr></tr>
  <tr></tr>
  <tr></tr>
  <tr></tr>
</table>
```

To create columns we can further divide up the rows by inserting either `<th>` table header cell or `<td>` regular table cell. The table headers are meant to label the tops of columns and the normal table cells are for separating data for each column. In the first row lets add table header cells for "Address", "City", "State", "Sales Price".

```html
<table>
  <tr>
    <th>Address</th><th>City</th><th>State</th><th>Sales Price</th>
  </tr>
  <tr></tr>
  <tr></tr>
  <tr></tr>
</table>
```

Then we will fill in some data for each real estate property within `<td>` elements for the remaining rows. We'll also format our `<th>` and `<td>` vertically so it's easier to read the code, although this will not effect the way it displays in the browser.

```html
<table>
  <tr>
    <th>Address</th>
    <th>City</th>
    <th>State</th>
    <th>Sales Price</th>
  </tr>
  <tr>
    <td>2345 Fairview Ln.</td>
    <td>Brooklyn</td>
    <td>NY</td>
    <td>$1.2 mil</td>
  </tr>
  <tr>
    <td>974 Clapton St.</td>
    <td>Queens</td>
    <td>NY</td>
    <td>$998 k</td>
  </tr>
  <tr>
    <td>14A Belmont Way</td>
    <td>Bronx</td>
    <td>NY</td>
    <td>$874 k</td>
  </tr>
</table>
```

Go ahead and save this page and refresh in the browser and you will see our table appears. The "th" cells have bold text that is centered above each column and the regular cells are normal text weight and left aligned. If you highlight the content of the table you will see the grid that the table is creating to align our content into rows and columns. Later on in a future lesson we will explore styling the table to adjust its visual appearance.

Next let's jump back over to the index.html page in your code editor.

### Images

To display images in HTML pages we use the `<img>` element. Let's insert one inside our index.html page just below our "h2". Then we will give it the two required attributes `src` and `alt`.

```html
<h2>Realty Group</h2>
<img src="" alt="">
```

The src (source) attribute points the browser to the location of our image file. Here will give it the relative path from our "index.html" page to our "intro-pic.jpg" file. Our image is inside of the "images" folder so we need to tell the browser to first open the images folder and load the intro-pic.jpg file inside of it such as `images/intro-pic.jpg`. We tell the browser to go into a folder by providing it "foldername/" folder name slash and to leave the current folder and go up to a parent directory we use "../" dot dot slash. In our case since the images folder is inside the same folder as our index page we can just specify `images/intro-pic.jpg`.

```html
<img src="images/intro-pic.jpg" alt="">
```

Next let's specify the alt attribute. The alt attribute stands for alternative text. It provides a text description for the visually impaired. In this case if a blind person was visiting this page a screen reader would read to them out loud the content of the page and when it got to our image it would read the alt text. This alt text is also useful for search engines.

```html
<img src="images/intro-pic.jpg" alt="A beautiful living room.">
```

We can also optionally add a title attribute that will display a text caption if the user mouses over the image and leaves the mouse there for a period of time.

```html
<img src="images/intro-pic.jpg" alt="A beautiful living room." title="Welcome to Exceptional Realty Group">
```

Let's save our file, and return to the browser and refresh the page you image should appear. When we mouse over the image and leave the mouse there for a second or two the title text "Welcome to Exceptional Realty Group" will appear. Notice that the alt text is hidden however.

### Links

Next, back in our code editor on the index.html page let's add some links to link all of the pages to each other. Above our image let's create some site navigation made up of `<a></a>` anchor link elements.

```
<!-- links -->
<a href="index.html">About</a>
```

Notice that we surround the content that we would like to act as a link with our starting `<a>` and ending `</a>` tags. The content in between these tags becomes the clickable link. We tell the browser which page to change to when we someone clicks our link by specifiying a relative path in the `href` attribute. So for our first link we wanted to link the text "About" to our "index.html" page. In the code this appears as: `<a href="index.html">About</a>`. Let's create more links one for each of out other site pages and one to link to an external website.

```html
<!-- links -->
<a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov">H.U.D.</a>
```

Note that on the last link instead of specifiying a relative file path as we did in the others that link to local site pages, we instead provided the absolute path using `http://` and the URL of the external website `hud.gov`. All of our links will by default target the current browser window so that when we click a link it will change the current browser window from the previous content to the content of the new page we are linking to. The last link for `hud.gov` we want to open a new browser tab when we click the link, that way the users current tab stays on our site and they are provided a new tab for the `hud.gov` Housing and Urban Development site. We accomplish this by adding the `target` attribute and setting its value to `_blank`. Here is the finished code:

```html
<!-- links -->
<a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
```

Let's copy and paste our link code and include it in the same place (just below the "h2" on all our other pages). Since the contact page is empty, fill it in with the following code:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
     <title>Exceptional Realty Group - Luxury Homes - Contact</title>
  </head>
  <body>
    <h1>Exceptional</h1>
    <h2>Realty Group</h2>
    <!-- links -->
    <a href="index.html">About</a> <a href="new-properties.html">New Properties</a> <a href="real-estate-listings.html">Listings</a> <a href="market-report.html">Market Report</a> <a href="contact.html">Contact</a> <a href="http://hud.gov" target="_blank">H.U.D.</a>
    <h3>Contact</h3>
  </body>
</html>
```

Then save all the pages and refresh the index page in the browser. Click the links on each page to test that we are properly linking to each page. The HUD link should open in a new browser tab.

### Validation

Let's talk about validating your HTML code. You're only human, we all make mistakes in our code from time to time. The most common type of error for a beginner is syntax error. That is when something in your code is not typed properly, is missing characters, or has additional uneccessary characters. To check for this, we can validate our code using the W3C's online HTML Validator.

To demonstrate this, we will purposely create a syntax error in our index page. Open the index.html page in your code editor. Scroll to where we wrote our first `<p>` element (for me this was on line 30 in the lecture video above) and remove the `>` symbol after the `<p`:

```html
<p lorem ipsum dolor sit amet, ... </p>
```

Now select all of your code by pressing Command + a on Mac or Ctrl + a on PC (Windows). Then copy the selected code to your clipboard by pressing Command + c on Mac or Ctrl + c on PC (Windows).

Next, open your browser and head to: `https://validator.w3.org/`. Then click the tab that says "Validate by Direct Input".

Click into the textarea field labeled "Enter the Markup to validate:" and paste your code by pressing Command + v on Mac or Ctrl + v on PC (Windows). Then click the big "Check" button.

A red bar should appear at the top of the page saying "Errors found while checking this document...". Scroll down the page where it says "Validation Output Errors". If all the rest of your code was correct except for the error message we just intentionally inserted, then the first error message will read something like:

> Line 30, Column 35: < in the attribute name. Probable cause: > missing immediately before.

The first part of the error "Line 30" identifies the line number of the issue. The second piece "Column 35" means 35 characters including spaces from the beginning of the line is where it sees the issue. The third piece "< in the attribute name." states that at that location it sees a `<` less than symbol that is being read as part of an attribute name on the `p` element. Then the fourth part "Probable cause: > missing immediately before" gives us a hint as to why this is broken. The reason is we have a missing `>` as it suggests.

Let's go back and fix our code adding the `>` symbol back in.

```html
<p>lorem ipsum dolor sit amet, ... </p>
```

Then save the file select all the text again and copy it to the clipboard, and paste it back into the validator and try checking it again a second time now that we corrected the error. This time a green bar appears at the top of the page that states "This document was successfully checked...". This means we have no more syntax errors in our code.

So you see the HTML validator can be helpful if we have typos in our code and they are tough to see on our own. The validator will scan the code and check for us letting us know of any potential issues.

### Backing Up Your Changes

In Terminal, type `git status` and press return to list any changes that have occured on your files. Looks like there were quite a few modified files. To stage the files type `git add .` and press return. Then commit the changes by typing `git commit -m "add main pages, text content, image, and links"` and press return.

To backup our branch on the remote server we can push it up by typing `git push -u origin main-pages` and press return. This will push up this recent commit to your personal Github repository.

Next let's go back to our master branch by typing `git checkout master` and press return.

Since we like the work we did on our "main-pages" branch, let's merge it into "master". This will include our commits from "main-pages" into the "master" branch. To do so type `git merge main-pages` and press return.

Normally, to back up our `master` branch we'd push it up to our personal GitHub remote by typing `git push origin master` and pressing return. However in order to submit this lesson, you'll need to type `learn submit`.

Congrats!

## Resources

- [HTML - Lang Codes](http://www.sitepoint.com/web-foundations/iso-2-letter-language-codes/)
- [HTML Encoding (Character Sets)](http://www.w3schools.com/html/html_charset.asp)

<p class='util--hide'>View <a href='https://learn.co/lessons/html-css-html-elements-code-along'>HTML Elements Code-Along</a> on Learn.co and start learning to code for free.</p>

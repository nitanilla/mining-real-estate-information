# HTML5 Video Embed Code-Along

<iframe width="640" height="480" src="//www.youtube.com/embed/ymUxDt_mOxU?rel=0&modestbranding=1" frameborder="0" allowfullscreen></iframe>

<p><a href="https://www.youtube.com/watch?v=ymUxDt_mOxU">HTML5 Video Embed Code-Along</a></p>

All the files needed to follow along are available in this lab. Just click 'Open IDE' in Learn. However, if you were following along using a personal `exceptional-realty`
repository in the previous HTML lessons, you can continue from where we left
off by running the following in your terminal:

```
git clone https://github.com/<your_username_here>/exceptional-realty
cd exceptional-realty
```

Following good git practices, since we're going to be adding some new content,
type `git checkout -b embed-video` to start up a new branch for this lesson.

[Click here to get the MP4 video linked to in the exercise](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/real-estate.mp4)

[Click here to get the OGV video linked to in the exercise](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/real-estate.ogv)

### Embedding Videos

Starting from inside your project folder (wherever your HTML files are stored),
let's create a new folder for videos by typing `mkdir videos` in our terminal.
This folder will appear beside your `images` folder. We'll use two videos
during this lesson, and we need to get them into our project before we can
incorporate them into the HTML. With the in-browser IDE, we'll need to use our
old friend `wget`. Navigate into the `videos` folder using `cd`, then when in
there, use `wget` with the following urls:

* Our MP4 video: http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/real-estate.mp4
* Our OGV video: http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/real-estate.ogv

Both videos should appear in your `videos` folder. In order to reach all
browser types, we want to include both of these videos in the event that one
video type is not supported by a particular browser.

Okay, we've got our content stored locally, so now we need to place it in our
webpage. In HTML5, we have a specific element for this, `<video>`. The
`<video>` element acts slightly differently than other media tags such as
`<img>`. It needs both an opening and closing tag, and instead of listing the
source as an attribute, the source of the video is added inside of the opening
and closing `<video>` tags.

Let's go ahead and add these `<video>` tags to our `index.html` page, just
below our paragraphs of text. Before adding a source, we'll add one attribute
to the opening `<video>` tag, `controls`. This will indicate to the browser to
always show controls for the embedded video.

Next, we'll add the source. Inside the `<video` tags, add `<source>`, and then,
as attributes, add in `src` and `type`. For our `src` attribute, we'll point it
to our `.mp4` video using a relative path to the file. We also want to
designate the type of this source as "video/mp4". At this point, our code will
look like this:

```
<video controls>
  <source src="videos/real-estate.mp4" type="video/mp4">
</video>
```

Now we'll add _a second source_, but change the source to
"videos/real-estate.ogv", and the type to "video/ogg".

This secondary source acts as a fallback.  Currently, all modern browsers support
`video/mp4`, but as of 2018, roughly 5% of users may still be using a browser
that does not, so adding this second line will ensure that every user can watch
the video.  

Well.. every user can watch the video as long as the browser they are using supports
the `<video>` element itself.  Again, there is still a small percentage of users
that are using outdated browsers that may not know what to do the HTML5 `<video>` tags.

For these users, we can also add a message inside the `<video>` tags. This message display
if a user's browser doesn't support the HTML5 video element. The message can
simply be "Your browser does not support HTML5 video", but we want to be nice
to our users, so we can also go ahead and add a link in this message that opens
a new page and navigates to a useful site such as
[https://browsehappy.com/](https://browsehappy.com/).

```
<video controls>
  <source src="videos/real-estate.mp4" type="video/mp4">
  <source src="videos/real-estate.ogv" type="video/ogg">
  Your browser does not support HTML5 video.  <a href="https://browsehappy.com/" target="_blank">Please upgrade your browser</a>
</video>
```

Now, if we test out our site in multiple browsers, we can see how our source
files work. In Chrome and Safari, for instance, the `.mp4` version of the video
will play. Opera and Firefox, on the other hand, will play the `.ogv` file.
Pretty much all modern browsers support at least one of these file types, so
we'd have to dig up an old, out of date browser to see our message and link.

### Wrapping Up

We now have a nice video on our home page! Everything is working and looking
good, so let's merge our `embed-video` branch with `master`. First, you'll
want to add, commit and push the work on our branch.

```
git add .
git commit -m 'add embedded video to index.html'
git push -u origin embed-video
```

Then, we will merge our branch into `master`, add and commit the newly merged
content, then push up the work to your repository:

```
git checkout master
git merge embed-video
git add .
git commit -m 'merged embed-video branch'
git push
```

<p data-visibility='hidden'>View <a
href='https://learn.co/lessons/html5-video-embed-code-along' title='HTML5 Video
Embed Code-Along'>HTML5 Video Embed Code-Along</a> on Learn.co and start
learning to code for free.</p>

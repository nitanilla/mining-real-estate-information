**Breadit**
==
An Open-Source Reddit App for Android
--

Yes, Breadit is an Open-Source application for Reddit. It's built with
the latest Android SDK with Android's new Material design in mind. Breadit
is designed to be a natural experience for Reddit on mobile. Instead of
the classic up and down arrows for voting that take up precious screen
real-estate, Breadit uses gestures to not only allow for more information
on the screen at one time but also make it easier to upvote/downvote
comments and submissions.

![Image of Upvoting/Downvoting](http://giant.gfycat.com/HelpfulSecondhandDog.gif)

Breadit also integrates the Imgur API beautifully, allowing for image
previews with Imgur titles and descriptions.

**Further optimizations include**
* Tap-to-hide to hide the rest of a comment tree from any comment
* Large, beautiful YouTube previews
* Watch YouTube videos without ever leaving the app
* Complete Gfycat support and caching - never waste mobile data
* Image caching, so you don't download the same image multiple times
* More to come

**Technical Details**

For networking, Breadit primarly uses Koush's
[Ion](https://github.com/koush/Ion) and
[AndroidAsync](https://github.com/koush/AndroidAsync) libraries, though
there is some legacy code that uses my own networking via Android's
AsyncTask API.

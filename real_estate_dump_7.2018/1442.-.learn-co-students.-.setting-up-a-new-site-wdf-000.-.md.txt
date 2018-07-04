# Setting up a New Site

## Objectives

1. Set up initial GitHub repository for upcoming labs
2. Review branching, committing and pushing to GitHub
3. Create some basic files and folders for your repository

## Introduction

In the upcoming labs, we will be working through the creation of a full
website, introducing various HTML concepts and components while applying them
to our site. Each lesson builds off of the work completed in the last, so in
this lesson, we will be going through the process of setting up your own GitHub
repository to code along in. In addition to this, in the event that you get
stuck or your personal repository isn't working as intended, you will have
access to a repository with starter code to follow along with from each lesson.

**NOTE**: Videos are provided in these lessons, but contain some instructions
and steps that have changed, especially if you are using the in-browser Learn
IDE. For this reason, the Readme content of these lessons will differ slightly
from video instructions, and will include up-to-date steps for navigating the
Learn IDE and completing these lessons entirely within your browser Learn
environment (instead of Sublime, the text editor used in the video). You do not
need specific applications such as Sublime or iTerm.

While using [the in-browser Sandbox][sb], if you leave the page or refresh, _any
work completed will be lost unless it is pushed up to a remote repository_,
which we will be discussing in this lesson. Make sure, though, to **always open
a new browser tab or window when navigating away from Learn**.

### Setting Up Your GitHub Repository

Let's start by creating some initial folders and files before creating a remote
git repository online.

* We will be creating a website for a fake real estate company called
  'Exceptional Realty Group.' Before anything else, we need a place to put our
  work. In your Learn terminal, create a project folder by typing
  `mkdir exceptional-realty`. Then, to navigate into that folder,
  type `cd exceptional-realty`.
* Let's create some basic files. From inside your project folder, type
  `touch README.md` to create an empty README file. The file will appear in
  the folder tree beside the text editor in the Learn IDE, within the
  `exceptional-realty` folder.
* We can add some content to this file by clicking the file to open it. Let's
  add a title, 'Exceptional Realty Group Website' and on a new line, we'll add
  a description: 'This is an example site for the Intro to Front-End Web
  Development course at the Flatiron School'.
* We should also create a `.gitignore` file, which is _essential_ in preventing
  private and/or sensitive files from being shared publicly when your
  repository is online. First, type `touch .gitignore` to create the
  file. For now, we can use a list of common `.gitignore` configurations to
  populate this file, provided via GitHub. Navigate to <a href="https://gist.github.com/octocat/9257657" target="_blank">https://gist.github.com/octocat/9257657</a>, copy the
  contents of the `.gitignore` file provided there, and paste them into your
  newly created
  file.

Now that we've got some files in our project, let's initialize a new git
repository locally, then create a remote repo and connect them.

* To initialize a new git repository locally, in our `exceptional-realty`
  folder, type `git init`. You should see a line in your terminal that displays
  where your git file has been created:

  ```
  Initialized empty Git repository in /home/.../exceptional-realty/.git/
  ```

* We now have a local git repository. If you type `git status` in your
  terminal, you should see the files we just created listed as
  'Untracked files'. Since these files are untracked, any changes made to them
  won't be recognized by our git repository yet.
* To track the files we've created and changed, type `git add .`. Then, we want
  to record, a.k.a 'commit', these changes to our git repo by typing
  `git commit -m 'first commit'`. The `-m` is short for `--message=`, which
  we'll use to state what we're doing during this particular commit.
* If you type `git status` now, you'll see that our files are no longer listed,
  and that there is 'nothing to commit, the working directory is clean',
  meaning there are no new changes since the last commit.

We've got our local work ready to go, so now we need to set up a new remote
repository to store this in.

* Open a new browser tab and go to <a href="github.com" target="_blank">github.com</a>
  and make sure you are signed in.
* In the upper right-hand corner of the page, click the **`+`** button and
  choose **_New repository_**
* You'll be brought to the **_Create a new repository_** page. We can go ahead
  and name this repository the same name we gave our folder, so in the
  _Repository name_ field, enter 'exceptional-realty'. Then, we'll add a brief
  description of what this repository is for in the _Description_ field.
* We can leave this repository set to _Public_. We also already have a
  README.md file, so we do not need to initialize this repository with one.
  Click **_Create repository_** to continue.
* GitHub provides commands in the **_Quick setup_** page for starting from
  scratch, pushing an existing local repository, or importing code from another
  repository. In our case, we need the commands for 'pushing an existing
  repository.' The url provided will be unique to your GitHub username and repo,
  so copy the first command that looks something like:

`git remote add origin https://github.com/<your_username_here>/exceptional-realty.git...`

* Back in the Learn terminal, paste in the copied command and press return. If
  you have any trouble, make sure you've set up an GitHub account SSH key to
  your local computer. Checkout this link for more info on setting up your
  SSH: <a href="https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/" target="_blank">Adding a New SSH Key to Your GitHub Account</a>.
* To push up your local work to this new remote repository, we'll use the
  second command GitHub provides:

```
git push -u origin master
```

* This tells our git repository to push up to our remote repository, `origin`,
  using our local repository's `master` branch. The `-u` is necessary for the
  first time we do this, as it also tells git to set up tracking between our
  local and remote `master` branches. You may need to enter your GitHub
  credentials in the terminal to complete this step. If successful, your
  terminal will display that it is counting and writing objects to your remote
  repository, and that `Branch master set up to track remote branch master from origin.`
* Head back github.com and refresh the _'Quick setup'_ page. Your pushed up
  files should appear.
* At any point going forward, if you accidentally navigate away from these
  learn lessons or refresh the page, you can always re-clone a copy of your
  remote repo by entering the following into your terminal:

`git clone https://github.com/<your_username_here>/exceptional-realty`

This will download a copy to your Learn IDE based on whatever you last
committed and pushed up to GitHub. Always push up any work you want
to keep and access again! If you run into any issues while following along in
these lessons, or are unable to set up your own repository, remember that you
will still be able to use a demonstration repository in each of the following
lessons to code along.

### Adding Branches

* From inside your repository folder in the Learn IDE, type `git branch`. This
  command will show you all the existing branches that are stored locally on
  your computer, and currently, we only have one, `master`. As a general best
  practice, the `master` branch should always be kept in a fully functional
  state; any new features or additions made on a repo should be done on a
  separate branch, allowing one or more developers to work on isolated parts of
  a project without interfering with the `master` version until the branch code
  is fully ready.
* We're going to create a new branch and add some files to this repository. To
  do this, type:

```
git checkout -b main-pages
```

Your terminal should now display that you are on a new branch, `(main-pages)`,
instead of `(master)`.

* Let's create some additional web pages for our website. You can do this by
  choosing to click the `Create New` button in your Learn IDE and choosing
  `File`, or by using your terminal and the command `touch`, followed by the
  name of the file. Go ahead and create our first file, `index.html`, all
  lowercase, which will be our homepage on the website. Now, let's create the
  rest of our web pages:

```
touch index.html
touch contact.html
touch market-report.html
touch new-properties.html
touch real-estate-listings.html
```

* Naming these files based on what they will contain will keep us better
  organized, and can also help when it comes to search engine optimization, as
  search engine bots can use file names to find relevant search information.

### Retrieving Files Using the `wget` Command

* We will need a separate folder for storing some image files. Create a
  directory using `mkdir` or your `Create New` button, and name it `images`.
* Let's go ahead and add an image to this folder. You may be used to
  downloading images off the internet by simply navigating to that image, right
  clicking, and saving the file. We're going to employ a special terminal
  command that will work with the in-browser IDE, `wget`. First,
  though, we need an image. Since we're building a real estate website, let's
  use the image found at <a href="http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/intro-pic.jpg" target="_blank">http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/intro-pic.jpg</a>:

![Intro Pic](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/intro-pic.jpg "Intro Pic")

* Copy the full url path of the image, navigate (`cd`) into your `images`
  folder, and type the following:

`wget http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/intro-pic.jpg`

* The file `intro-pic.jpg` should appear in your images folder. You may not be
  able to view this image in the Learn IDE, but that is fine; we can still use it
  in our site.

In the upcoming videos, whenever an image or video is downloaded from the
internet, the written instructions will use `wget` instead to retrieve those
files.

### Testing our Website Using `httpserver`

While we build our website and add content, we need to be actively checking to see what the
actual site looks like. In the Learn IDE, we can use a tool that is already
built in, `httpserver`!

* Navigate out of the `images` folder using `cd ..`, so you are in your main
  `exceptional-realty` folder.
* In your terminal, type `httpserver` and press `return`.
* You will see a message `Your server is running at ...`, following by a string
  of numbers, with periods and a colon. Copy that string, open a new tab, and paste.
* At this point, you will see a blank page because we don't have anything in
  our index.html file. However, you can check to see if the files are being
  served by adding the following to the end of the pasted numbers: `/images/intro-pic.jpg`
* If all is well, the image we retrieved using `wget` and placed in our
  `images` folder should appear.
* To stop `httpserver`, make sure your terminal is in focus and press `Control` + `C`.

We will use `httpserver` throughout these lessons in place of opening files via
Finder, the method mentioned in the videos.

### Wrapping Up

We now have a remote repository set up with a good foundation of necessary
files. Before moving on, make sure you have added, committed and pushed your
local work up to your remote repository. But wait! If you've been following
along, you're currently on a _new branch_, `main-pages`! Our new features
aren't complete, so we want to make sure this branch is stored separately from
our `master` branch in our remote repository. Entering the following commands
will push up this new branch without interfering with `master`:

```
git add .
git commit -m 'added html pages and an image'
git push -u origin main-pages
```

This adds any changes you've made, creates a commit record of them, and tells
git to push the `main-pages` branch to your `origin`, the remote repository,
setting up tracking between your local and remote `main-pages` branches. If
you check out your repository on GitHub, you'll see that you now have **2**
branches, `master`, and `main-pages`.

Always make sure to push up any new work before continuing to the next lesson.
This way, at the beginning of your next lesson, you can clone down a copy of
your remote repository, switch over to the `main-pages` branch and continue
working. The following instructions will be in each lesson, but
for reference, here are the steps:

```
git clone https://github.com/<your_username_here>/exceptional-realty
cd exceptional-realty
git fetch --all
git checkout main-pages
```

The `git fetch --all` is necessary, as just cloning down a repository will
only pull the `master` branch to your local computer. We use `fetch --all` to
retrieve all remote branches, then `checkout` to switch over to one.


<iframe width="640" height="480" src="//www.youtube.com/embed/i61lTJ6OpDE?rel=0&modestbranding=1" frameborder="0" allowfullscreen></iframe>

[Alternate video link.](https://www.youtube.com/watch?v=i61lTJ6OpDE)

[Click here to go to the intro pic used in this code along.](http://ironboard-curriculum-content.s3.amazonaws.com/front-end/lab-assets/intro-pic.jpg)

[Here is a direct link to the gitignore code referenced in the video.](https://gist.githubusercontent.com/octocat/9257657/raw/3f9569e65df83a7b328b39a091f0ce9c6efc6429/.gitignore)

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/setting-up-a-new-site' title='Setting up a New Site'>Setting up a New Site</a> on Learn.co and start learning to code for free.</p>

[sb]: http://help.learn.co/ide-in-browser/ide-in-browser-sandbox

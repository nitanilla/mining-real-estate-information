# HTML Fundamentals Code Along Exercise 1

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

In this exercise you will code along with the video to review the HTML fundamentals.

## Instructions

### Open the Repository

Use the `Open` button on this page to fork and clone the project repository locally. Once you've done this, open up the project directory in Atom using `atom .` or `open . -a "Atom"`

### Starting a New Site Project

At this point in Terminal you would create any sub folders and files using the `mkdir` command and `touch` commands. We have already done this for you so you can get coding right away. In Sublime you will see we have already created the files and folders.

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

### Code Along Video

Follow along with the provided video, coding everything you see there. Feel free to stop, pause, rewind or fast forward through the content to keep pace. After the video, continue on to the text instructions that follow below.

<iframe width="640" height="360" src="https://www.youtube.com/embed/videoseries?list=PLj148bJp5wiyXRRpL8rM-cLETaClgdBK2" frameborder="0" allowfullscreen></iframe>

### Setup local testing.

Please <a href="https://www.mozilla.org/en-US/firefox/new/" target="_blank">install Firefox</a> if you haven't already as it is required for the screenshot tests to run.

### Run local tests.

To run local tests type the `learn` command from Terminal. This will take a snapshot of one of your pages and make a comparison with a solution snapshot. If it passes, the local build light will turn green for this lesson page back at learn.co in your browser. If it does not pass watch the video again, and check your code.

### Stage, commit, and push up your changes.

#### `git add`

Adding changes with the `git add` command is a way to stage any changes and get them ready to become a permanent record in your git log via a commit. The workflow worth memorizing right now is to simply add all your changes via `git add .`.

#### `git commit`

A commit is a permanent moment in time in your git history. A commit creates a new version of your code. To commit, memorize this command. `git commit -m "Your commit message"`. You are using the `git commit` command with the flags `-m`, which tell git to include a commit message. You supply the commit message in `""` directly in the command, `"Your commit message"`.

#### `git push`

Pushing is the process of taking your local code and commits and syncing them, or uploading them, to GitHub. You're updating the GitHub remote (remotes are just fancy names for copies of the repository), generally your fork, represented by a remote named `origin`, by pushing your code to the remote. The git command to do this is simply `git push`. When you `git push` from within a git repository, it will take all the commits that you have locally and push them to the online remote.

### Make a Pull Request on Github

Submitting a pull request is how you submit your lab to be evaluated or graded on Learn. We've abstracted some of the complexities of doing this, so all you need to do is type `learn submit`

## Resources

- [HTML Encoding (Character Sets)](http://www.w3schools.com/html/html_charset.asp)

Introduction
============

This repo consists of `bash` scripts (et cetera) for use with [`madonctl`][1], the best solution for command line usage of [Mastodon][4] available, in my honest opinion.

Don't expect heavily polished stuff here. I generally make things as I go. `madonctl` is meant to be easily scriptable, which lends itself well to quick solutions.

Also, I'm working on a set of templates tweaked to my liking. I usually have an active [`tmux`][2] window of 5 panes, 4 of which are dedicated to `madonctl`. Using a fair amount of real estate, I like to keep things simple.

Scripts
=======

 * **`toot`** has 3 forms, all of which take input from stdin and can optionally add a single attachment:
   1. **`toot dm [file`*****`URL | path`*****`]`** creates a direct message. don't forget to include the mention.
   1. **`toot`*****`status-id | URL`*****`[ file`*****`URL | path`*****`]`** will reply with appropriate visibility and mentions.
   1. **`toot [ file`*****`URL | path`*****`]`** will create a new toot.
 * **`untoot`*****`status-id | URL`*** deletes toots.
 * **`mytoots`** shows recent mentions.
 * **`follows`** deals with follow requests. For each, you can accept/deny and assuming the former, follow back if you like.
 * **`follow`*****`status-id | user-id | URL`*** follows a user.
 * **`unfollow`*****`status-id | user-id | URL`*** unfollows a user.
 * **`fav`*****`status-id | URL`*** just favorites.
 * **`boost`*****`status-id | URL`*** just boosts. 
 * **`favboost`*****`status-id | URL`*** boosts and favorites.
 * **`show`*****`status-id`*** opens a toot in the browser.
 * **`tootmux`** adds my preferred set up to the current tmux window, occupying 60% of the total space:
   1. home stream (30%)
   1. local stream (30% - 10 lines)
   1. mentions-only notifications stream (6 lines)
   1. area for entering commands (2 lines)

Templates
=========

 * **mynotifications.tmpl** to use with `--template-file` for notifications.
   ![pic of mynotifications.tmpl in action](https://raw.githubusercontent.com/wxl/madonctl-scripts/master/assets/images/mynotifications.png "direct, sensitive toot with content warning")
   ![pic of mynotifications.tmpl with attachment](https://raw.githubusercontent.com/wxl/madonctl-scripts/master/assets/images/attachmentnotification.png "public toot with attachment")
   * Bell at the beginning, which `tmux` makes visual.
   * Trimmed down to remove anything except stuff relevant to mentions. I don't care being notified about reblogs or favorites (but thank you for them!), so none of that is there.
   * Emojis for `sensitive: true` (⚠), `visibility: direct` (🔒), and whether or not there are attachments (📎).
   * No names, no attachment links. 
   * As little as 2 lines (default can be up to 10 times that):
     1. status-id (reply-to-id as relevant), account and id, link to status
     2. spoiler (if available) followed by message.

Installation
============

Make sure that `$HOME/bin` is in your `$PATH` and fill it up with symlinks:

```
find /path/to/madonctl-scripts/src/scripts -type f -exec ln -s {} ~/bin \;
```

Compatibility
=============

tl;dr Everything should Just Work™ with Mastodon instances running v2.0.0, which `madonctl` should be updated for at this point as well.

As of [v2.0.0][10], `id` attributes are not returned as strings instead of integers. Whenever templating is employed, this is now represented as `{{.id}}` whereas previously it was `{{printf "%.0f" .id}}`. Naturally, if any conditionals are used, the logic will need to be a little different. 

Support
=======

Further questions and comments may be addressed to [@wxl@soc.ialis.me][3] 

Shout outs
==========

 * Super big thank yous to [@McKael@mamot.fr][7] for not only creating [`madonctl`][1] but for being so darn responsive to my many questions and suggestions. Someone give this guy a raise! (actually, there's a donation button on a [website][8] related to another project of his)
 * A special thank you to [@redwolf@masto.io][5] for the lovely example toot to show off my notifications template. It does seem to suggest that he (and/or me) is a perv, but in fact, it was a lovely picture of [mating iguanas][6]. Of course, he still *might* be a perv, but…
 * Thanks to [@ghost@anticapitalist.party][9] (who is super duper awesome and is always good for a thoughtful, in depth conversation!) for sending me a lovely pic of Alice in Wonderland. She's right, it's too darn cute!

[1]: https://github.com/McKael/madonctl
[2]: https://github.com/tmux/tmux
[3]: https://soc.ialis.me/@wxl
[4]: https://github.com/tootsuite/mastodon
[5]: https://masto.io/@redwolf
[6]: https://pictor.ialis.me/media_attachments/files/000/218/734/original/79069ce1b3ea6da5.jpg
[7]: https://mamot.fr/@McKael
[8]: https://mcabber.com/
[9]: https://anticapitalist.party/@ghost
[10]: https://github.com/tootsuite/mastodon/releases/tag/v2.0.0

# Slackify

[![Build Status](https://travis-ci.org/strimeapp/Slackify.svg?branch=master)](https://travis-ci.org/strimeapp/Slackify)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/strimeapp/Slackify/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/strimeapp/Slackify/?branch=master)
[![Total Downloads](https://poser.pugx.org/strimeapp/slackify/downloads)](https://packagist.org/packages/strimeapp/slackify)
[![License](https://poser.pugx.org/strimeapp/slackify/license)](https://packagist.org/packages/strimeapp/slackify)

Slackify is a PHP bundle which lets you communicate with Slack API.

It has been initially developed for [Strime](https://www.strime.io).

## Installation

The recommended way to install Slackify is through [Composer](https://getcomposer.org).

```bash
$ composer require strimeapp/slackify
```

## Webhooks

Slackify allows you to easily send messages to webhooks.

```php
use Strime\Slackify\Webhooks\Webhook;

$webhook = new Webhook("https://hooks.slack.com/services/YOUR/WEBHOOK");

$webhook->sendMessage(array(
    "message" => "My first message",
    "username" => "Bobby",
    "icon" => "http://upshout.net/wp-content/uploads/2016/03/unicorn-002.jpg",
    "link" => "https://www.strime.io",
    "link_text" => "Strime"
));
```

The `icon` parameter may either be an URL to an image, or an emoji code (:taco: for instance).

The `link_text` parameter is the text that will be clickable, if you set the `link` parameter.

## Sending attachments

If you want to send attachments allong to your message, you can do it like this, before sending the message:

```php
use Strime\Slackify\Webhooks\Webhook;

$webhook = new Webhook("https://hooks.slack.com/services/YOUR/WEBHOOK");

$webhook->setAttachments(
    array(
        array(
            "fallback" => "A fallback text",
            "text" => "The text of your attachment",
            "color" => "#123456",
            "fields" => array(
                "title" => "My attachment",
                "value" => "The value of my attachment",
                "short" => FALSE
            )
        )
    )
);

$webhook->sendMessage(array(
    "message" => "My first message",
    "username" => "Bobby",
    "icon" => "http://upshout.net/wp-content/uploads/2016/03/unicorn-002.jpg",
    "link" => "https://www.strime.io",
    "link_text" => "Strime"
));
```

- *fallback*: A plain-text summary of the attachment. This text will be used in clients that don't show formatted text (eg. IRC, mobile notifications) and should not contain any markup.
- *color*: Like traffic signals, color-coding messages can quickly communicate intent and help separate them from the flow of other messages in the timeline. An optional value that can either be one of `good`, `warning`, `danger`, or any hex color code (eg. `#439FE0`). This value is used to color the border along the left side of the message attachment.
- *pretext*: This is optional text that appears above the message attachment block.
- *author*: The author parameters will display a small section at the top of a message attachment that can contain the following fields:
	- *author_name*: Small text used to display the author's name.
	- *author_link*: A valid URL that will hyperlink the `author_name` text mentioned above. Will only work if `author_name` is present.
	- *author_icon*: A valid URL that displays a small 16x16px image to the left of the `author_name` text. Will only work if `author_name` is present.
- *title*: The `title` is displayed as larger, bold text near the top of a message attachment. By passing a valid URL in the `title_link` parameter (optional), the title text will be hyperlinked.
- *fields*:
	- *title*: Shown as a bold heading above the value text. It cannot contain markup and will be escaped for you.
	- *value*: The text value of the field. It may contain [standard message markup](https://api.slack.com/docs/message-formatting) and must be escaped as normal. May be multi-line.
	- *short*: An optional flag indicating whether the value is short enough to be displayed side-by-side with other values.
- *image_url*: A valid URL to an image file that will be displayed inside a message attachment. We currently support the following formats: GIF, JPEG, PNG, and BMP. Large images will be resized to a maximum width of 400px or a maximum height of 500px, while still maintaining the original aspect ratio.
- *thumb_url*: A valid URL to an image file that will be displayed as a thumbnail on the right side of a message attachment. We currently support the following formats: GIF, JPEG, PNG, and BMP. The thumbnail's longest dimension will be scaled down to 75px while maintaining the aspect ratio of the image. The filesize of the image must also be less than 500 KB. For best results, please use images that are already 75px by 75px.
- *footer*: Add some brief text to help contextualize and identify an attachment. Limited to 300 characters, and may be truncated further when displayed to users in environments with limited screen real estate.
- *footer_icon*: To render a small icon beside your footer text, provide a publicly accessible URL string in the `footer_icon` field. You must also provide a `footer` for the field to be recognized. We'll render what you provide at 16px by 16px. It's best to use an image that is similarly sized.
- *ts*: By providing the ts field with an integer value in "[epoch time](https://en.wikipedia.org/wiki/Unix_time)", the attachment will display an additional timestamp value as part of the attachment's footer.

## API

Slackify also allows you to easily send requests to the API.

In order to instantiate a connection to the API, you will need a token. You can generate test tokens [here](https://api.slack.com/docs/oauth-test-tokens).

Each section of the [API documentation](https://api.slack.com/methods) has its own class with the corresponding methods.

```php
use Strime\Slackify\Api\Api;

// API request
$api_request = new Api("your-api-token-comes-here");
$api_request->test();
```

The following links will give you more details about the methods, specially about the variables and the error codes:
- [test](https://api.slack.com/methods/api.test)


```php
use Strime\Slackify\Api\Auth;

// Auth requests
$api_auth_request = new Auth("your-api-token-comes-here");
$api_auth_request->revoke("a-token-to-revoke", TRUE);
$api_auth_request->test("a-token-to-test");
```

The following links will give you more details about the methods:
- [revoke](https://api.slack.com/methods/auth.revoke)
- [test](https://api.slack.com/methods/auth.test)


```php
use Strime\Slackify\Api\Bots;

// Bots requests
$api_bots_request = new Bots("your-api-token-comes-here");
$api_bots_request->info("B123456");
```

The following links will give you more details about the methods:
- [info](https://api.slack.com/methods/bots.info)


```php
use Strime\Slackify\Api\Channels;

// Channels requests
$api_channels_request = new Channels("your-api-token-comes-here");
$api_channels_request->archive("C123456");
$api_channels_request->create("C123456");
$api_channels_request->history("C123456", "now", 0, 0, 100, 0);
$api_channels_request->info("C123456");
$api_channels_request->invite("C123456", "U56789");
$api_channels_request->join("C123456");
$api_channels_request->kick("C123456", "U56789");
$api_channels_request->leave("C123456");
$api_channels_request->list_channels(0);
$api_channels_request->mark("C123456", time());
$api_channels_request->rename("C123456", "New name");
$api_channels_request->replies("C123456", time());
$api_channels_request->setPurpose("C123456", "New purpose");
$api_channels_request->setTopic("C123456", "New topic");
$api_channels_request->unarchive("C123456");
```

The following links will give you more details about the methods:
- [archive](https://api.slack.com/methods/channels.archive)
- [create](https://api.slack.com/methods/channels.create)
- [history](https://api.slack.com/methods/channels.history)
- [info](https://api.slack.com/methods/channels.info)
- [invite](https://api.slack.com/methods/channels.invite)
- [join](https://api.slack.com/methods/channels.join)
- [kick](https://api.slack.com/methods/channels.kick)
- [leave](https://api.slack.com/methods/channels.leave)
- [list](https://api.slack.com/methods/channels.list)
- [mark](https://api.slack.com/methods/channels.mark)
- [rename](https://api.slack.com/methods/channels.rename)
- [replies](https://api.slack.com/methods/channels.replies)
- [setPurpose](https://api.slack.com/methods/channels.setPurpose)
- [setTopic](https://api.slack.com/methods/channels.setTopic)
- [unarchive](https://api.slack.com/methods/channels.unarchive)


```php
use Strime\Slackify\Api\Chat;

// Chat requests
$api_chat_request = new Chat("your-api-token-comes-here");
$api_chat_request->delete(time(), "C12345");
$api_chat_request->meMessage("C12345", "foo bar");
$api_chat_request->postMessage("C12345", "foo bar", "full", 0);
$api_chat_request->update(time(), "C12345", "foo bar");
```

The following links will give you more details about the methods:
- [delete](https://api.slack.com/methods/chat.delete)
- [meMessage](https://api.slack.com/methods/chat.meMessage)
- [postMessage](https://api.slack.com/methods/chat.postMessage)
- [update](https://api.slack.com/methods/chat.update)


```php
use Strime\Slackify\Api\Dnd;

// Dnd requests
$api_dnd_request = new Dnd("your-api-token-comes-here");
$api_dnd_request->endDnd();
$api_dnd_request->endSnooze();
$api_dnd_request->info("U12345");
$api_dnd_request->setSnooze(10);
$api_dnd_request->teamInfo("U12345,U67890");
```

The following links will give you more details about the methods:
- [endDnd](https://api.slack.com/methods/dnd.endDnd)
- [endSnooze](https://api.slack.com/methods/dnd.endSnooze)
- [info](https://api.slack.com/methods/dnd.info)
- [setSnooze](https://api.slack.com/methods/dnd.setSnooze)
- [teamInfo](https://api.slack.com/methods/dnd.teamInfo)


```php
use Strime\Slackify\Api\Emoji;

// Emoji requests
$api_emoji_request = new Emoji("your-api-token-comes-here");
$api_emoji_request->list_emoji();
```

The following links will give you more details about the methods:
- [list](https://api.slack.com/methods/emoji.list)


```php
use Strime\Slackify\Api\FilesComments;

// FilesComments requests
$api_files_comments_request = new FilesComments("your-api-token-comes-here");
$api_files_comments_request->add("F12345", "Foo bar", "U12345");
$api_files_comments_request->delete("F12345", "Fc12345");
$api_files_comments_request->edit("F12345", "Fc12345", "Foo bar");
```

The following links will give you more details about the methods:
- [add](https://api.slack.com/methods/files.comments.add)
- [delete](https://api.slack.com/methods/files.comments.delete)
- [edit](https://api.slack.com/methods/files.comments.edit)


```php
use Strime\Slackify\Api\Files;

// Files requests
$api_files_request = new Files("your-api-token-comes-here");
$api_files_request->delete("F12345");
$api_files_request->info("F12345", 100, 1);
$api_files_request->list_files("U12345", "C12345", "now", "all", "all", 100, 1);
$api_files_request->revokePublicURL("F12345");
$api_files_request->sharedPublicURL("F12345");
$api_files_request->upload("test.txt", "/path/to/file", "text", "A title", "A comment", "C12345,C67890");
```

The following links will give you more details about the methods:
- [delete](https://api.slack.com/methods/files.delete)
- [info](https://api.slack.com/methods/files.info)
- [list](https://api.slack.com/methods/files.list)
- [revokePublicURL](https://api.slack.com/methods/files.revokePublicURL)
- [sharedPublicURL](https://api.slack.com/methods/files.sharedPublicURL)
- [upload](https://api.slack.com/methods/files.upload)


```php
use Strime\Slackify\Api\Groups;

// Groups requests
$api_groups_request = new Groups("your-api-token-comes-here");
$api_groups_request->archive("G12345");
$api_groups_request->close("G12345");
$api_groups_request->create("Foo bar");
$api_groups_request->createChild("G12345");
$api_groups_request->history("G12345", "now", "0", 0, 100, 1);
$api_groups_request->info("G12345");
$api_groups_request->invite("G12345", "U12345");
$api_groups_request->kick("G12345", "U12345");
$api_groups_request->leave("G12345");
$api_groups_request->list_groups(1);
$api_groups_request->mark("G12345", (string)time());
$api_groups_request->open("G12345");
$api_groups_request->rename("G12345", "Foo bar");
$api_groups_request->replies("C12345", time());
$api_groups_request->setPurpose("G12345", "Foo bar");
$api_groups_request->setTopic("G12345", "Foo bar");
$api_groups_request->unarchive("G12345");
```

The following links will give you more details about the methods:
- [archive](https://api.slack.com/methods/groups.archive)
- [close](https://api.slack.com/methods/groups.close)
- [create](https://api.slack.com/methods/groups.create)
- [createChild](https://api.slack.com/methods/groups.createChild)
- [history](https://api.slack.com/methods/groups.history)
- [info](https://api.slack.com/methods/groups.info)
- [invite](https://api.slack.com/methods/groups.invite)
- [kick](https://api.slack.com/methods/groups.kick)
- [leave](https://api.slack.com/methods/groups.leave)
- [list](https://api.slack.com/methods/groups.list)
- [mark](https://api.slack.com/methods/groups.mark)
- [open](https://api.slack.com/methods/groups.open)
- [rename](https://api.slack.com/methods/groups.rename)
- [replies](https://api.slack.com/methods/groups.replies)
- [setPurpose](https://api.slack.com/methods/groups.setPurpose)
- [setTopic](https://api.slack.com/methods/groups.setTopic)
- [unarchive](https://api.slack.com/methods/groups.unarchive)


```php
use Strime\Slackify\Api\Im;

// Im requests
$api_im_request = new Im("your-api-token-comes-here");
$api_im_request->close("D12345");
$api_im_request->history("G12345", "now", "0", 0, 100, 1);
$api_im_request->list_im();
$api_im_request->mark("D12345", time());
$api_im_request->open("U12345", TRUE);
$api_im_request->replies("D12345", time());
```

The following links will give you more details about the methods:
- [close](https://api.slack.com/methods/im.close)
- [history](https://api.slack.com/methods/im.history)
- [list](https://api.slack.com/methods/im.list)
- [mark](https://api.slack.com/methods/im.mark)
- [open](https://api.slack.com/methods/im.open)
- [replies](https://api.slack.com/methods/im.replies)


```php
use Strime\Slackify\Api\Mpim;

// Mpim requests
$api_mpim_request = new Mpim("your-api-token-comes-here");
$api_mpim_request->close("D12345");
$api_mpim_request->history("G12345", "now", "0", 0, 100, 1);
$api_mpim_request->list_mpim();
$api_mpim_request->mark("D12345", time());
$api_mpim_request->open("U12345,U67890", TRUE);
$api_mpim_request->replies("D12345", time());
```

The following links will give you more details about the methods:
- [close](https://api.slack.com/methods/mpim.close)
- [history](https://api.slack.com/methods/mpim.history)
- [list](https://api.slack.com/methods/mpim.list)
- [mark](https://api.slack.com/methods/mpim.mark)
- [open](https://api.slack.com/methods/mpim.open)
- [replies](https://api.slack.com/methods/mpim.replies)


```php
use Strime\Slackify\Api\Oauth;

// Oauth requests
$api_oauth_request = new Oauth("your-api-token-comes-here");
$api_oauth_request->access("client_id", "client_secret", "code", "https://www.foo.com");
```

The following links will give you more details about the methods:
- [access](https://api.slack.com/methods/oauth.access)

```php
use Strime\Slackify\Api\Pin;

// Pin requests
$api_pin_request = new Pin("your-api-token-comes-here");
$api_pin_request->add("C12345", "F12345", "Fc12345", time());
$api_pin_request->list_pin("C12345");
$api_pin_request->remove("C12345", "F12345", "Fc12345", time());
```

The following links will give you more details about the methods:
- [add](https://api.slack.com/methods/pins.close)
- [list](https://api.slack.com/methods/pins.list)
- [remove](https://api.slack.com/methods/pins.remove)

```php
use Strime\Slackify\Api\Reactions;

// Reactions requests
$api_reactions_request = new Reactions("your-api-token-comes-here");
$api_reactions_request->add("F12345", "Fc12345", "C12345", time());
$api_reactions_request->get("F12345", "Fc12345", "C12345");
$api_reactions_request->list_reactions("U12345", TRUE);
$api_reactions_request->remove("F12345", "Fc12345", "C12345", time());
```

The following links will give you more details about the methods:
- [add](https://api.slack.com/methods/reactions.add)
- [get](https://api.slack.com/methods/reactions.get)
- [list](https://api.slack.com/methods/reactions.list)
- [remove](https://api.slack.com/methods/reactions.remove)

```php
use Strime\Slackify\Api\Reminders;

// Reminders requests
$api_reminders_request = new Reminders("your-api-token-comes-here");
$api_reminders_request->add("Foo", time(), "U12345");
$api_reminders_request->complete("Rm12345");
$api_reminders_request->delete("Rm12345");
$api_reminders_request->info("Rm12345");
$api_reminders_request->list_reminders();
```

The following links will give you more details about the methods:
- [add](https://api.slack.com/methods/reminders.add)
- [complete](https://api.slack.com/methods/reminders.complete)
- [delete](https://api.slack.com/methods/reminders.delete)
- [info](https://api.slack.com/methods/reminders.info)
- [list](https://api.slack.com/methods/reminders.list)

```php
use Strime\Slackify\Api\Rtm;

// Rtm requests
$api_rtm_request = new Rtm("your-api-token-comes-here");
$api_rtm_request->start(TRUE, FALSE, TRUE);
```

The following links will give you more details about the methods:
- [start](https://api.slack.com/methods/rtm.start)

```php
use Strime\Slackify\Api\Search;

// Search requests
$api_search_request = new Search("your-api-token-comes-here");
$api_search_request->all("pickleface", "score", "asc", TRUE, 20, 3);
$api_search_request->files("pickleface", "timestamp", "asc", TRUE, 20, 3);
$api_search_request->messages("pickleface", "timestamp", "asc", TRUE, 20, 3);
```

The following links will give you more details about the methods:
- [all](https://api.slack.com/methods/search.all)
- [files](https://api.slack.com/methods/search.files)
- [messages](https://api.slack.com/methods/search.messages)

```php
use Strime\Slackify\Api\Stars;

// Search requests
$api_stars_request = new Stars("your-api-token-comes-here");
$api_stars_request->add("F12345", "Fc12345", "C12345", time());
$api_stars_request->list_stars(20, 3);
$api_stars_request->remove("F12345", "Fc12345", "C12345", time());
```

The following links will give you more details about the methods:
- [add](https://api.slack.com/methods/stars.add)
- [list](https://api.slack.com/methods/stars.list)
- [remove](https://api.slack.com/methods/stars.remove)

```php
use Strime\Slackify\Api\Team;

// Search requests
$api_team_request = new Team("your-api-token-comes-here");
$api_team_request->accessLogs(100, 2, "now");
$api_team_request->billableInfo("U12345");
$api_team_request->info();
$api_team_request->integrationLogs("foo", "bar", "U12345", "foo", 20, 2);
$api_team_request->profile.get("all");
```

The following links will give you more details about the methods:
- [accessLogs](https://api.slack.com/methods/team.accessLogs)
- [billableInfo](https://api.slack.com/methods/team.billableInfo)
- [info](https://api.slack.com/methods/team.info)
- [integrationLogs](https://api.slack.com/methods/team.integrationLogs)
- [profile.get](https://api.slack.com/methods/team.profile.get)

```php
use Strime\Slackify\Api\UserGroups;

// Search requests
$api_user_groups_request = new UserGroups("your-api-token-comes-here");
$api_user_groups_request->create("foo", "bar", "description", "C12345,C67890");
$api_user_groups_request->disable("S12345", TRUE);
$api_user_groups_request->enable("S12345", TRUE);
$api_user_groups_request->list_usergroups(TRUE, FALSE, TRUE);
$api_user_groups_request->update("S12345", "Foo", "bar", "description", "C12345,C67890", TRUE);
$api_user_groups_request->users.list("S12345", TRUE);
$api_user_groups_request->users.update("S12345", "U12345,U67890", TRUE);
```

The following links will give you more details about the methods:
- [create](https://api.slack.com/methods/usergroups.create)
- [disable](https://api.slack.com/methods/usergroups.disable)
- [enable](https://api.slack.com/methods/usergroups.enable)
- [list](https://api.slack.com/methods/usergroups.list)
- [update](https://api.slack.com/methods/usergroups.update)
- [users.list](https://api.slack.com/methods/usergroups.users.list)
- [users.update](https://api.slack.com/methods/usergroups.users.update)

```php
use Strime\Slackify\Api\Users;

// Search requests
$api_users_request = new Users("your-api-token-comes-here");
$api_users_request->deletePhoto();
$api_users_request->getPresence("U12345");
$api_users_request->identity();
$api_users_request->info("U12345");
$api_users_request->list_users(TRUE);
$api_users_request->setActive();
$api_users_request->setPresence("away");
```

The following links will give you more details about the methods:
- [deletePhoto](https://api.slack.com/methods/users.deletePhoto)
- [getPresence](https://api.slack.com/methods/users.getPresence)
- [identity](https://api.slack.com/methods/users.identity)
- [info](https://api.slack.com/methods/users.info)
- [list](https://api.slack.com/methods/users.list)
- [setActive](https://api.slack.com/methods/users.setActive)
- [setPhoto](https://api.slack.com/methods/users.setPhoto)
- [setPresence](https://api.slack.com/methods/users.setPresence)

```php
use Strime\Slackify\Api\UsersProfile;

// Search requests
$api_users_profile_request = new UsersProfile("your-api-token-comes-here");
$api_users_profile_request->get("U12345", TRUE);
$api_users_profile_request->set("U12345", "{first_name: 'Bobby', last_name: 'Brown'}");
```

The following links will give you more details about the methods:
- [get](https://api.slack.com/methods/users.profile.get)
- [set](https://api.slack.com/methods/users.profile.set)

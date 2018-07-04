# kickball-app
mobile app design project for the Iron Yard week 7

# App Inspiration

The three main pieces of the UI for this app will be the newsfeed, leaderboards and stats, and chat. I couldn't find a single app does all of these things well, so I'll divide the inspiration up by section.

## Newsfeed

### [Twitter](https://itunes.apple.com/us/app/twitter/id333903271?mt=8)

I appreciate the way that twitter uses active states to expand and collapse features to preserve real estate. For example, when you land on the twitter page, the "what's happening" field is collapsed, but prominent. When you click on it, however, it expands to include other options. 

Also, 140 characters is just the right amount of space to indicate what sort of content will be in a post. 


## Chat

### [Slack](https://itunes.apple.com/us/app/slack/id803453959?mt=12)

Slack is doing it right in terms of chat. It's so straightforward. Slack is a little more complex than the Kickball chat needs to be (ex - I don't think we'll need file sharing?) but the way the conversations are organized & how easy they are to start - are both things to aspire to w/ my design. 

## Leaderboards & Stats

### App Store Top Charts

Getting super meta here. I was looking for an app that had a really obvious sort selector. In my experience building dashboards for users within other softwares, I notice that people don't use the sort filters proportionally to how useful they are, and I hypothesize that it's because they're buried under an ambiguous funnel icon. 

A couple apps with sort filters that I use were Modcloth and Amazon - but I was actually disappointed with how un-obvious they were. So for this research, I actually went to the app store itself to look for a better example, and noticed that they had the top charts page - with three ways to sort - paid, free, and top grossing - all in a horizontal nav. 

I loved it because it's low profile but still pretty obvious.

This only works when you have a few metrics to sort by, and in this case, we do. I suppose you could always have navigation arrows if you had to extend the metric list. 

# User Studies
## Set 1 - Kickball 

### Personas 
#### Lindsey D - 22, Female 
UT Sophomore socialogy major, from Iowa and new to Austin. Coaching so she can make friends. She wears shorts and t-shirts always and lives on campus. She's often got her headphones in jammin' to 90s Brooks & Dunn songs. 

#### Matt C - 31, Male
Accountant in Miami, florida. Introvert who just loves sports and no one else wanted to coach. He has a lab mix named Bax but no kids. He eats Chili's probably too much, and is currently re-watching Louie Season 3. 

#### Eileen M - 51, female. 
Eileen has two grown kids. She mostly shops at Kohl's and wears a lot of the color turquoise. She has an iPhone and is pretty tech savvy for an older lady (or she likes to think so). She's an early bird. 

### User Stories
As a team captain, I need to receive notifications so I can give my team updated information. 

As a team captain, I need to be able to forward notifications to my team quickly so I can relay information at a moment's notice. 

### Scenarios

Matt had a late night last night and is feeling pretty crappy today, which sucks because he has a playoff game later. He's trying to decide whether to have a mimosa brunch with his bro, or just take it easy so he can bring his A game tonight. It depends on who he's playing - the Lake Austin Otters (we got this) or Pleasant Valley Parrots (oh shit.) 

Lindsey had a super crazy day at work today and didn't notice that there was a 80% change of thunderstorms. It's 5 and there is a practice at 6. The team really needs to shape up before the big game Saturday, and she only wants to cancel if the league makes her, but the league hasn't sent any notifications so she wants to let her team know as soon as she knows. 


### Use Cases

1. Check weather app again
2. Close weather app
3. Go to league announcements page
4. refresh
5. refresh
6. oh, there's a subscribe button
7. subscribe to updates
8. wait
9. receive update
10. read prompt to dismiss or share with team
11. hit "share"
12. prompted to add text "looks like we have to cancel tonight, stay tuned for practice reschedule"
13. hit send
14. confirmation displayed


### User Flow 

// = Displayed to user

~ = Action taken by user

	//Receive notification
	~Dismiss 
		//End Flow
	~Share
		~Add text
			//Confirm? 
				~Yes
					//Confirmation Screen
				~Cancel
					//Back to Receive Notification Screen
		~Just Send
			//Confirm? 
				~Yes
					//Confirmation Screen
				~Cancel
					//Back to Receive Notification Screen

# Paper Prototype

So my first attempt at paper prototype testing was unsuccessful. Here are some of my failure points:

* Recruitment: user was not an iPhone user and was therefore unfamiliar with how you normally behave w/ notifications.
* Handwriting: user was squinting to read my handwriting, which would not happen in a real app scenario, and the help I gave him to read definitely dirtied my results.
* Methodology: Instead of sketching elements, I tried to sketch out every possible state the screen could be in after interactions, which was super confusing

So I learned a lot, but didn't feel like I understood the failures of my flow, so I tried again

![Picture](https://github.com/amaliebarras/kickball-app/blob/master/paperprototype/all_together.png)

With this cleaner prototype, I got some great feedback on the flows themselves. 

* Hierarchy: It matters a lot in mobile since everything is so small, but you have to get creative with how you show it since only a certain range of type sizes will work on a mobile device
* Consistency: The user should be able to see the notification that they are commenting on, the whole time across the journey. 
* Tie it in: This flow doesn't exist in a vacuum - what can the user do after? (This is in the prototype, but the "go to chat" button was drawn in later

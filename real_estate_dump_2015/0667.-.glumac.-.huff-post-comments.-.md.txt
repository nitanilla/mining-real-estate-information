# HuffPo Voices 
### Make yourself heard. 
# 
![Huff icon](http://www.glumac.net/HuffPoVoices.jpg)

####Description:

HuffPo Voices is an audio commenting widget that gives readers a chance to hear comments from the mouths others in  Huffington Post’s vibrant and diverse community.  View a [HuffPo Voices ](http://huffpo-audio-comments.herokuapp.com/) first prototype on Heroku. (Tested only in Chrome.)

####The Idea:

This app would occupying a modicum of page real estate (happily existing next to traditional written comments)  while packing a wallop of intriguing content.  Users will be encouraged to continually contribute to article comment playlists with the tantalizing possibly of earning more “airtime” for their future remarks beyond the initial 6 second limit via “Amplify” up-votes. 

####MVP: 
This MVP prototype of HuffPo Voices enables a commenter to record, approve, and upload a six second message (with a countdown timer). Recording is handled within the browser with HTML5 and Javascript using Web Audio API, and delivery of .wav files to the Heroku AWS server is handled via Carrierwave.  A database of comments is stored in a PostgreSQL database, managed with Ruby/Rails. 

#### The Experience
It was most fun to experiment with Web Audio API, which is approaching something of a tipping point of browser adoption. As Heroku is read-only for content, it took a bit of craftiness to enable file uploads without use of a separate storage server. Also the handling of file uploads slightly complicates the JSON-ification of the rails app, so I de-Angularized to focus on making my own Web Audio API implementation.

#### Some Next Steps: 
* Create user login / avatars, and variable time recording limits.   Currently the app is sketched out for a single (new) user. 
* Develop a clean and compact circular javascript player/playlist based on the aesthetic of [JQuery knob]( http://anthonyterrien.com/knob/) and [Circle Player](https://github.com/maboa/circleplayer). Currently the app is using the standard html5 audio skin. My photoshop rendering of one concept is above. 
*  Complete Angular [refactoring](https://shellycloud.com/blog/2013/10/how-to-integrate-angularjs-with-rails-4]) of Rails CRUD. 
*  Enable real time updates for concurrently signed-in users, as I did in my laptop choir app   [MIDI Flashmob](http://huffpo-audio-comments.herokuapp.com/) .
* Convert to a compressed audio format, and possibly merge clips on the server before delivery for better performance with the intended concurrent play. 
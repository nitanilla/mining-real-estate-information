# Three Toe: An SMS Autoresponder using the Twilio API

Author: [Colin Devroe](http://cdevroe.com)

Three Toe accepts a [Twilio](http://twilio.com) webhook POST and responds to the sender with the contents of a TXT file (based on the body of a sender's message) if found.

1. Sender TXTs Twilio powered phone number with "T0001"
2. Twilio sends webhook to Three Toe
3. Three Toe looks for "T0001.txt" in /responses
4. If found, responds. If not found, responds with responses/notfound.txt

This simple script was built to scratch an itch and learn the basics of the Twilio API. You can [read more about the backstory on my blog](http://cdevroe.com/2016/06/24/three-toe-a-simple-sms-autoresponder-on-top-of-the-twilio-api/).

## Installation

1. Copy entire app to server
2. Copy app/config-private-sample.php and create app/config-private.php
3. Fill in Twilio account information, phone numbers, app URL, and password in your config-private.php
4. Open /configure to create, edit, and delete codes and responses

(You'll need to set up a phone number on Twilio with a webbook that points to your URL.)

## Version History

### 0.3.0 - June 28, 2016
  - New: Bootstrap-based UI
  - New: About page.
  - Fixed: Mobile considerations

### 0.2.1 - June 27, 2016
  - Fixed: App determination if Twilio is sending a request or not

### 0.2.0 - June 27, 2016
  - Added: Code & Response configuration panel
  - Update: Generic "not found" response to make less real estate specific
  - Updated readme

### 0.1.0 - June 24, 2016
  - Initial app
  - Basic responses based on text file
  - Basic response if no code found
  - Readme

JustInThyme

Installation:
If you've not signed up for a trial account, do so now by navigating to https://www.twilio.com/try-twilio. Navigate to the Github repository linked below. Clone the repository and load it in a text editor of your choice. Edit the code base to include your Twilio credentials (TwilioSend.java, lines between 11&13, enter token information; phone number goes on line 23). Go to the application.properties file and change the port number to match the port number in your MAMP settings. Be sure to start your Start your servers with MAMP. Use Gradle to bootRun the application file. Navigate your brower to localhost:8080/JustinThyme. Have fun!


URL to the repo: https://github.com/JasonOnes/JustinThyme.git

URL for wire-frames and page flows: https://tinyurl.com/yb5t8xl5

URL to the test plan: https://tinyurl.com/y8s46hhv

The Elevator Pitch: An app for people who want to know when, and get reminders to, plant vegetable seeds. It's useful for novice and intermediate growers alike. The novice user can discover vegetables that grow easily in their region, and the intermediate user can keep track of the seeds they have. All users can use JustinThyme to receive text messages when it is time to plant specific seeds.



Brief:
The aim of this website is to notify users of when to plant some seeds, just in time! It also aims to provide users with information regarding when to plant certain seeds, and to give suggestions on which seeds to plant if they don't know where to start in the process. The target audience for this website is those that want to be reminded of when to plant seeds. They could be a beginner grower who doesn't really know which seeds to plant, to an intermediate grower who wants to keep track of their seeds on hand, and be reminded of when to grow them. This website is for people with access to gardening spaces, whether it be at their own home and at a community plot. The amount of space needed is varied for different seeds and is not within the scope of this website to provide that information. The target audience, demographically, is varied in age... A very young to a very old person with access to the internet could access the website. If they have the text notifications enabled, they're within the age range of a cell phone user. The target audience can access the site via phones, tablets, or desktops... But without access to a cell phone, one cannot utilize the benefit of the notifications available from the website. The look of the site feels green and naturey; the feel is excitement for growing something to eat for yourself and you are anticipating the grow season... It'll have a little splash page with a quick ditty of how to utilize the web app.

User Stories:
User #1 
  Rebecca comes to the site, doesn't have an account but would like one. She likes the splash page and is so impressed she continues to the sign-up page. All her info (name, password, area, phonenumber)is valid and she is redirected to her brand new dashboard which contains a list of vegetables available to plant in her area. She chooses carrots, peas, and onions and decides to ignore brussel sprouts and squash because, well squash. After making her selections her dashboard is refreshed. She is happy with her choices and sets reminders for peas and carrots but not onions. Rebecca (not Becky!) has a multitude of things on her agenda other than admire our beautiful pages so she logs out.
  
User #2
  Tom already has an account but realizes that carrots are dirt cheap and not worth the real estate in his meager garden. He successfully logs in with his username and password, goes to his dashboard where he removes carrots from his list. Upon removing carrots from Tom's list the reminder for carrots is automatically set to OFF so he won't be bothered. He views his updated dashboard and is content, so content he logs off.
 
User #3
  Hula is a current user who is happy with the product but is moving to sunnier climes. She wants to keep using Justin Thyme at her new abode and wants to update her profile with her new setting. She logs in and at her dashboard selects Edit Profile from the navbar at the top. Selecting that button brings up the edit page where she changes her AREA from a dropdown menu and submits. Her seed list on her dashboard is now empty with the requisite suggested ten (five?) vegetable options for her new home displayed for her to choose from. She chooses tomatoes and broccoli with reminders set for both, logs out and gets back to packing.
  
User #4
  Randy's wife, who is a vegetarian, has just left him and the reminders to plant seeds of her favorites are too much for him to bare. Through his tears he somehow manages to log in with his password and immediately at his dashboard clicks the opt-out button on the navbar. He is directed to a page asking him to confirm his desire to leave (more sobbing) where he clicks yes. Behind the scenes Randy's profile is deleted from the database.

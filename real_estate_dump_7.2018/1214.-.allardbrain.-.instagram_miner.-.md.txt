# Instagram Miner
Instagram Miner allows a user to view & save all posts made with a specific hashtag within a time range.

![Instagram Miner Campaign Detail](/ig_miner_app/static/chicago_bandits.png) 

Table of Contents
----------
- [Technologies Used](https://github.com/erinallard/instagram_miner#technologies-used)
- [Installation](https://github.com/erinallard/instagram_miner#installation)
- [Access Tokens and Secret Keys](https://github.com/erinallard/instagram_miner#access-tokens-and-secret-keys)
- [Database Setup](https://github.com/erinallard/instagram_miner#database-setup)
- [Admin Account Setup](https://github.com/erinallard/instagram_miner#admin-account-setup)
- [Server Setup](https://github.com/erinallard/instagram_miner#server-setup)
- [Basic Usage](https://github.com/erinallard/instagram_miner#basic-usage)
- [Known Issues](https://github.com/erinallard/instagram_miner#known-issues)
- [Choices I Made](https://github.com/erinallard/instagram_miner#choices-i-made)
- [Version 2.0](https://github.com/erinallard/instagram_miner#version-20)
- [About the Author](https://github.com/erinallard/instagram_miner#about-the-author)


Technologies used
----------
- Python backend
- Django web framework
- Postgres database
- Psycopg2
- HTML/CSS
- Bootstrap
- Instagram API

Installation
-----------
Clone this repo to your machine. If you need help with this part, GitHub has [great documentation](https://help.github.com/articles/fork-a-repo/) -- follow along up to, but not including, Step 3.

We need to create a virtual environment in our copy of the repository, so that the technologies you download to make Instagram Miner work don't interfere with any other technologies you may have installed on your computer. To do this, make sure you're in the ` instagram_miner/ ` directory then type the following in your Terminal:

` $ virtualenv env `

Next, type ` $ source env/bin/activate ` to create a "bubble" around the workspace.

You will see that there is now '(env)' in front of the command line prompt: ` (env) $ `

It is worth mentioning the .gitignore file at this point. There are certain files that we don't want or need to commit to the repository, and the names of those files will go inside a different file called ` .gitignore `. When we eventually do make our commits, git will automatically ignore (ha, ha) the files listed inside the .gitignore file. The .gitignore file is already included in the instagram_miner repository you cloned -- you don't need to do anything here.

We now need to install all the libraries and technologies that appear in the file ` requirements.txt `. From the ` instagram_miner/ ` directory (which you should still be in), simply type the following into your Terminal:

` (env) $ pip install -r requirements.txt `

You should see a success message similar to this at the bottom of the Terminal window:

``` python
Installing collected packages: Django, httplib2, psycopg2, requests, simplejson
Successfully installed Django-1.9.5 httplib2-0.9.2 psycopg2-2.6.1 requests-2.10.0 simplejson-3.8.2
```
Access Tokens and Secret Keys
----------
In the ` instagram_miner/ ` directory create a file called 'secrets.sh'. On a Mac, the Terminal command is: 

` (env) $ touch secrets.sh `

Add these two lines to ` project/secrets.sh `:

``` python
export ACCESS_TOKEN=''
export SECRET_KEY='' 
```

You will need an Instagram ACCESS_TOKEN in order to make the API call. Obtain one from [PixelUnion](http://instagram.pixelunion.net/) (Instagram account required). Copy and paste the ACCESS_TOKEN into ` project/secrets.sh ` like so (do not include the brackets):

` export ACCESS_TOKEN='<access_token>' `

You will need a SECRET_KEY for the Django app. Obtain one from [MiniWebTool](http://www.miniwebtool.com/django-secret-key-generator/). Copy and paste the SECRET_KEY into ` project/secrets.sh ` like so (do not include the brackets):

` export SECRET_KEY='<secret_key>' `

 **DO NOT commit secrets.sh to your repository!** Instead, add ` secrets.sh ` as a line in your ` project/.gitignore ` file:

 ``` python
.DS_STORE
*.pyc
env/
secrets.sh
 ```

**Important!** We are not committing the ACCESS_TOKEN or SECRET_KEY to our repo for security reasons, but we still need to tell our app this info exists. To do this on a Mac, we need to source the secrets.sh file while in our ` project/ ` directory in **every** Terminal tab we'll be using for this project. 

` (env) $ source secrets.sh `

Database Setup
-----------
Download [Postgres](http://postgresapp.com/) if you don't already have it, and install it. Make sure it is running! If you're on a Mac, there will be a small black elephant in the upper right corner of your menu bar.

We can launch an interactive Postgres console in a Mac Terminal. Open a new Terminal tab. Source the environment again, just to be sure. From the ` instagram_miner/ ` directory, run the command ` (env) $ psql `. You'll know you're in the Postgres database when the ` $ ` at the beginning of your command line prompt is replaced with a ` # `.

To create a user, type the following command into the Terminal. Replace 'name' with your name (no white spaces!):

``` python
CREATE USER name;
CREATE ROLE
```

Next, we need to create the actual database. Type the following command into the Terminal. Replace 'db_name' with the name you want to give to the database (no white spaces!) and 'name' with the name you created for yourself in the previous step.

``` python
CREATE DATABASE db_name OWNER name;
CREATE DATABASE
```

Cool, now we have a database! We need to tell Instagram Miner that it exists. Find this chunk of text in your ` instagram_miner/ig_miner/settings.py ` file, and update the placeholder database text for 'NAME' with the 'db_name' you created in the previous steps. Update 'USER' with the 'name' you created in the previous steps.

``` python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'db_name',
        'USER': 'name',
        'PASSWORD': '',
        'HOST': 'localhost',
        'PORT': '',
    }
}
```

If you need more help, check out [this tutorial](https://github.com/DjangoGirls/tutorial-extensions/blob/master/optional_postgresql_installation/README.md) from [Django Girls](https://djangogirls.org/) on installing Postgres with Django.

Switch back to the first Terminal tab you created (make sure you're still in your virtual environment) and run ` python manage.py migrate ` in the Terminal. You should see a success message similar to this:

``` python
Operations to perform:
  Apply all migrations: admin, ig_miner_app, contenttypes, auth, sessions
Running migrations:
  Rendering model states... DONE
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying ig_miner_app.0001_initial... OK
  Applying ig_miner_app.0002_photo_campaign_id... OK
  Applying ig_miner_app.0003_auto_20160502_1503... OK
  Applying ig_miner_app.0004_auto_20160502_1520... OK
  Applying ig_miner_app.0005_auto_20160502_1536... OK
  Applying ig_miner_app.0007_auto_20160506_1330... OK
  Applying ig_miner_app.0008_auto_20160506_1424... OK
  Applying ig_miner_app.0009_auto_20160506_2116... OK
  Applying ig_miner_app.0010_auto_20160507_0832... OK
  Applying sessions.0001_initial... OK
```

Admin Account Setup
-----------
We're getting so close! Let's create an admin. Run this command in the Terminal and follow the prompts to enter your name, email and password:

` python manage.py createsuperuser `


Server Setup
-----------
Woo hoo! You're now ready to run your server! Using the same Terminal tab from the steps we just completed for the admin, type the following command in your Terminal:

` (env) $ python manage.py runserver `

If all went well, you'll receive a success message similar to this:

``` python
Performing system checks...

System check identified no issues (0 silenced).
May 07, 2016 - 17:10:58
Django version 1.9.5, using settings 'ig_miner.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
[07/May/2016 17:11:07] "GET / HTTP/1.1" 200 1439
[07/May/2016 17:11:07] "GET /static/css/ig_miner_app.css HTTP/1.1" 200 682
```

You can now visit the URL ` http://localhost:8000 ` in your web browser and you should see the navbar on the home page! There won't be any campaigns listed on the home page, because you haven't created any yet.

![Instagram Miner Homepage](/ig_miner_app/static/instagram_miner.png)


Basic Usage
-----------
### 1. Create a new campaign
* Visit ` http://localhost:8000/campaign/new/ ` or click the 'New Campaign' link in the top navbar.
* The Campaign Title should be unique and descriptive.

* The Start Date and End Date for a given hashtag query must be in increments of one whole day, and must be entered by the user as MM/DD/YYY. For example: 03/01/2016 to 03/02/2016. The start date must be in the past and the end date must be no later than the day the user is accessing the app.

* Enter the desired hashtag **without** the '#' symbol. It is a good idea to first check how many posts have been made using the hashtag you've chosen. Login to Instagram and search for the hashtag. The larger the number of posts associated with it, the slower the campaign_detail page will be to load. The data returned from a query on a hashtag with up to 35,000 posts should fit within the 5,000/hour rate limit, but the results page will take a long time to load.

### 2. Viewing your campaigns
* The home page provides an alphabetized list of your campaigns: ` http://localhost:8000/ `
* You can also access this list by clicking the link 'My Campaigns' in the top navbar.

### 3. Viewing your campaign details
* Clicking on a campaign title on the home page will take you to that campaign's detail page: ` http://localhost:8000/campaign/<pk> `, where ` <pk> ` is the primary key (id) associated with that campaign in the database. Remember to use the pagination feature at the bottom of each page to access all of the result-photos!

Known Issues
------------
- Throws errors if New Campaign form submission doesn't contain all fields.

- If there are lots of result photos, some may not render initially on the Campaign Detail page. You can refresh the page and they should appear. 

Choices I Made
-----------
- In order to reduce the risk of hitting the rate limit for the endpoint (5,000/hour), I sent a ` {'count': 100} ` parameter in the header of the GET request to the Instagram API. I tested this by pulling result photos for a hashtag with 1,550 posts. I expected to have 16 API hits but instead had 22, for an average of 70.5 results per page of the endpoint. The new_campaign view contains logic such that if the rate limit hits 4,999 the program will stop making API calls and will work with the data thus far obtained.

- The API call returns data for the time the photo was posted to Instagram as epoch time. The New Campaign form allows the user to enter start/end dates as strings, which are converted to epoch time. All date info is stored in the Postgres database as epoch time in order to more easily determine whether or not a photo was posted within the specified time range.

- I chose to focus my time on creating a web app with the requested primary functionality of making an API call and collecting photos from it. I opted not to include login/logout functionality for v1.0, but plan to include it in v2.0

- I listed the photo owner's Instagram username under each photo as a link. Someone who is considering using this person's photo for marketing purposes can first check out the user's other posts, to make sure they are not insensitive or inflammatory. 

- I added a place-holder button under each photo that will eventually allow a user to request permission directly from the photo's owner to use the photo for marketing purposes. 

- I used Django because I wanted to learn a new Python web framework. The documentation is AWESOME!

Version 2.0
-----------
- Add login/logout functionality so users' campaigns are visible only to them

- Explore parallel processing of many new campaign requests happening simultaneously

- Include error handling for an expired Instagram API access token

- Instagram requires that a developer "Only store or cache User content for the period necessary to provide your app's service." Campaigns could be deleted after 3-6 months of inactivity, with an email sent to the User before deletion. 

- Allow a user to delete a campaign they've created, and subsequently delte its associated photos from the database

- Allow a user to delete result photos from a specific campaign if they don't want to use that photo for marketing

- Allow a user to alter the campaign's date range if their initial inquiry yielded too many / not enough result photos

- Allow a user to request permission from the photo's owner to re-use the photo for marketing purposes

- Add tests

Many Thanks
-----------
...to StackOverflow user Bernard Parah [for their help with](http://stackoverflow.com/a/37094453/5166521) describing the steps to replicate my original Django app.


About the author
-----------
[LinkedIn - Erin Allard](http://www.linkedin.com/in/erinallard1 "Erin Allard's LinkedIn profile")

I'm a 2016 graduate of [Hackbright Academy](http://www.hackbrightacademy.com) in San Francisco, the leading full-stack engineering school for women. My background is in economics, commercial real estate and wealth-building education. I love [quilting](http://www.instagram.com/millennialquilter) and botanical art. 

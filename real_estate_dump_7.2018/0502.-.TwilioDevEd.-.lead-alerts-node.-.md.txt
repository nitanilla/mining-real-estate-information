<a href="https://www.twilio.com">
  <img src="https://static0.twilio.com/marketing/bundles/marketing/img/logos/wordmark-red.svg" alt="Twilio" width="250" />
</a>

# Instant Lead Alerts for Node.js and Express

This demo application shows how to implement instant lead alerts using Node.js and Express. Notify sales reps or agents right away when a new lead comes in for a real estate listing or other high value channel.

[Read the full tutorial here](https://www.twilio.com/docs/tutorials/walkthrough/lead-alerts/node/express)!


## Local development

To run this project on your computer, you will need to download and install either [Node.js](http://nodejs.org/) or [io.js](https://iojs.org/en/index.html), both of which should also install [npm](https://www.npmjs.com/). You will also need to [sign up for a Twilio account](https://www.twilio.com/try-twilio) if you don't have one already.

1. First clone this repository and `cd` into it.

   ```bash
   $ git clone git@github.com:TwilioDevEd/lead-alerts-node.git
   $ cd lead-alerts-node
   ```

1. Next, open `.env` at the root of the project and update it with
  values from your
  [Twilio account](https://www.twilio.com/console)
  and local configuration. You'll need to set
  `TWILIO_AUTH_TOKEN`, `TWILIO_ACCOUNT_SID`, and `TWILIO_NUMBER`.

  For the `TWILIO_NUMBER` variable you'll need to provision a new number
  in the
  [Manage Numbers page](https://www.twilio.com/user/account/phone-numbers/incoming)
  under your account.

  The `AGENT_NUMBER` variable represents the number alerts will be sent to. Please make sure you have allowed SMS to be sent to the Country this number belongs to on the [Global SMS Permissions page](https://www.twilio.com/console/sms/settings/geo-permissions). Also, if you are on a trial account, make sure you have verified this number on the [Verified Callers IDs page](https://www.twilio.com/console/phone-numbers/verified).

  The phone numbers should be in
  [E.164 format](https://www.twilio.com/help/faq/phone-numbers/how-do-i-format-phone-numbers-to-work-internationally).

  Run `source .env` to export the environment variables.

1. Navigate to the project directory in your terminal and run:

  ```bash
  $ npm install
  ```

  This should install all of our project dependencies from npm into a local `node_modules` folder.

1. To launch the application, you can use `node .` in the project's root directory. You might also consider using [nodemon](https://github.com/remy/nodemon) for this. It works just like the node command, but automatically restarts your application when you change any source code files.

  ```bash
  $ npm install -g nodemon
  $ nodemon .
  ```

### Docker local development

1. Install [Docker](https://www.docker.com/) and [docker-compose](https://docs.docker.com/compose/install/).

1. Make sure you performed step **2** on the previous section.

1. Copy the template .env file and set the required environment variables.You
   can find these values at https://www.twilio.com/user/account/voice and at
   https://dashboard.authy.com.

    ```bash
    cp .env.example .env
    ```
1. Load the variables in your session:

    ```bash
    source .env
    ```
1. Finally, run the following commands to start your Docker containers:

  ```
  $ docker-compose up -d
  ```

  Warning: If you previously ran  ```npm install``` locally, the node_modules folder will conflict with the file structure of the container when you run the above command. We recommended installing your node dependencies one folder up from the rest of your source code.

1. You can then visit the application at [http://localhost:3000/](http://localhost:3000/). If you're using [boot2docker](https://docs.docker.com/installation/mac/) to run Docker on OS X, you'll need to use the value of `boot2docker ip` instead of `localhost`.

1. To stop your containers, run `docker-compose stop`.

You can then visit the application at [http://localhost:3000/](http://localhost:3000/).

## Meta

* No warranty expressed or implied. Software is as is. Diggity.
* [MIT License](http://www.opensource.org/licenses/mit-license.html)
* Lovingly crafted by Twilio Developer Education.

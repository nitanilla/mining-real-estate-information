#Mission

## Pain Points:
While there are considerable number of resources available for users related to public safety, there do not seem to be any that provide the information in a frictionless way similar to what some commercial apps can deliver. It's really easy to find out what houses cost in a neighborhood I'm passing through via Redfin(or a host of other real estate apps that do a pretty good job), but not nearly as straight forward to find out how safe that neighborhood is.

Access to information that is both geo and time specific to the user at the point of inquiry, provided in the most frictionless way possible and optimized for mobile, is not an experience that currently exists but could prove extremely useful. The data is out there and we don't think this is an impossible challenge to meet.

This main focus will be to provide a user a quick checkin, to get safety related information based on publicly available resources. There is also the opportunity to provide complimentary activities and information which could be accessed by drilling further into the app. Here are a few examples, some low hanging fruit for this one but most appropriate only as a second phase:

- Anonymous reporting of suspicious or illegal activity to authorities.
- Machine learning algorithms based on aggregated data to provide predictive results
- Contact information for neighborhood groups in the area
- Links to other services like fire, police and emergency medical services in the area
- Data visualizations
- Push notifications for emergencies in the area
- Upload photo or video related to an event
- Make our data API (and possibly the piece that consumes/exposes it) publicly availble in hopes of increasing interest, reuse, etc. 
- Provide users with the ability to understand where the data comes from and how any rating or "level" is calculated.

## Design Criteria:
- Simple, elegant, clear communication
- Web app but think native experience, interaction
- Select or develop a strong collection of visual assets (icons) to help communicate information. 
- Use color to subtly convey emotion associated with safety: calm/caution/danger as well as night/day/morning/twilight


## Dates:
- August 10th first programming day
- August 17th Second programming day
- August 24th Judging and Presentation day

## Trello:
https://trello.com/b/Z4WXaHw2/neighborhood-intelligence

## Slack:
https://neighborhood-intellig.slack.com/messages/

## Machine Learning
http://burakkanber.com/blog/machine-learning-in-js-k-nearest-neighbor-part-1/


## Getting started:
- Open terminal and navigate to client > src >

```
npm install npm -g
npm install -g bower
npm install
bower install
```


## Troubleshooting

~~If you're receiving dependency errors you may be running a newer version of node than what is supported. Install [nvm](https://github.com/creationix/nvm) . Once installed type "nvm install 0.12.0" and then "nvm use 0.12.0". If you are having trouble getting nvm installed, see this issue for help: [https://github.com/creationix/nvm/issues/576](https://github.com/creationix/nvm/issues/576)~~

Updated package to use current node LTS 4.4.7. No longer need to run nvm to get an older version of node

## Git process

https://guides.github.com/introduction/flow/

## Data

### Neighborhood

https://www.phoenix.gov/nsd/programs/neighborhood-coordination

### City of Phoenix

https://www.phoenix.gov/OpenDataFiles/Crime%20Stats.csv


## Server 

### Install dependencies

npm install

### Boot your db

https://www.npmjs.com/package/mongodb#booting-up-a-mongodb-server

### Importing from csv via command line

Navigate to the server directory, make sure mongo is running

```
mongoimport -d server -c records --type csv --file ./public/data/crime-stats.csv --headerline
```


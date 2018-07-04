# PropertyWebBuilder Themable front end

> Built with vue and vuetify

Please help support this project by making a contribution to PropertyWebBuilder here: https://opencollective.com/property_web_builder

[![Gitter](https://badges.gitter.im/dev-1pr/1pr.svg)](https://gitter.im/property_web_builder/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=body_badge)

PropertyWebBuilder is a website builder for the real estate sector.  It can be adapted for use as a CRM, property listings site, vacation rentals listing site etc.

This project implements a new look and feel for PropertyWebBuilder.  The goal is to make it easier to customise and to provide more functionality.  As of March 2018, it is under active development and any help in completing it will be much appreciated.

## Collaborate with me

I would like this to be a reference implementation of building a front end with Vue / Vuetify and to involve as many collaborators as possible.  It is easy to run this project locally or to deploy your own instance with netlify by clicking the button below:

[![Deploy to Netlify](https://www.netlify.com/img/deploy/button.svg)](https://app.netlify.com/start/deploy?repository=https://github.com/etewiah/pwb-themes-base)

You can see a demo deploy here:

https://elated-mcclintock-50866b.netlify.com/

It consumes the public api of a Rails app running PropertyWebBuilder here:
https://pwb-jan-2018.herokuapp.com/api_public/v1/en/pages/home

You can change the backend (source of the public api) by editing the \_redirects file in the dist folder.

The main repo for PropertyWebBuilder is here:
https://github.com/etewiah/property_web_builder

Features I'm currently working on include:

* Allow site visitors to make some limited changes to the theme
* Add authentication so visitors can login to save their favourite properties
* Enable real time currency conversion


I also want to create first class documentation about this project.  To help with this, feel free to contact me directly or to raise an issue.


## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

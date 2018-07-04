# LOI CARREZ

> node.js workshop based on real estate

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Intro](#intro)
- [Workshop in 1 sentence](#workshop-in-1-sentence)
- [How to do that?](#how-to-do-that)
- [Stack](#stack)
- [Just tell me what to do](#just-tell-me-what-to-do)
- [Steps to do](#steps-to-do)
  - [Step 1 - Classified ad real estate definition](#step-1---classified-ad-real-estate-definition)
    - [To do](#to-do)
  - [Step 2 - Estimation from Meilleurs agents](#step-2---estimation-from-meilleurs-agents)
    - [To do](#to-do-1)
  - [Step 3 - UX/UI](#step-3---uxui)
    - [To do](#to-do-2)
  - [Step 4 - require('leboncoin')](#step-4---requireleboncoin)
    - [To do](#to-do-3)
  - [Step 5 - require('meilleursagents')](#step-5---requiremeilleursagents)
    - [To do](#to-do-4)
  - [Step 6 - node app.js](#step-6---node-appjs)
    - [To do](#to-do-5)
  - [Step 7 - UX/UI](#step-7---uxui)
    - [Todo](#todo)
- [Don't forget](#dont-forget)
- [Licence](#licence)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->


## Intro

*La loi Carrez* is a French law which obliges the vendor of a property lot to mention the surface area.

*La loi Carrez* is a good way to verify if a real estate classified ad is a good deal: you can check the price by square meter.

You could use the free website [meilleursagents.com](https://www.meilleursagents.com/) to know the average price by town (estimation)

In France, [leboncoin.fr](http://www.leboncoin.fr/) is the website leader of classified ad: minimalist UX and UI without registry.

## Workshop in 1 sentence

**Determine if the price of a real estate on leboncoin.fr classified ad is a good deal**

## How to do that?

By creating a link between [leboncoin.fr](http://www.leboncoin.fr/), [meilleursagents.com](https://www.meilleursagents.com) and the end-user.

## Stack

```txt
node.js + NPM + Material Design (mdl, bootstrap...) + Vanilla JS
```

## Just tell me what to do

1. Fork the project https://github.com/92bondstreet/carrez via `github`
1. Clone the project `git clone https://github.com/YOUR_USERNAME/carrez`
1. Follow the steps as breadcrumb.
1. Don't forget to commit and push

## Steps to do

### Step 1 - Classified ad real estate definition

What are the given properties for a real estate ad: town, area, type... ?

For example: https://www.leboncoin.fr/ventes_immobilieres/1076257949.htm?ca=12_s

#### To do

Define the JSON schema for a real estate leboncoin.fr classified ad.

Example of JSON Schema: [Basic example](http://json-schema.org/examples.html)

### Step 2 - Estimation from Meilleurs agents

What are the properties we need to provide to [meilleursagents.com](https://www.meilleursagents.com/) to compute an estimation ?

#### To do

Define the JSON schema to compute the square meter estimation for a real estate ad.

Exemple of estimation:
https://www.meilleursagents.com/prix-immobilier/#estimates

### Step 3 - UX/UI

How to create a connexion between the leboncoin ad and lacentrale?

#### To do

Write a User Flow

### Step 4 - require('leboncoin')

Create a module called `leboncoin`

#### To do

From the ad url, scrap the webpage and return the real estate properties in JSON format.

### Step 5 - require('meilleursagents')

Create a module called `meilleursagents`.

#### To do

From a real estate ad JSON object, determine:
* price for the square meter
* if it's a good deal

### Step 6 - node app.js

Build the node server.

#### To do

Build the Node server with Express.

### Step 7 - UX/UI

Let's go for the Web App !!

#### Todo

From a leboncoin real estate ad url, compute the price by square meter and give a feedback to the user about the deal (good or not).

## Don't forget

**Focus on codebase and UX/UI**

## Licence

[Uncopyrighted](http://zenhabits.net/uncopyright/)

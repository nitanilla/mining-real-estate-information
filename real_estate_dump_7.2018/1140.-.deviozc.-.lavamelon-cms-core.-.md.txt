# Lavamalon CMS

## Overview

A content management system backend based on Sails.js that supports multi-site.

## Getting start

Setup database connection in /config/connections.js

Setup server environment in /config/env/

```bash
sails lift
```

##RESTful API

###User

| Endpoint | Description | Parameters |
| ---- | --------------- | ---------------------|
| POST /users | Add a user (Admin only) | email, password, fullName, admin(boolean) |
| PUT /users | update a user (Admin only) | id, email, password, fullName, admin(boolean) |
| POST /users/login | Login user | email, password |
| POST /users/logout | Logout user (user only) | none |
| GET /users/me | get user profile (login user only) | none |

###Site

| Endpoint | Description | Parameters |
| ---- | --------------- | ---------------------|
| POST /sites | Add a site (Admin only) | domain |
| POST /users/:userId/sites/:siteId | Add site owner (admin only) | none |

###Content Type - Article

A generic content type that stores title and content

| Endpoint | Description | Parameters |
| ---- | --------------- | ---------------------|
| POST /articles | Add an article (site owner only) | json {"template":"template", "section": "section", "images":["file_id"], "domain": "domain", "en":{"title":"title", "body": "body"}} |
| PUT /articles/:articleId | Edit an article (site owner only) | same as POST |
| DELETE /articles/:articleId | Delete an article (site owner only) | none |
| GET /sites/:domain/articles | Get all articles of the domain | none |
| GET sites/:domain/section/:section/articles | Get all articles of a section of a site | none |

###Content Type - Property

A genertic content type for real estate property

| Endpoint | Description | Parameters |
| ---- | --------------- | ---------------------|
| GET /properties?domain=domain&mls=mlsID&agent=agentID&type=propertyType&page=PageNum&swk=-125.40&swC=0.193&nek=-100.85&neC=49.37&price_low=200000&price_high=250000 | get properties, limit 100 listings per request. Use page param to navigate | queryString - domain(required), mls(mls ID, optional), agent(agent V number, optional), type(property type, eg. House/Single Family, optional), page(page index, start from 0, optional) |
| GET /properties/:propertyId | get a property| none |
| PUT /properties/:id | Edit a property (site owner only) | same as POST |
| DELETE /properties/:id | Delete a property (site owner only) | none |

###Content Type - File

Content type that keeps teack of uploaded file

| Endpoint | Description | Parameters |
| ---- | --------------- | ---------------------|
| POST /files/upload | upload a file (site owner only) | domain, file(octet-stream) |
| GET /sites/:domain/files | Get all files on the site | none |
| GET /sites/:domain/images | Get all images on the site | none |
| DELETE /files/:fileId | Delete a file (site owner only) | none |
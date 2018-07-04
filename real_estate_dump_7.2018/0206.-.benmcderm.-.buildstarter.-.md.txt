# Buildstarter

[Buildstarter live][heroku]

[heroku]: www.buildstarter.co/

Buildstarter is a web application that allows users to crowdfund real estate investments.  

Buildstarter is a single page application built using React.js, the Flux data flow design pattern, a PostgreSQL database, and a Ruby on Rails back-end.

## Features & Implementation

### Single-Page App

Buildstarter is a single-page application with all content delivered on one static page using asynchronous API calls to the backend.

### Design Docs
* [View Wireframes][views]
* [React Components][components]
* [Flux Cycles][flux-cycles]
* [API endpoints][api-endpoints]
* [DB schema][schema]

[views]: docs/views.md
[components]: docs/components.md
[flux-cycles]: docs/flux-cycles.md
[api-endpoints]: docs/api-endpoints.md
[schema]: docs/schema.md

### Project Browsing

Projects can be browsed using the `BrowserIndex` component. The index implements a category search so that users can find projects that pertain to their own interests.

The index is composed of `BrowserIndexItem` components. `BrowserIndexItem` components display all the necessary details for a quick glimpse into the real estate investment.

### Project Viewing

Projects are viewed with a `ProjectDetail` component. The total investment in a project is calculated and updated dynamically.

Only logged in users are allowed to make investments in a project.

### Project Creation

Projects are created with a `ProjectForm` component. Users can add projects they'd like to receive funding for via a simple form.

### Search Bar

The dynamic search bar overrides the original `navBar` component, allowing users to search for projects by Name, Description, or Rating.

### Current User Menus

When a user is logged in, they can hover over their username in the `navBar` in order to see a drop down with options for 'Profile' and 'Logout'.

The users's Profile will display any recent investments they've made and which project it relates to.


## Future Direction for the Project

Features below will be implemented in a future version of this project:


### Likes, Comments, and Updates

The `ProjectDetail` component will allow users to post likes and comments, and founders to post updates.

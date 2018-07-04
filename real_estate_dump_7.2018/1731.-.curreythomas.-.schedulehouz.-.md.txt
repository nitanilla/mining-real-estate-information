# ScheduleHouse User Stories

> As a _type of user_, I want _some goal_ so that _some reason_.

## Overview

Showing scheduling and management for real-estate agents and home buyers.

## Search Properties

As a user, I want to search my MLS listings in the following ways:

  - MLS #
  - Street Address
  - Square Footage
  - Number of Bedrooms
  - Number of Bathrooms

Once a single property is selected, display the property details based on the current user's role. See **Display Property Details (By Agent)** and **Display Property Details (By Buyer)**.  

## Sign Up

As a potential user of the system, I need a way to sign up and provide my personal details.  I want the option to sign up as one of the following roles:

  - Agent
  - Buyer

As a potential home buyer, I wish to indicate which agents I am currently working.  

## Sign In

As a user, I need a way to sign into the system so that I can access my relevant information.  

## Distinguish Roles

As an administrator of the system, I need to designate users into one of the following roles. Only an administrator can place a user in a role.

  - Agent
  - Buyer
  - Administrator.

As a potential home buyer, I need to:

  - Access my biographical information
  - Search properties
  - View property details
  - Request showings
  - Rate houses I visit during a showing.

As a realtor, I need to:

  - Access my biographical information
  - Search properties
  - View property details
  - Schedule showings
  - Rate houses I visit during a showing

##  Display Property Details (By Agent)

As a real estate agent, I want to view the public _and private_ details for a specific property.

See [Property Details Data Elements](/schedulehouse/data#property-details).

##  Display Property Details (By Buyer)

As a potential home buyer, I want to view the public details for a specific property.

See [Property Details Data Elements](/schedulehouse/data#property-details).

## Schedule Showing by Agent

As a real estate agent, I want to schedule a showing of a property from the **Property Details Page** (See **Display Property Details By Agent**). Scheduling involves a real estate agent selecting a buyer, selecting a schedule date, and selecting available start and end times for the property.

See [Showing Data Elements](/schedulehouse/data#showing).

## Request Showing by Buyer

As a potential home buyer, I want to request a showing of a property from the property details page (See **Display Property Details By Buyer**).  Requesting involves selecting a date, reviewing available times for the property, and selecting an available start and end time.

See [Showing Data Elements](/schedulehouse/data#showing).

## Map Property

As an authenticated user, while I'm viewing the details of a specific property, I want to see where a property is located on a map.  

## Search Buyers By Last Name

As a real estate agent, I want the ability to search buyers by Last name.

Once selected, **Display Buyer**.  

## Browse Buyers from A to Z

As a real estate agent, I want the ability to browse buyers by last name.

Once selected, **Display Buyer**.

## Display Buyer

As a real estate agent, I need a **Buyer Details Page** to view the details on an individual buyers.

See [Buyer Elements](/schedulehouse/data#buyer).

## Display Calendar for an Agent's Showings

As a real estate agent, I want to see a calendar that displays my related showings for _all_ the properties for _all_ my buyers.  Each showing on the calendar should display:  

  - Showing Start Time
  - Showing End Time
  - Property Street Address
  - Buyer Last Name

See [Showing Data Elements](/schedulehouse/data#showing).

Selecting a showing on the calendar provides the following options:

  - Navigate to the **Buyer Details Page**
  - Navigate to the **Property Details Page**
  - **Filter Calendar for Buyer's Showings**
  - **Filter Calendar for Property's Showings**
  - Navigate to the Realtor's **Daily Showing Schedule Page**
  - Navigate to the Buyer's **Daily Showing Schedule Page**
  - Navigate to the Property's **Daily Showing Schedule Page**

## Filter Calendar for Buyer's Showings

As a real estate agent, I want to see a specific buyer's schedule.  I want to see a calendar that displays _all_ the showings for a _specific_ buyer.  Each showing on the calendar should display:  

  - Showing Start Time
  - Showing End Time
  - Property Street Address
  - Buyer Last Name

See [Showing Data Elements](/schedulehouse/data#showing).

Selecting a showing on the calendar provides the following options:

  - Navigate to the **Buyer Details Page**
  - Navigate to the **Property Details Page**
  - **Filter Calendar for Property's Showings**
  - Navigate to the Realtor's **Daily Showing Schedule Page**
  - Navigate to the Buyer's **Daily Showing Schedule Page**
  - Navigate to the Property's **Daily Showing Schedule Page**

## Filter Calendar for Property's Showings

As a real estate agent, I want to see when a specific property is available for showing.  I want to see a calendar that displays all showings for a _specific_ property across all realtors.  Each showing on the calendar should display:  

  - Showing Start Time
  - Showing End Time
  - Property Street Address
  - Buyer Last Name

See [Showing Data Elements](/schedulehouse/data#showing).

Selecting a showing on the calendar provides the following options:

  - Navigate to the **Buyer Details Page**
  - Navigate to the **Property Details Page**
  - **Filter Calendar for Buyer's Showings**
  - Navigate to the Realtor's **Daily Showing Schedule Page**
  - Navigate to the Buyer's **Daily Showing Schedule Page**
  - Navigate to the Property's **Daily Showing Schedule Page**

## Display Realtor Showing Schedule for a Specific Day (Daily Showing Schedule Page)

As a real estate agent, I want to see my showing schedule for a specific day on a **Daily Showing Schedule Page**.

Selecting an item on the Showing Schedule provides the user with the following options:

  - Route the app to the **Buyer Details Page**.
  - Route the app to the **Property Details Page**.
  - Route the app to the Buyer's **Daily Showing Schedule Page**.
  - Route the app to the Property's **Daily Showing Schedule Page**.

## Display Buyer Showing Schedule for a Specific Day (Daily Showing Schedule Page)

As a potential home buyer, I want to see my showing schedule for a specific day on a **Daily Showing Schedule Page**.

Selecting an item on the Showing Schedule provides the user with the following options:

  - Route the app to the **Buyer Details Page**.
  - Route the app to the **Property Details Page**.

## Display Property Showing Schedule for a Specific Day (Daily Showing Schedule Page)

As a real estate agent, I want to see the showing schedule for a specific property for a specific day on a **Daily Showing Schedule Page**.

Selecting an item on the Showing Schedule provides the user with the following options:

  - Route the app to the **Buyer Details Page**.
  - Route the app to the **Property Details Page**.
  - Route the app to the Buyer's **Daily Showing Schedule Page**.
  - Route the app to the Realtor's **Daily Showing Schedule Page**.

## Map Property (Property Details Page)

As an authenticated user of the system, when I am viewing property details on the **Property Details Page**, I desire the need to see where a specific property is located on a map so that I can drive to the property.

## Map Properties (Map Properties Page)

As an authenticated user of the system, when I am looking at my showing schedule, I desire the need to see where a specific set of properties are located on a map so that I can drive to the verious properties.

## Reveal Mapped Property Details (Map Properties Page)

Selecting a specific mapped property on the map reveals the following property details:

  - Address
  - Price
  - Photo
  - Link to **Property Details Page**.
  - Navigate my vehicle to the property address.

## Rate houses

As an authenticated user of the system, I need the ability rate a house during or after the designated showing start time.  I would prefer to provide my ratings on the **Property Details Page**.  

Do not allow me to provide a rating until the designated showing start time.

As a potential home buyer, I need the ability to provide the following feedback on a property:

  - Buyer Interest Rating
  - Overall Experience Rating
  - Buyer Price Opinion Rating

As an agent, I need the ability to provide the following feedback on a property:

  - Agent Price Opinion Rating

## SMS - Buyer Sends Link to Property (Property Details Page) to Agent

As a potential home buyer, I wish to let my agent know I am interested in a particular home so we can have a conversation by text messaging one another.

## SMS - Agent Sends Link to Property (Property Details Page) to Buyer

As an agent, I want to send a text that includes a link to the Property Details Page so the buyer can review the property.

## Adjust Agent Showing Schedule

As a realtor, I need to adjust my showing schedule for a specific day on a **Daily Showing Schedule Page**. I'd like to reorder my showings by dragging items above or below one another.  

Once saved, SMS Buyer to notify of schedule change.
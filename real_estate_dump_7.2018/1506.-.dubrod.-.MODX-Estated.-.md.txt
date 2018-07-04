# MODX-Estated

> A MODX Extra for www.estated.com real estate data service

## Dependencies:
1. www.Estated.com API Key

## Features:
1. Estated Address Look up via PHP Snippet
2. Only Looks up Addresses for the template ID specified in System Settings.
3. Saves Estated data back to resource TVs so it's cached and usable like normal MODX data
4. Updates listings only when you hit the Estated Data Resource so you don't burn up API queries.
5. Template Variable option to exclude resource from lookup so you don't burn up API queries.
6. A chunk to display all parameters as a 2 column list.

## Usage:
1. Install package
2. Go to System Settings; Update API Key and Templated ID used for Individual Listings
3. Go to Template used for Individual Listings and assign the *Estated* TVs
4. Create a resource for your listing. Info Required: Street, City, State, Zip
5. Go to `/estated-lookup.html`
6. Clear Cache to recache resources if necessary.

### Current Parameters being Saved:

 - Zoning Category
 - Zoning Description
 - Acres
 - Year Built
 - Beds
 - Baths
 - Total Size
 - Garage Size
 - Architecture Type
 - Exterior Wall Type
 - AC Type
 - Category
 - Condition
 - Pool Type
 - Quality
 - Roof Type
 - Value

 Full List of available parameters you can add: https://estated.com/developers/docs/schema

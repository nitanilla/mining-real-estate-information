User Stories

As a real estate associate
I want to record a building
So that I can refer back to pertinent information

Acceptance Criteria:

*I must specify a street address, city, state, and postal code
*Only US states can be specified
*I can optionally specify a description of the building
*If I enter all of the required information in the required format, the building is recorded.
*If I do not specify all of the required information in the required formats, the building is not recorded and I am presented with errors
*Upon successfully creating a building, I am redirected so that I can record another building.

As a real estate associate
I want to record a building owner
So that I can keep track of our relationships with owners

Acceptance Criteria:

*I must specify a first name, last name, and email address
*I can optionally specify a company name
*If I do not specify the required information, I am presented with errors
*If I specify the required information, the owner is recorded and I am redirected to enter another new owner

As a real estate associate
I want to correlate an owner with buildings
So that I can refer back to pertinent information

Acceptance Criteria:

*When recording a building, I want to optionally associate the building with its rightful owner.
*If I delete an owner, the owner and its primary key should no longer be associated with any properties.

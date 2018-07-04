# Ruby Comprehensive Lab

In this lab we'll be writing a collection of Ruby classes for a real estate app to manage apartments. Use the same approach as you did for the car lot assignment: You are not writing the actual higher-level app itself, but you should have test files that verify the behavior and interactions of your classes.

## Classes

### `Building`
* has an address
* has many apartments
* the list of apartments should not be modified directly (bonus: actually prevent it from being modified directly)
* has a method to add an apartment
* has a method to remove a specific apartment by its number, which raises an error if the number is not found or the apartment currently has any tenants (bonus: allow overriding this constraint)
* has a total square footage, calculated from all apartments
* has a total monthly revenue, calculated from all apartment rents
* has a list of tenants, pulled from the tenant lists of all apartments
* has a method to retrieve all apartments grouped by credit rating (bonus: sort the groups by credit score)

### `Apartment`
* has a number, rent, square footage, number of bedrooms, and number of bathrooms
* has many tenants
* the list of tenants should not be modified directly (bonus: actually prevent it from being modified directly)
* has a method to add a tenant that raises an error if the tenant has a "bad" credit rating, or if the new tenant count would go over the number of bedrooms
* has a method to remove a specific tenant either by object reference *or* by name (bonus: do this without checking classes), which raises an error if the tenant is not found
* has a method that removes all tenants
* has an average credit score, calculated from all tenants
* has a credit rating, calculated from the average credit score using the logic below

### `Tenant`
* has a name, age, and credit score
* has a credit rating, calculated from the credit score as follows:
  * 760 or higher is "excellent"
  * 725 or higher is "great"
  * 660 or higher is "good"
  * 560 or higher is "mediocre"
  * anything lower is "bad"

Homework 11: Add Search and GIS Computatibilty to Elegant Props
====

### Tasks 1 through 10 constitute Homework 11. __Due date is Thursday, May 10__ by 11:59pm. Submit by pushing to your github repository.

### This final assignment is based on the ongoing Elegant Properties application we have been working on AND the Lab 12 (https://github.com/rmedinahu/cs350lab12/blob/master/README.md) Geopy exercise.

#### NOTE: Solutions to homework 9 and 10 are included in this repository as separate commits. You can view those by using the links below. Commits are labeled accordingly.

Homework 9 ==> https://github.com/rmedinahu/cs350-props-03/tree/89aaa33ae21c531a2de2f995eb2933fc6e2a9ff0

Homework 10 ==> https://github.com/rmedinahu/cs350-props-03/tree/a1aca9269f43604c87d1001cc13435f911042dde

# Get Started
1. __fork__ this repository (https://github.com/rmedinahu/cs350-props-03) to your GitHub account (use the fork button at the top)
2. __clone__ your forked repo to your local working directory
3. cd to repository/project root
... you know the drill...
4. create a virtual environment for this project
5. Run: `pip install -r requirements.txt` (will install django and geopy)
6. Setup the django app: `python manage.py migrate`
7. Load the database with sample data containing a set of real estate properties, transactions, and messages: 

`python manage.py loaddata property-testdata`

`python manage.py loaddata transaction-testdata`

`python manage.py loaddata message-testdata`

8. Create a superuser for the app: `python manage.py createsuperuser`
9. Run the test server: `python manage.py runserver` and make sure the page loads as expected.


TODO: properties App Search
----

Useful reference: https://github.com/rmedinahu/cs350lab12/blob/master/README.md

Add a search form to the property app that allows a user to query the **description** attribute of all property listings. Form should return all properties that contain at least one occurrence of the query in the description.


### 1. Add a view to properties/views.py to display the search form and handle form submissions. It will do double duty. See geoquery/views.py (https://github.com/rmedinahu/cs350lab12/blob/master/geoquery/views.py) for example used in lab. Your view should inherit from generic.FormView

a. The form handling will need to be implemented in get_context_data for your view. It is in this override that you can fetch the url query parameters.

b. Your html form (in your template) needs to use the `GET` method rather than the `POST` method.

c. Performing the search requires you to loop over all Property objects to determine which ones have a match with the query.

d. Make sure to return those property objects that match as template variable. 

### 2. Add new file - properties/forms.py and write a new form class to display the query form with your view. Add this class to the form_class attribute located in the view you created in step 1.

### 3. Add new template file to properties to display the view created in step 1.
a. Display information for each matching property object in the template as a list of "matching properties". For each matching listing in the template include a link to the detail view for that property object. E.g., use the `{% url %}` filter with a url `name` and `argument` (the pk of the object)

### 4. Modify properties/urls.py to route your new view and test.

TODO: properties App Search by Geolocation
----

Add a search form to the property app that allows a user to query those properties that are within range of a user inputted address and user inputted number of miles. For example, retrieve all properties that are within 200 miles of 1314 chavez st., las vegs, nm.

Useful reference: https://github.com/rmedinahu/cs350lab12/blob/master/README.md

* Please study Lab 12 to understand how to use Geopy to compute distance between two Location objects.

### 5. As in the previous search component, create view for displaying and handling a form for collecting an address AND number of miles (or range). The view should determine which properties are within range of ADDRESS by indicated MILES.

a. Same setup as the previous search component.

### 6. Add a new form class to your properties/forms.py but this one should display two fields: a location field (CharField) AND an IntegerField to capture miles. Add this class to the form_class attribute located in the view you created in step 5.

### 7. You can use the same template created in step 3 above as long as your view (step 5) creates the same template variable used in the previous search component.

### 8. Modify properties/urls.py to route your new view and test.

### 9. Add a link to the home page (e.g., http://localhost:8000) for each search view created above.

### 10. Add two unit tests to properties/tests.py. The tests should test the two views you created above. The key test is to count the number of properties stored in the context variable that stores the results of each query. See the following example in the lab12 repository for a guide. Note that you will have to construct a query parameter string relevant to your forms.

https://github.com/rmedinahu/cs350lab12/blob/master/geoquery/tests.py

## Done.


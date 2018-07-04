# Zillow Real Estate Search - Android app

Provides an Android Activity (page) to take Address, City, and State as input. The Address and City fields are text boxes, while the
“State” field is a dropdown menu. When the “Search” button is tapped, error checking is done, and on valid input, the JSON result
from the PHP file located on your AWS server is returned. On all valid input, another activity should show the results page, which
is a tabbed interface.Pressing the “Back” button of android should take you to the first user interface, to take the next query.
There should be a button at the top-right of the “Basic Info” tab which is a Facebook share button . Clicking on it will allow one
to post the property details on Facebook.

Search for real estate in a native android app

  - Service in PHP - validates user input and retrieves data from [Zillow API](http://www.zillow.com/howto/api/APIOverview.htm)
  - The reponse is sent back to the user in JSON format
  - Application UI uses Android actvities to display relevant content
  - The search results can be shared by the user on their Facebook page via the Facebook app
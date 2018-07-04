I got frustrated using the "Great Real Estate" plugin (http://www.rogertheriault.com/agents/plugins/great-real-estate-plugin/) because of it's lack of flexibility. I'm a real estate photographer doing virtual tours and GRE didn't have a place for me to add my vt-links to my client's site. I liked GRE ok otherwise, so I recreated most of the functionality with Pods.

The listings index isn't changed much from GRE, but I re-built the detail pages. I'm making use of NextGen Gallery and Simple Google Maps plugins.

A couple of things that are still a bit over my head that I'd like to implement:

1. Use a drop-down menu to pick the appropriate NextGen Gallery based on Gallery name.
2. Filters. I'd like to let the visitors sort on list_price and maybe bedrooms. Depends on how many listings this client ends up with. It may be a moot point if they have 20 or less at any one time.

I'm running three different Pods loops based on status (For Sale or Rent, Pending Sale or Lease, and Sold or Rented).

I'm sure the code could be cleaned up by using some functions, but I'm still learning and don't have that technique mastered yet. I decided to release it as-is since it worked.

Also Needed (if used as-is):

NextGen Gallery Plugin
http://alexrabe.de/?page_id=80

Simple Google Map Plugin
http://clarknikdelpowell.com/wordpress/simple-google-map/

I had the contents of the listings_style.css at the bottom of my theme's style.css

The functions in listings_functions.php are straight from the GRE Plugin and were placed in my functions.php file.

The other .php files are just copies of the pods packages (or should be).  I was using them in my text editor and copy-pasting over to the pods interface in wordpress as a workflow.

The clear_date input helper and select_from_table input helper are straight from the Podscms.org packages page.

I think that's about it!  

Brett Weaver
http://spotlightvt.com
brett@spotlightvt.com
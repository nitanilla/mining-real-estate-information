
Tools for investigating local election and finance data in Monroe County, NY
============================================================================

Searching the monroe taxes database is prolly not a good idea.
Querying the geo db might be better:
    http://geo.cityofrochester.gov/defmenu.asp?qrytype=ownername

But some residential buildings are owned by LLCs.  PITA!  Luckily, LLCs have to
register and can be searched here:
    http://www.dos.ny.gov/corps/bus_entity_search.html

So if we build three tables:

    - donors
    - owners of real estate
    - owners of businesses

Then we can collapse the third into the first two; meaning, rewrite the first
two with knowledge of the third.  Then, look for simple corrolations between the
first two rewritten sets.

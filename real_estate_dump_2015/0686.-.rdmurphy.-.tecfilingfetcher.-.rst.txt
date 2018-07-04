TEC Filing Fetcher
==================

Fetching TEC filing data made easy! Plug in a TEC filing ID, get back contribution or expenditure data in CSV format.

Installation
------------

::

    pip install tecfilingfetcher

How it works
------------

Pretty straightforward:

::

    usage: fetchfiling [-h] [-t {contributions,expenditures}] [-s]
                       filing_id [filing_id ...]

    positional arguments:
      filing_id             The TEC filing ID(s) to fetch

    optional arguments:
      -h, --help            show this help message and exit
      -t {contributions,expenditures}, --type {contributions,expenditures}
                            The type of data you want to get
      -s, --simple          Returns only basic fields, good if you only want
                            numbers

Examples
--------

::

    $ fetchfiling -s -t contributions 580604  # Texans for Rick Perry's July 2013 Semiannual

    ..

    Unique ID,Entity Code,Last/Organization Name,First Name(s),Title,Suffix,Street Address 1,Street Address 2,City,State,ZIP Code,Date,Amount/In-kind Value,Description,Employer,Principal Occupation/Job Title,Travel Outside Texas (If In-kind)
    2,IND,London,Stacy,,,,,Houston,TX,77024,20130617,400.00,,Self,Real Estate,
    1,IND,Cantwell,Michael,,,,,Leander,TX,78641,20130617,100.00,,,,
    28,IND,Anwar,S. Javaid,Mr. and Mrs.,,,,Midland,TX,79705,20130620,16250.00,(See travel info),Midland Energy,Owner/President,X
    2,,,,,,,,,,,,,,,,X
    3,,,,,,,,,,,,,,,,X
    4,,,,,,,,,,,,,,,,X
    3,IND,Jones,Dale,,,,,Coppell,TX,75019,20130624,500.00,,Best Efforts,Best Efforts,
    4,IND,Holmes,William,,,,,El Paso,TX,79912,20130624,1000.00,,Best Efforts,Best Efforts,
    5,IND,Musil,Stephen,,,,,Cedar Park,TX,78613,20130624,25.00,,,,
    6,IND,Vazquez,Laura,,,,,El Paso,TX,79936,20130624,25.00,,,,
    7,IND,Lott,Thomas,Mr.,,,,Fulshear,TX,77441,20130624,100.00,,Andarko Petroleum,Geologist,
    8,IND,Brunone,Dominick,,,,,The Hills,TX,78738,20130624,25.00,,,,
    9,IND,Ciaccio,Michael,,,,,Sugar Land,TX,77496,20130624,10.00,,,,
    10,IND,DiLorenzo,Mary,Ms.,,,,Bethpage,NY,11714,20130624,100.00,,Suffolk County National Bank,VP Financial Reporting Manager,
    11,IND,Higginbotham,Lou,Ms.,,,,Dallas,TX,75205,20130624,500.00,,Retired,Retired,
    12,IND,Baker,James,,,,,San Marcos,TX,78666,20130624,25.00,,Self,Real Estate,
    15,IND,Holdren,David,Mr.,,,,San Angelo,TX,76903,20130625,10.00,,Retired,Retired,
    14,IND,Pappas,Peter,,,,,Rockbridge,MO,65741,20130625,25.00,,Best Efforts,Best Efforts,
    16,IND,Eskridge,Robert,,,,,Round Rock,TX,78681,20130625,100.00,,,,

The filing fetcher outputs to stdout – if you need to save it, direct it into a file.

::

    fetchfiling -s -t contributions 580604 > texans_for_rick_perry_july13.csv

You can now fetch multiple reports in one swoop by passing in space-separated filing IDs. You should probably only do this if you are **fetching multiple reports for the same filer**. The reports themselves do not identify which row belongs to which filer, so make sure all of your IDs refer to the same one!

::

    $ fetchfiling -s -t contributions 580604 599270  # Texans for Rick Perry's July 2013 Semiannual + January 2014 Semiannual

But wait... where do I get those IDs?
-------------------------------------

The `Texas Ethics Commission <http://www.ethics.state.tx.us/index.html>`_, via the `campaign finance search form <http://www.ethics.state.tx.us/dfs/search_CF.htm>`_. For example, you can find Texans for Rick Perry filing IDs on `this page <http://www.ethics.state.tx.us/php/filer.php?acct=00015741>`_.

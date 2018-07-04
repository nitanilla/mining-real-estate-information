django-brokerage   
====================
:author: Colin Powell
:date: 2011-04-29
:by: One Cardinal Web Development
:license: GPLv3

Brokerage is a Django application designed to handle basic needs of a real estate broker's website. It is by no means a complete package for a fully-functioning website, but is instead intended to add the ability to manage listings, agents and the details of a brokerage office (or multiple brokerage offices if needed).

Models
--------
Attribute from django-attributes
Gallery, Photo from django-photologue

PropertyType
  - title
  - slug
  - description

Property
  - title
  - slug
  - description
  - price
  - addressfield
  - galleries (photologue)
  - photos (photologue)

PropertyAttribute (Attribute)

PropertyAmenity (Attribute)
  
URLs
-------

    URL                           Named view
    ----                          -----------
    /                          -> bk_index
    /properties                -> bk_property_list
    /properties/<type>/        -> bk_propertytype_list
    /properties/<type>/<slug>/ -> bk_property_detail
    /agents/                   -> bk_agent_list
    /agents/<slug>/            -> bk_agent_detail


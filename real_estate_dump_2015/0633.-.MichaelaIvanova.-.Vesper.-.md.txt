# Vesper
Team Vesper Telerik Academy

Vesper's free ads - like olx:

1. Use jQuery
2. Objects:
   - module User properties:
             1. alias
             2. name
             3. list of posted ads (array)
   - module: abstract class Ad properties:
             1. title
             2. category
             3. info
             4. img
             5. date
             6. price
             7. posted by user
             8. location
             9. contact (phone number)

    - module:class Real Estate - inherits Ad, properties:
                  1. city
                  2. address
                  3. type (for sell or rental)

     CATEGORIES:
    - module:abstract class Device - inherits Ad properties:
                1. model
                2. manufacturer
                3. condition (new or used)

    - module : class Computers - inherits Device properties:
                1.display
                2.specifications
    - module : class Mobile - inherits Device properties:
                1. display
                2. weight
    - module : class Audio - inherits Device properties:
                1. battery


    - module : abstract class Vehicle - inherits Ads properties:
                1. model
                2. year
    - module : class Car - inherits Vehicle:
                1. type

    - module : class Motorcycle inherits Vehicle:
               1. engine
    - module : class Boat inherits Vehicle
               1. size
    ///////////////////////////////////////////////////////

         WE ARE USING PARSE
    //////////////////////////////////////////////////////
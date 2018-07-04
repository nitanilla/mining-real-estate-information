Priority Places
============

*Note: This project uses deprecated GeoTrellis 0.9*

This project created a web-based prioritization map to facilitate business siting and real estate development for the city of Ashville, North Carolina.

The tool enables users to select and assign weights to criteria that they consider important, such as proximity to infrastructure and amenities like interstate ramps, economic incentives like low tax value areas needing investment or demographic factors like density of adults with a college degree. Users also have the option of using a mask to limit their analysis to particular areas, such as Industrial Zoning or Tax Incentives. With the click of a button, Priority Places integrates this information to generate a heat map highlighting those locations that best meet a user’s specified needs.



To run, clone this repository, change to current working directory to the 'geotrellis' subfolder, and type 

```console
./sbt run
```

This will start the application which can be reached at http://localhost:8080/ 

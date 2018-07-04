# BC Stats / BCIC Housing Data Visualization

This app is a solution for BC Government Data Visualization Challenge to provide 
improved data visualization capacity and usefullness of Crown data with regards 
to the housing market and condiotions in BC.

App is currently publicly available at https://bcdevx.rubyind.com/.

## Table of Contents

  * [ BC Stats / BCIC Housing Data Visualization](#bc-stats-bcic-housing-data-visualization)
      * [About the app](#about-the-app)
          * [About Ruby Industries Inc](#about-ruby-industries-inc.)
      * [Installation Instructions](#installation-instructions)
          * [System Requirements](#system-requirements)
          * [Installation](#installation)
      * [Data Sources](#data-sources)
          * [Census Canada](#census-canada)
          * [Property Transfer Tax](#property-transfer-tax)
      * [Credits](#credits)

## About the app
The Province of British Columbia and other agencies collect a wealth of administrative data that relates 
to housing, including the market for housing, as a consequence of their regulatory and administrative authorities.
 
The British Columbia Government wanted to develop statistics that will provide greater certainty 
about the state of housing in the province, including the role of foreign ownership, 
real estate as an investment or business strategy (rather than home ownership), 
and insights into the regional impact of these issues. 
For more information see https://github.com/bcgov/housing-data-visualization-project.

This application is the result of the *Data Visualization Challenge*,
launched by the [BC Innovation Council](http://www.bcic.com)
in partnership with [BC Stats](https://www2.gov.bc.ca/gov/content/data/about-data-management/bc-stats)
in December 2016.

The challenge aimed to develop a tool to visualize BC housing data in a more meaningful and impactful way.
BCIC and BCStats invited innovators around the province to submit their proposed solutions to the challenge.
A review panel comprised of the BC Innovation Council, BC Developers’ Exchange and BC Stats 
selected the five finalists who have been selected to present their prototypes at the 
2017 [BCTech Summit](https://bctechsummit.ca/), the largest tech event in BC and a joint initiative between 
the Province and BC Innovation Council. 
[Ruby Industries Inc.](https://rubyind.com) was announced as 
the winner of the Challenge and got the opportunity to continue working on the project and develop the solution.

Ruby Industries combined a variety of data visualization approaches in a way that makes 
significant improvements to the accessibility and readability of BC Stats’ housing data.
It provides BC Stats with an innovative tool
for better use of their data and, and at the same time, offers interested BC residents, government agencies,
and non-profits the opportunity to interact with, understand and make decisions based on community growth
and housing data. The platform is currently in its beta-version, users are invited to provide
[feedback](http://bcic.com)
on their use of this iteration including ideas as to how it could be advanced
to further fulfill its role.

### About Ruby Industries Inc.
[Ruby Industries Inc.](https://rubyind.com/) is Kelowna-based [Data Science and Data Visualization consulting](https://rubyind.com/) firm.
They provide engaging interactive data visualization solutions across wide range of industries.
The company also features a number of Machine Learning APIs in marketing analytics domains. These include customer segmentation
and prediction of customer lifetime value and customer churn.

## Installation instructions

### System Requirements
Local installation requires R statistical software to be installed.
Following is the R session info with required packages (on Linux server).

```
> sessionInfo()
R version 3.4.3 (2017-11-30)
Platform: x86_64-pc-linux-gnu (64-bit)
Running under: Debian GNU/Linux buster/sid

Matrix products: default
BLAS: /usr/lib/x86_64-linux-gnu/blas/libblas.so.3.7.1
LAPACK: /usr/lib/x86_64-linux-gnu/lapack/liblapack.so.3.7.1

locale:
 [1] LC_CTYPE=en_US.UTF-8       LC_NUMERIC=C              
 [3] LC_TIME=en_US.UTF-8        LC_COLLATE=en_US.UTF-8    
 [5] LC_MONETARY=en_US.UTF-8    LC_MESSAGES=en_US.UTF-8   
 [7] LC_PAPER=en_US.UTF-8       LC_NAME=C                 
 [9] LC_ADDRESS=C               LC_TELEPHONE=C            
[11] LC_MEASUREMENT=en_US.UTF-8 LC_IDENTIFICATION=C       

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
 [1] bindrcpp_0.2          shinyBS_0.61          shinycssloaders_0.2.0
 [4] treemap_2.4-2         sunburstR_1.0.2       plotly_4.7.1         
 [7] ggplot2_2.2.1         tidyr_0.7.2           DT_0.2               
[10] htmlwidgets_0.9       dplyr_0.7.4           lubridate_1.7.1      
[13] magrittr_1.5          stringr_1.2.0         readr_1.1.1          
[16] leaflet_1.1.0         sf_0.6-0              shinyjs_0.9.1        
[19] here_0.1              shiny_1.0.5          

loaded via a namespace (and not attached):
 [1] purrr_0.2.4         colorspace_1.3-2    miniUI_0.1.1       
 [4] htmltools_0.3.6     viridisLite_0.2.0   rlang_0.1.6        
 [7] e1071_1.6-8         pillar_1.1.0        glue_1.2.0         
[10] DBI_0.7             RColorBrewer_1.1-2  bindr_0.1          
[13] plyr_1.8.4          munsell_0.4.3       gtable_0.2.0       
[16] httpuv_1.3.5        crosstalk_1.0.0     class_7.3-14       
[19] Rcpp_0.12.13        xtable_1.8-2        udunits2_0.13      
[22] backports_1.1.1     scales_0.5.0        classInt_0.1-24    
[25] jsonlite_1.5        mime_0.5            hms_0.4.0          
[28] digest_0.6.14       stringi_1.1.5       grid_3.4.3         
[31] rprojroot_1.2       tools_3.4.3         lazyeval_0.2.1     
[34] tibble_1.3.4        pkgconfig_2.0.1     gridBase_0.4-7     
[37] data.table_1.10.4-3 assertthat_0.2.0    httr_1.3.1         
[40] R6_2.2.2            units_0.5-1         igraph_1.1.2       
[43] compiler_3.4.3     
```

### Installation
In terminal, type the following:
```
shiny::runGitHub("housing-data-challenge-ruby", "bcgov")
```
This will download the app localy in your current working directory and run the app.

## Data Sources

BC Housing Data Visualization Platform uses the following datasets:
- Census Canada (years 2016, 2011 and 2006).
- Property Transfer Tax (2017 and 2016).

### Census Canada
Census data is provided by [Statistics Canada](http://www.statcan.gc.ca/)
and obtained through [CensusMapper API](https://censusmapper.ca/api) 
using [cancensus R package](https://github.com/mountainMath/cancensus).
- Statistics Canada. No date. 2006 Census of Canada (Provinces, Census Divisions, Municipalities) (database).
- Statistics Canada. No date. 2011 Census of Canada (Provinces, Census Divisions, Municipalities) (database).
- Statistics Canada. No date. 2016 Census of Canada (Provinces, Census Divisions, Municipalities) (database).

Statistics Canada provides a wealth of detail about the information collected in the Census. Some of the key pages are:

* [Census Program homepage](http://www12.statcan.gc.ca/census-recensement/index-eng.cfm)

* [Data products, 2016 Census](http://www12.statcan.gc.ca/census-recensement/2016/dp-pd/index-eng.cfm)

   - [Data tables, 2016 Census](http://www12.statcan.gc.ca/census-recensement/2016/dp-pd/dt-td/index-eng.cfm), grouped by topic, variable, and map 
   
   - [Reference materials, 2016 Census](http://www12.statcan.gc.ca/census-recensement/2016/ref/index-eng.cfm): concepts and definitions, reference guides and other materials
   
   - [Reference materials, 2016 Census: Housing](http://www12.statcan.gc.ca/census-recensement/2016/ref/98-501/98-501-x2016007-eng.cfm)



### Property Transfer Tax
Property transfer tax data relates to market transactions within the province.

It is provided by Province of British Columbia Ministry of Finance, 
licensed under [Open Government LicenCe - British Columbia](http://www.data.gov.bc.ca/local/dbc/docs/license/OGL-vbc2.0.pdf).

The data is available for download at [B.C. Data Catalogue administered by DataBC](https://catalogue.data.gov.bc.ca/organization/property-taxation).

## Credits

The platform is developed using [R statistical software](https://www.r-project.org/), and realized as R [Shiny™](http://shiny.rstudio.com/) app 
with the help of the following open-source R packages:

- [Shiny™](https://github.com/rstudio/shiny) - Interactive web applications with R.
- [Plotly](https://github.com/ropensci/plotly) - R implementation of plotly.js interactive graphing library. 
- [Readr](https://github.com/tidyverse/readr) - Read flat files (csv, tsv, fwf) into R.
- [Stringr](https://github.com/tidyverse/stringr) - String manipulation in R.
- [Magrittr](https://github.com/tidyverse/magrittr) - Improve the readability of R code with the pipe operator.
- [Lubridate](https://github.com/tidyverse/lubridate) - Working with dates in R.
- [Tidyr](https://github.com/tidyverse/tidyr) - Tidy data with spread and gather functions.
- [Dplyr](https://github.com/tidyverse/dplyr) - A grammar of data manipulation.
- [Cancensus](https://github.com/mountainMath/cancensus) - R wrapper for calling [CensusMapper APIs](https://censusmapper.ca/api).
- [Leaflet](https://github.com/rstudio/leaflet/) - R Interface to leaflet.js maps.
- [RGDAL](https://r-forge.r-project.org/projects/rgdal/) - R bindings to Geospatial Data Abstraction Library.
- [Rgeos](https://r-forge.r-project.org/projects/rgeos/) - Tools for interfacing the C++ translation of the Java Topology Suite.
- [Sf](https://r-spatial.github.io/sf/) - Simple Features for R.
- [rmapshaper](https://github.com/ateucher/rmapshaper) - An R wrapper for the mapshaper javascript library.
- [Htmlwidgets](https://github.com/ramnathv/htmlwidgets) - HTML Widgets for R.
- [DT](https://github.com/rstudio/DT) - R Interface to the jQuery Plug-in DataTables.
- [SunburstR](https://github.com/timelyportfolio/sunburstR) - R htmlwidget for sequence sunburst charts.
- [Treemap](https://github.com/mtennekes/treemap) - R package for treemap visualisation.
- [ShinyJS](https://github.com/daattali/shinyjs) - Improve the user experience of your Shiny™ apps.
- [Shinycssloaders](https://github.com/andrewsali/shinycssloaders) - CSS loader animations for Shiny™ outputs.
- [ShinyBS](https://github.com/ebailey78/shinyBS) - Twitter Bootstrap Components for Shiny™.


# soothsay
Searching for a home or apartment in the NYC real estate market is cruel, daunting and pricey. Soothsay is an attempt to help narrow your search by locating neighborhoods with the best appreciation potential. It seeks to identify neighborhoods on the cusp of gentrification, buy low / sell high. To find these neighborhoods, I used approximately 9 years of real estate data, Google search term volume and mentions in the NY Times Real Estate section, aggregated into monthly buckets.

I used vector autoregression (VAR) to model my three time series: median price, google trends and nytimes mentions. The results of the predictions were used to color a D3 choropleth map of every neighborhood in New York City. 

Happy house hunting!


<!-- README.md is generated from README.Rmd. Please edit that file -->
RealEstateR <img src="man/figures/realestater_logo.png" align="right" width="140" />
------------------------------------------------------------------------------------

[![Travis build status](https://travis-ci.org/estebanangelm/RealEstateR.svg?branch=master)](https://travis-ci.org/estebanangelm/RealEstateR)[![Coverage status](https://codecov.io/gh/estebanangelm/RealEstateR/branch/master/graph/badge.svg)](https://codecov.io/github/estebanangelm/RealEstateR?branch=master)

RealEstateR is a package that analyzes real estate data from the Zillow API.

Installation
------------

You can install the latest development version of RealEstateR using devtools:

``` r
devtools::install_github("estebanangelm/RealEstateR")
```

API Token
---------

To use the Zillow API in this package, you will need to get a Zillow Web Services ID (ZWSID) which can be done by registering [here](http://www.zillow.com/webservice/Registration.htm).

Once you have your ZWSID, you can set it:

``` r
library(RealEstateR)
```

``` r
set_zwsid("your-zwsid-here")
```

This allows you to make API calls within the package without having to pass in your ZWSID every time.

**Note:** If you are contributing to the package and need to run tests locally, add your ZWSID to `.Renviron`. You can do this by running the following command in your RStudio console:

    Sys.setenv(ZWSID='your-key-here')

Usage Examples
--------------

For a more comprehensive overview of all functions, check out the [vignette](https://s3-us-west-2.amazonaws.com/realestater/vignette.html).

To get search results response, use `get_search_results()`:

``` r
response <- get_search_results("2144 Bigelow Ave", "Seattle", "WA")
```

Note that the address must be include a street number. Passing in `"Bigelow Ave"` without the street number will result in an error. `get_search_results()` gives you the raw Zillow API response. You can use this response in other functions to extract information from it.

For example, you can get information about the property's `zpid`:

``` r
get_zpid(response)
#> [1] "48879021"
```

You can also extract the location data (e.g., geocoordinates) from the response:

``` r
get_loc(response)
#> 
#> Status:  Request successfully processed 
#> <Zillow: http://www.zillow.com/webservice/GetSearchResults.htm?zws-id=X1-ZWz1gc6yixcsnf_a57uf&address=2144+Bigelow+Ave&citystatezip=Seattle%2C+WA>
#> 
#> # A tibble: 1 x 6
#>     zip street             city    state latitude longitude
#>   <int> <chr>              <chr>   <chr>    <dbl>     <dbl>
#> 1 98109 2414 Bigelow Ave N SEATTLE WA        47.6     -122.
```

To get information about similar recent sales, use `get_comp_df()`:

``` r
zpid <- get_zpid(response)
get_comp_df(zpid = zpid, count = 5)
#> # A tibble: 5 x 8
#>        zpid bedrooms bathrooms  year  size lot_size    value  rent
#>       <dbl>    <dbl>     <dbl> <dbl> <dbl>    <dbl>    <dbl> <dbl>
#> 1 49127356.       2.      1.10 2002. 1070.    1306.  793432. 2695.
#> 2 48690160.       4.      3.00 1915. 2420.    2613. 1297267. 3939.
#> 3 48689945.       4.      2.00 1912. 2500.    2500. 1111751. 3499.
#> 4 48690000.       2.      1.00 1905. 1730.    3920.  894580. 2500.
#> 5 48690267.       2.      1.50 1911. 1570.    3500.  952394. 3000.
```

This returns a dataframe with information about bedrooms, bathrooms, lot size of properties that are similar to your property.

You can also get price estimates of other properties in the neighbourhood and plot them on a map:

``` r
neighbours <- get_neighbour_zestimates('2144 Bigelow Ave', 'Seattle', 'WA')
plot_neighbour_zestimates(neighbours)
```

<img src="man/figures/neighbour_plot.png" width=55%/>

To get screenname of a real estate agent in a specific city:

    reviews_get_screennames(name = 'Rakesh Ram Real Estate Group', city = 'Cincinnati', state = 'OH')

To get information of up-to 5 real estate agents based on their screennames:

    screennames <- c("Rakesh Ram Real Estate Group", "mwalley0", "pamelarporter", "klamping4", "Cincysrealtor")

    reviews(screennames)

Limitations
-----------

In Zillow's [Terms of Use](https://www.zillow.com/howto/api/APITerms.htm), reverse-engineering like scrapping is not allowed. Thus, it is not possible to get screennames of all real-estate agents in a location through web scrapping method. At the same time, Zillow API allows 1000 requests per day, which also limits the number of agents' reviews information you can get. Reflecting from this limitation, our `reviews` function only allows you to search for reviews information of 5 agents at most.

Contribution
------------

Please note that this project is released with a [Contributor Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project you agree to abide by its terms.

The house icon in the logo is free for commercial use and is taken from [Alex Timashenka](https://www.iconfinder.com/icons/384890/building_home_house_icon#size=128).

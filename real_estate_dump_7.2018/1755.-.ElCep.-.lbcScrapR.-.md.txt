# lbcScrapR
Some R function to Scrape [www.leboncoin.fr](www.leboncoin.fr) French classified website.

## Install
From [here](https://cran.r-project.org/web/packages/githubinstall/vignettes/githubinstall.html), a nice way to install packages from github is to use `devtools` packages. If it's not present in your system, you can install it with :

    install.packages('devtools', dependencies = T)

Once it's done, you've got access to `install_github` functions :

    library(devtools)
    install_github("ElCep/lbcScrapR")

## basic how-To

    library(lbcScrapR)
    ## find your region
    my.region <- region.lbc()[7]
    ## real estate scraping function
    a<-scape_immo(my.region,1, "","Aniane", 5, 5)
    ## extract surfaces from title
    a$surface<-lbc_surf(a)

## Go deeper

    library(lbcScrapR)
    ## find your region
    my.region <- region.lbc()[7]
    ##Price
    my.price <- seq(from=25000, to=200000,by=25000)
    ## real estate scraping function
    a<-scape_immo(my.region,1, "","Aniane", 7, 5)


## Pense-bête
* information about [packaging](http://r-pkgs.had.co.nz/description.html)

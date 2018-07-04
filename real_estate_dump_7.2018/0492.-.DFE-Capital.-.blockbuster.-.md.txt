
[![Build Status](https://travis-ci.com/mammykins/blockbuster.svg?token=sGXpJU3xjdpxsRrMLhKy&branch=master)](https://travis-ci.com/mammykins/blockbuster)
[![codecov.io](http://codecov.io/github/mammykins/blockbuster/coverage.svg?branch=master)](http://codecov.io/github/mammykins/blockbuster?branch=master)
[![GitHub tag](https://img.shields.io/github/tag/mammykins/blockbuster.svg)]()
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/mammykins/blockbuster?branch=master&svg=true)

# DEPRECIATED

This package represents an older version of the Blockbuster model. Code optimisation resulted in a completely rewritten code base so it is appropriate to initiate a new github page. The current version can be found at: (https://github.com/DFE-Capital/Blockbuster-2)

# blockbuster

*This is a prototype package being developed in anticipation of analysing the [Condition Data Collection](https://www.gov.uk/guidance/condition-data-collection-programme-information-and-guidance) and is subject to constant development*

This R package allows you to simulate the deterioration of School buildings through time using a Discrete Time Markov Chain. R packages are an ideal way to package and distribute R code and data for re-use by others.  

The data were collected during the Property Data Survey Programme (PDSP) of 2012-2014. Approximately 2.7 million rows of data were collected. This provides the initial state of the School Estate at timestep zero. The deterioration of the School Estate is then modelled by using deterioration rates associated with each Construction Elements-Sub-element-construction-type. Cost of repairs for these building components are estimated. An investment profile for rebuilding and maintaining the School Estate can also be input to mitigate this entropic spiral. Here we provide an anonymised ten percent sample of School buildings or blocks with identifying features removed. During the development period we have some simulated data available to aid code development, real data may be uploaded later or may be available on request.

|Data inputs|Description|
|---|---|
|building condition|Input data for time zero. A sample simulated from the PDS condition data table.|
|transition matrices|Deterioration rates based on estimates of expected lifetime of a building element-sub-element-construction-type.|
|repair costs|Repair costs of building components from condition grades D-B back to A.|
|rebuild costs|Rebuild cost in pounds per metre squared per unit of gross internal floor area to be rebuilt.|

## Installing the package

The package can be installed with the `devtools` package with `devtools::install_github('mammykins/blockbuster')`.

If you cannot use this function (due to firewalls for instance) you can download the package as a `.zip` file from the main repository page, and run `devtools::install_local('path_to_zip_file')`. You may need to install [Rtools](https://cran.r-project.org/bin/windows/Rtools/) to facilitate this.

## Using the package

### From an R session

Launch an R session as normal and run the following (again setting the arguments as required):

```
library(blockbuster)
```
The beauty of package development is that the business knowledge is enshrined in the package, with the code and documentation in one place. To familiarise yourself after install you can work through the blockbuster vignette which will provide typical uses.  

You can also use the extensive R help which explains the input arguments and output values of all functions by prefixing a function with a *?*.

```
?blockbuster()
```
### Project goal

To simulate the deterioration of the School Estate into the future under various maintenance and rebuilding spending policies. This will provide a data driven approach to improving the management of the [School Estate potenitally saving public money](https://www.nao.org.uk/report/capital-funding-for-schools/). The model's predictions should be evaluated with the next [Condition Data Collection](https://www.gov.uk/guidance/condition-data-collection-programme-information-and-guidance) due in 2017 and beyond. This package will also provide the skills and learnings necessary to extend this package functionality for the CDC data.  

### Improvements

* If you find any bugs raise an issue on the [Github package page](https://github.com/mammykins/blockbuster).
* Any suggestions or improvments to the decision making process within the model would also be welcome.
* Package development is iterative and dependent on user feedback.


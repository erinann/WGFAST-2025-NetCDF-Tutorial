Plotting MVBS in R
================
Erin LaBrecque
2025-04-05

`tidync` was developed and maintained by
[ROpenSci](https://github.com/ropensci/tidync/tree/main)

# Install the package…

from CRAN:

``` r
#install.packages("tidync")
```

or the developmental install from GitHub:

``` r
# install.packages("remotes")
#remotes::install_github("ropensci/tidync", dependencies = TRUE)
```

# Attach packages

The warnings have been muted with `message = FALSE`

``` r
library(tidync)
library(dplyr)
library(ggplot2)
library(lubridate)
```

# Loading the data

The .nc file is in the data folder. First set a path to the data folder
using the `here` package, then load the file using `tidync`.

We are only going to use one function from the `here` package, so we are
not going to attach it to session like we did by calling the other
packages with `library()`. By using the package name and `::` we can
call a function from the package. We are using `here()` instead of
`setwd()` because `here` enables easy file referencing by using the your
top-level directory (folder) to build file paths.

``` r
# path to data folder
dta <- here::here("data")

# load data
mvbs <- tidync(paste0(dta, "/test_MVBS.nc"))

# show data
mvbs
```

    ## 
    ## Data Source (1): test_MVBS.nc ...
    ## 
    ## Grids (4) <dimension family> : <associated variables> 
    ## 
    ## [1]   D2,D1,D0 : Sv    **ACTIVE GRID** ( 419580  values per variable)
    ## [2]   D0       : channel, frequency_nominal
    ## [3]   D1       : ping_time, latitude, longitude
    ## [4]   D2       : depth
    ## 
    ## Dimensions 3 (all active): 
    ##   
    ##   dim   name      length   min   max start count  dmin  dmax unlim coord_dim 
    ##   <chr> <chr>      <dbl> <dbl> <dbl> <int> <int> <dbl> <dbl> <lgl> <lgl>     
    ## 1 D0    channel        3    NA    NA     1     3    NA    NA FALSE TRUE      
    ## 2 D1    ping_time    180     0   895     1   180     0   895 FALSE TRUE      
    ## 3 D2    depth        777     0   388     1   777     0   388 FALSE TRUE

There are three dimensions in the file. Use `hyper_dims` to inspect the
dimensions in more detail.

``` r
hyper_dims(mvbs)
```

    ## # A tibble: 3 × 7
    ##   name      length start count    id unlim coord_dim
    ##   <chr>      <dbl> <int> <int> <int> <lgl> <lgl>    
    ## 1 depth        777     1   777     2 FALSE TRUE     
    ## 2 ping_time    180     1   180     1 FALSE TRUE     
    ## 3 channel        3     1     3     0 FALSE TRUE

<br>

``` r
hyper_vars(mvbs)
```

    ## # A tibble: 1 × 6
    ##      id name  type      ndims natts dim_coord
    ##   <int> <chr> <chr>     <int> <int> <lgl>    
    ## 1     0 Sv    NC_DOUBLE     3     7 FALSE

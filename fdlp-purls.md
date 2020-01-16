fdlp-purls
================

This notebook contains R code to analyze monthly PURL usage statistics
from the Government Publishing Office (GPO).

``` r
# load packages
library(tidyverse)
library(lubridate)
```

``` r
# import and combine monthly usage files
files <- dir(pattern = "purl_referrals_0633")
usage <- files %>%
  map(read_csv) %>%
  reduce(rbind)
```

``` r
# rename and transform variables
colnames(usage) <- c("timestamp", "host", "purl", "target", "sudoc", 
                     "title", "author", "pub_year", "pattern")
usage$timestamp <- ymd_hms(usage$timestamp)
usage$pub_year <- as.integer(usage$pub_year)
```

    ## Warning: NAs introduced by coercion

``` r
usage$host <- as.factor(usage$host)
usage$pattern <- as.factor(usage$pattern)
```

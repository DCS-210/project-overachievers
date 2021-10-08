Project proposal
================
Overachievers

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

## 2. Data

``` r
#install.packages("codebook")
```

``` r
happy2015 <- read_csv("/cloud/project/data/world-happiness/2015.csv")
```

    ## Rows: 158 Columns: 12

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): Country, Region
    ## dbl (10): Happiness Rank, Happiness Score, Standard Error, Economy (GDP per ...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
#happy2016 <- read_csv("/cloud/project/data/world-happiness/2016.csv")
#happy2017 <- read_csv("/cloud/project/data/world-happiness/2017.csv")
#happy2018 <- read_csv("/cloud/project/data/world-happiness/2018.csv")
#happy2019 <- read_csv("/cloud/project/data/world-happiness/2019.csv")
drug <- read_csv("/cloud/project/data/pharmaceutical-drug/pharmaceutical_data_csv.csv")
```

    ## Rows: 1036 Columns: 7

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): LOCATION, FLAG_CODES
    ## dbl (5): TIME, PC_HEALTHXP, PC_GDP, USD_CAP, TOTAL_SPEND

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
glimpse(happy2015)
```

    ## Rows: 158
    ## Columns: 12
    ## $ Country                         <chr> "Switzerland", "Iceland", "Denmark", "…
    ## $ Region                          <chr> "Western Europe", "Western Europe", "W…
    ## $ `Happiness Rank`                <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12,…
    ## $ `Happiness Score`               <dbl> 7.587, 7.561, 7.527, 7.522, 7.427, 7.4…
    ## $ `Standard Error`                <dbl> 0.03411, 0.04884, 0.03328, 0.03880, 0.…
    ## $ `Economy (GDP per Capita)`      <dbl> 1.39651, 1.30232, 1.32548, 1.45900, 1.…
    ## $ Family                          <dbl> 1.34951, 1.40223, 1.36058, 1.33095, 1.…
    ## $ `Health (Life Expectancy)`      <dbl> 0.94143, 0.94784, 0.87464, 0.88521, 0.…
    ## $ Freedom                         <dbl> 0.66557, 0.62877, 0.64938, 0.66973, 0.…
    ## $ `Trust (Government Corruption)` <dbl> 0.41978, 0.14145, 0.48357, 0.36503, 0.…
    ## $ Generosity                      <dbl> 0.29678, 0.43630, 0.34139, 0.34699, 0.…
    ## $ `Dystopia Residual`             <dbl> 2.51738, 2.70201, 2.49204, 2.46531, 2.…

``` r
#glimpse(happy2016)
```

``` r
#glimpse(happy2017)
```

``` r
#glimpse(happy2018)
```

``` r
#glimpse(happy2019)
```

``` r
glimpse(drug)
```

    ## Rows: 1,036
    ## Columns: 7
    ## $ LOCATION    <chr> "AUS", "AUS", "AUS", "AUS", "AUS", "AUS", "AUS", "AUS", "A…
    ## $ TIME        <dbl> 1971, 1972, 1973, 1974, 1975, 1976, 1977, 1978, 1979, 1980…
    ## $ PC_HEALTHXP <dbl> 15.992, 15.091, 15.117, 14.771, 11.849, 10.920, 10.087, 9.…
    ## $ PC_GDP      <dbl> 0.727, 0.686, 0.681, 0.755, 0.682, 0.630, 0.613, 0.591, 0.…
    ## $ USD_CAP     <dbl> 35.720, 36.056, 39.871, 47.559, 47.561, 46.908, 47.649, 50…
    ## $ FLAG_CODES  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
    ## $ TOTAL_SPEND <dbl> 462.11, 475.11, 533.47, 652.65, 660.76, 658.26, 676.23, 72…

## 3. Data analysis plan

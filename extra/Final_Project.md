FinalProject
================
Overachievers

``` r
library(tidyverse)
library(broom)
library(countrycode)
```

``` r
happiness <- read_csv("/cloud/project/data/world-happiness/2015.csv")
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
drug_spending <- read_csv("/cloud/project/data/pharmaceutical-drug/pharmaceutical_data_csv.csv")
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
drug_spending <- drug_spending %>%
  filter(TIME == 2015) %>%
  mutate(Country = countrycode(LOCATION, "iso3c", "country.name")) %>%
  mutate(Continent = countrycode(LOCATION, "iso3c", "continent"))
```

``` r
happiness$Country_title = str_to_title(happiness$Country)

happiness %>%
  mutate(Continent = countrycode(Country_title, "country.name", "continent"))
```

    ## Warning in countrycode_convert(sourcevar = sourcevar, origin = origin, destination = dest, : Some values were not matched unambiguously: Kosovo

    ## # A tibble: 158 × 14
    ##    Country     Region         `Happiness Rank` `Happiness Scor… `Standard Error`
    ##    <chr>       <chr>                     <dbl>            <dbl>            <dbl>
    ##  1 Switzerland Western Europe                1             7.59           0.0341
    ##  2 Iceland     Western Europe                2             7.56           0.0488
    ##  3 Denmark     Western Europe                3             7.53           0.0333
    ##  4 Norway      Western Europe                4             7.52           0.0388
    ##  5 Canada      North America                 5             7.43           0.0355
    ##  6 Finland     Western Europe                6             7.41           0.0314
    ##  7 Netherlands Western Europe                7             7.38           0.0280
    ##  8 Sweden      Western Europe                8             7.36           0.0316
    ##  9 New Zealand Australia and…                9             7.29           0.0337
    ## 10 Australia   Australia and…               10             7.28           0.0408
    ## # … with 148 more rows, and 9 more variables: Economy (GDP per Capita) <dbl>,
    ## #   Family <dbl>, Health (Life Expectancy) <dbl>, Freedom <dbl>,
    ## #   Trust (Government Corruption) <dbl>, Generosity <dbl>,
    ## #   Dystopia Residual <dbl>, Country_title <chr>, Continent <chr>

``` r
combined <- inner_join(happiness, drug_spending, by = "Country")
```

``` r
drug_spending %>%
    ggplot(aes(x = LOCATION, y = TOTAL_SPEND)) +
    geom_jitter() +
    labs(x = "Countries",
         y = "Total spending on pharmaceutical drugs", 
        title = "Total spending on pharmaceutical drugs in 2015 by countries")
```

![](Final_Project_files/figure-gfm/finding-drug-spending-by-country-1.png)<!-- -->

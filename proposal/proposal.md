Project proposal
================
Overachievers

``` r
library(tidyverse)
library(broom)
```

## 1. Introduction

The World Happiness Report dataset was published by Sustainable
Development Solutions Network on Kaggle
(<https://www.kaggle.com/tunguz/pharmaceutical-drug-spending-by-countries>)
. The scores and rankings from this dataset were retrieved from the
Gallup World Poll. The data spans findings from 2013 to 2016 and employs
the Gallup weights to make the estimates representative. The data we are
looking at is a collection of what is defined as the ‘Happiness scores’
which were attributed to a list of countries. The evaluation poll
consisted of several questions which were taken from the Cantril ladder
which rank features of quality of life answers from 10 (being the most
desirable) and 0 (being the least desirable) which makes up the main
variable: “Happiness Score”. These scores were then ranked in order to
create the list of world’s happiest countries. There are also several
other variables that we will be examining within this data set (how
these factors influence happiness scores): Economy (GDP Percent),
Family, Freedom, and Trust (Government). We are interested in seeing how
these variables affect happiness and differences by continent/region.

For our other data set we selected the Pharmaceutical Drug Spending by
Country dataset which was published by Bojan Tunguz on Kaggle. This
dataset was created by merging data from two sources. The variables of
health spending, GDP, and US dollars per capita for each country were
collected from the Organisation for Economic Cooperation and Development
website (<https://data.oecd.org/healthres/pharmaceutical-spending.htm>).
The total spending and population data was retrieved from DataHub
(<http://datahub.io/core/population>). We are interested in seeing
different spending distributions across countries/regions.

We are first generally interested in running summary statistics and
plots on the variables within each respective data set. For our main
analysis we are interested in merging these data sets together to see if
there is a general correlation/relationship between the Pharmaceutical
Spending and World Happiness Rank. Our hypothesis is that countries near
the median for Pharmaceutical Drug Spending will be higher up in the
world happiness rank.

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
dim(happy2015)
```

    ## [1] 158  12

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

``` r
dim(drug)
```

    ## [1] 1036    7

## 3. Data analysis plan

#### The comparison groups you will use, if applicable.

1.  Merge Pharmaceutical Drug Spending and World Happiness Report Data
    Sets together
2.  Find unique country lists for each data set
3.  Remove countries present from one but missing from other (any other
    NA values)
4.  Filter for specific year within Pharmaceutical Drug Spending (2015)
5.  Run summary statistics on each data set (grouping by
    continent/region).
6.  Show distributions of Happiness Scores by continent/region
    -   Faceted Barplot
7.  Show distributions of Pharmaceutical Spending
    -   Faceted Barplot
8.  Correlation between Pharmaceutical Spending and World Happiness
    Ranking
    -   Scatter plot
    -   Density
    -   Look at top 5 and lowest 5 in each category for each data set
        and compare
9.  Other analyses tbd.

#### Comparision Groups Used

-   How different variables affect the happiness score. Impact of
    geographical location on the Happiness score.

#### Very preliminary exploratory data analysis, including some summary statistics and visualizations, along with some explanation on how they help you learn more about your data. (You can add to these later as you work on your project.)

-   See above psuedo-code, will add throughout as well.

#### The statistical method(s) that you believe will be useful in answering your question(s). (You can update these later as you work on your project.)

-   See above psuedo-code, will add throughout as well.

#### What results from these specific statistical methods are needed to support your hypothesized answer?

-   Meaningful differences in distributions across both data sets (by
    continent/country)
-   Significant correlation between Pharmaceutical Spending (near
    median) and World Happiness ranking.

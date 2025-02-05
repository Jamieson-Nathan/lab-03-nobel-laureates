Lab 03 - Nobel laureates
================
Jamieson Nathan
5/2/2025

### Load packages and data

``` r
library(tidyverse) 
```

``` r
nobel <- read_csv("data/nobel.csv")
```

## Exercises

### Exercise 1

``` r
dim(nobel)  # The first element is the number of rows and the second is the number of columns
```

    ## [1] 935  26

``` r
head(nobel) # descriptions of rows
```

    ## # A tibble: 6 × 26
    ##      id firstname    surname  year category affiliation city  country born_date 
    ##   <dbl> <chr>        <chr>   <dbl> <chr>    <chr>       <chr> <chr>   <date>    
    ## 1     1 Wilhelm Con… Röntgen  1901 Physics  Munich Uni… Muni… Germany 1845-03-27
    ## 2     2 Hendrik A.   Lorentz  1902 Physics  Leiden Uni… Leid… Nether… 1853-07-18
    ## 3     3 Pieter       Zeeman   1902 Physics  Amsterdam … Amst… Nether… 1865-05-25
    ## 4     4 Henri        Becque…  1903 Physics  École Poly… Paris France  1852-12-15
    ## 5     5 Pierre       Curie    1903 Physics  École muni… Paris France  1859-05-15
    ## 6     6 Marie        Curie    1903 Physics  <NA>        <NA>  <NA>    1867-11-07
    ## # ℹ 17 more variables: died_date <date>, gender <chr>, born_city <chr>,
    ## #   born_country <chr>, born_country_code <chr>, died_city <chr>,
    ## #   died_country <chr>, died_country_code <chr>, overall_motivation <chr>,
    ## #   share <dbl>, motivation <chr>, born_country_original <chr>,
    ## #   born_city_original <chr>, died_country_original <chr>,
    ## #   died_city_original <chr>, city_original <chr>, country_original <chr>

There appear to be 935 rows and 26 columns. As we can see in the above
tibble, the rows refer to each individual Nobel laureate, and the
columns give specific information like their name, year they won, what
category it was, etc.

### Exercise 2

``` r
library(dplyr)

nobel_living <- nobel %>%
  filter(is.na(died_date), !is.na(country), gender != "org")

nrow(nobel_living)
```

    ## [1] 228

Confirmed that after filtering for currently living, country-available,
and individual (not organisation) lareates, there are 228 remaining
entries.

### Exercise 3

``` r
nobel_living <- nobel_living %>%
  mutate(
    country_us = if_else(country == "USA", "USA", "Other")
  )

nobel_living_science <- nobel_living %>%
  filter(category %in% c("Physics", "Medicine", "Chemistry", "Economics"))

library(ggplot2)

ggplot(nobel_living_science, aes(x = country_us, fill = country_us)) +
  geom_bar() +
  facet_wrap(~ category, scales = "free_y") +
  coord_flip() +
  labs(title = "Nobel Prize Categories by Laureate's Country (USA vs Other)",
       x = "Country",
       y = "Count of Laureates",
       fill = "Country") +
  theme_minimal()
```

![](lab-03_files/figure-gfm/further_limits-1.png)<!-- -->

It appears that the buzzfeed article, remarkably, was accurate and that
most Nobel Prize Laureates were in fact US-based when they won.

### Exercise 4

…

### Exercise 5

…

### Exercise 6

…

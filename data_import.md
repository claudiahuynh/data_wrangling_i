Data Import document
================

This document will show how to import data.

The clean_names function in janitor package cleans the name of the
variables to lower case and replaces space with dash.

``` r
litters_df = read_csv("data/FAS_litters.csv")
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): Group, Litter Number, GD0 weight, GD18 weight
    ## dbl (4): GD of Birth, Pups born alive, Pups dead @ birth, Pups survive
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
```

## Look at data set

``` r
litters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>           <chr>      <chr>             <dbl>           <dbl>
    ##  1 Con7  #85             19.7       34.7                 20               3
    ##  2 Con7  #1/2/95/2       27         42                   19               8
    ##  3 Con7  #5/5/3/83/3-3   26         41.4                 19               6
    ##  4 Con7  #5/4/2/95/2     28.5       44.1                 19               5
    ##  5 Con7  #4/2/95/3-3     <NA>       <NA>                 20               6
    ##  6 Con7  #2/2/95/3-2     <NA>       <NA>                 20               6
    ##  7 Con7  #1/5/3/83/3-3/2 <NA>       <NA>                 20               9
    ##  8 Con8  #3/83/3-3       <NA>       <NA>                 20               9
    ##  9 Con8  #2/95/3         <NA>       <NA>                 20               8
    ## 10 Con8  #3/5/2/2/95     28.5       <NA>                 20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
head(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Con7  #85           19.7       34.7                 20               3
    ## 2 Con7  #1/2/95/2     27         42                   19               8
    ## 3 Con7  #5/5/3/83/3-3 26         41.4                 19               6
    ## 4 Con7  #5/4/2/95/2   28.5       44.1                 19               5
    ## 5 Con7  #4/2/95/3-3   <NA>       <NA>                 20               6
    ## 6 Con7  #2/2/95/3-2   <NA>       <NA>                 20               6
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
tail(litters_df)
```

    ## # A tibble: 6 × 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>         <chr>      <chr>             <dbl>           <dbl>
    ## 1 Low8  #79           25.4       43.8                 19               8
    ## 2 Low8  #100          20         39.2                 20               8
    ## 3 Low8  #4/84         21.8       35.2                 20               4
    ## 4 Low8  #108          25.6       47.5                 20               8
    ## 5 Low8  #99           23.5       39                   20               6
    ## 6 Low8  #110          25.5       42.7                 20               7
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

The view() function will open the entire data frame in a new window.
eval = FALSE so the data set doesn’t show up in the knitted document.

``` r
#view will open the entire data frame in a new window 
#eval = FALSE so the data set doesn't show up in the knitted document
view(litters_df)
```

## Learning Assessment

Importing the FAS_pups dataset.

Use relative path

``` r
pups_df = read_csv("./data/FAS_pups.csv")
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Litter Number, PD ears
    ## dbl (4): Sex, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = janitor::clean_names(pups_df)
```

Use absolute path

``` r
#pups_df = read_csv("/Users/claudiahuynh/Desktop/BIST8105/data_wrangling_i/data")
```

## Look at read_csv options

col_names = FALSE function generates column names as X1, X2, X3 skip = 1
skips the first row which was the original col names

``` r
litters_df = 
  read_csv(
    file = "data/FAS_litters.csv",
    col_names = FALSE,
    skip = 1
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (4): X1, X2, X3, X4
    ## dbl (4): X5, X6, X7, X8
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

What about missing data? Use the na = c() function to treat missing data
presented in the forms of Na, space or . as NA.

``` r
litters_df = 
  read_csv(
    file = "data/FAS_litters.csv",
    na = c("NA", "", "."),
  )
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

What if we code “group” as a factor variable? Factor variables are
useful when we know that the column has different levels. This section
does column parsing using the col_types = col() function.

``` r
litters_df = 
    read_csv(
      file = "data/FAS_litters.csv",
      col_types = cols(
        Group = col_factor()
      )
    )
```

## Import an excel file

Import MLB 2011 summary data. Load the library readxl first

The sheet = “” function allows you to specify which sheets to
import/read. The range = function specifies the cell range like B1:C12
to import/read.

``` r
mlb_df = read_excel("data/mlb11.xlsx", sheet = "mlb11")
```

## Import SAS data

Import SAS data. Load the library haven first

``` r
pulse_df = read_sas("data/public_pulse_data.sas7bdat")
```

\#Never use read.csv Read.csv will not read the data right. Read_csv
treats the data as a tibble instead of a dataframe. It will prevent you
from using shorthands that seem to work but may break the code such as
litters_df\$L. For example:

``` r
litters_df = read.csv("data/FAS_litters.csv")

#litters_df$L example. $ is a shorthand that pulls a variable out of the dataset. 
```

# R Package Data
This document outlines the [**Package Data** Page from R Packages by Hadley Wickham](http://r-pkgs.had.co.nz/data.html).

It's often useful to include data in a package. There are three main ways to include data in your package, depending on what you want to do with it and who should be able to use it:
* If you want to store binary data and make it available to the user, put it in `data/`. This is the best place to put example datasets.
* If you want to store parsed data, but not make it available to the user, put it in `R/sysdata.rda`. This is the best place to put data that your functions need.
* If you want to store raw data, put it in `inst/extdata`.



# Exported Data
The most common location for package data is `data/`. Each file in this directory should be a `.RData` file, created by `save()`, and containing a single object (with the same name as the file). The easiest way to adhere to these rules is to use `devtools::use_data()`:
```r
x <- sample(1000)
devtools::use_data(x, mtcars)
```

If the `DESCRIPTION` file contains `LazyData: true`, then datasets will be "lazily" loaded. This means that they won't occupy any memory until you use them. It is recommended that you always use `LazyData: true` in your `DESCRIPTION`. `devtools::create()` does this for you. 

Often, data you include in `data/` is a cleaned-up versions of raw data you've gathered from somewhere else. It is recommended that you include the code used to do this in the source version of your package, as this will make it easy for you to update or reproduce your version of the data. It is suggested that you put this code in `data-raw/`. You don't need this code in the bundled version of the package, so also add it to `.Rbuildignore`. You can accomplish all of this in one step with `devtools::use_data_raw()`.

## Documenting datasets
Documenting a dataset is similar to documenting a function, but with a few minor differences. Instead of documenting the data directly, you document the name of the dataset and save it in `R/`. For example, the roxygen2 block used to document the diamonds data in ggplot2 is saved as `R/data.R` and looks something like this:
```
#' Prices of 50,000 round cut diamonds.
#'
#' A dataset containing the prices and other attributes of almost 54,000
#' diamonds.
#'
#' @format A data frame with 53940 rows and 10 variables:
#' \describe{
#'   \item{price}{price, in US dollars}
#'   \item{carat}{weight of the diamond, in carats}
#'   ...
#' }
#' @source \url{http://www.diamondse.info/}
"diamonds"
```
There are two additional tags that are important for documenting datasets:
* `@format` gives an overview of the dataset. For data frames, you should include a definition list that describes each variable. It's usually a good idea to describe variables' units here.
* `@source` provides details of where you got the data, often a `\url{}`.

**Never** `@export` a dataset. 



# Internal data
Sometimes functions need pre-computed data tables. If these are put in `data/`, they'll also be available to package users, which is not appropriate. Instead, you can save them in `R/sysdata.rda`. You can use `devtools::use_data()` to create this file with the argument `internal = TRUE`:
```r
x <- sample(1000)
devtools::use_data(x, mtcars, internal = TRUE)
```
Again, to make this data reproducible, it's a good idea to include the code used to generate it in the `data-raw/` directory. 



# Raw data
If you want to show examples of loading/parsing raw data, put the original files in `inst/extdata`. When the package is installed, all files (and directories) in `inst/` are moved up one level to the top-level directory (so they can't have names like `R/` or `DESCRIPTION`). To refer to files in `inst/extdata`, use `system.file()`. 



# Other data
### Data for tests
It's OK to put small files directly into your test directory. But remember that unit tests are testing for correctness, not performance, so keep the size small.

### Data for vignettes
If you want to show how to work with an already-loaded dataset, put that data in `data/`. If you want to show how to load raw data, put that data in `inst/extdata`. 

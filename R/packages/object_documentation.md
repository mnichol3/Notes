# R Object Documentation
This document outlines the [**Object Documentation** Page from R Packages by Hadley Wickham](http://r-pkgs.had.co.nz/man.html).

Documentation is one of the most important aspects of a good package. Without it, users won’t know how to use your package. Documentation is also useful for future-you (so you remember what your functions were supposed to do), and for developers extending your package.



# Documentation Workflow
There are four basic steps:
1. Add roxygen comments to your `.R` files.
2. Run `devtools::document()` (or press `CTRL + Shift + D` in RStudio) to convert roxygen comments to `.Rd` files. (`devtools::document()` calls `roxygen2::roxygenise()` to do the heavy lifting).
3. Preview the documentation with `?`.
4. Rinse and repeat until you're happy with the way the documentation looks. 

## Roxygen comments
Adding roxygen comments to your source file is the first step in the documentation workflow. Roxygen comments start with `#'` to distinguish them from regular comments. All the roxygen lines preceding a function are called a **block**. Each line should be wrapped in the same manner as your code, normally at 80 characters. 

Blocks are broken into **tags**, which follow the format: `@tagName details`. The content of a tag extends from the end of the tag name to the start of the next tag (or the end of the block). Because `@` has a specieal meaning in roxygen, you need to use `@@` if you want to add a literal `@` to the documentation (i.e., in an email address or accessing slots of S4 objects).

Each block includes some test before the first tag, called the **introduction**, and is parsed specially:
* The first *sentence* becomes the title of the documentation. That's what you'll see when you look at `help(package = mypackage)` and is shown at the top of each help file. It should fit on one line, be written in sentence case, but not end in a full stop. 
* The second *paragraph* is the description. It comes first in the documentation and should briefly describe what the function does.
* The third and subsequent *paragraphs* go into the details. This is often a long section that is shown after the argument descriptions and should go into detail about how the function works.

Below is an example of what the introduction for `sum()` might look like if it had been written with roxygen:
```r
#' Sum of vector elements.
#' 
#' \code{sum} returns the sum of all the values present in its arguments.
#' 
#' This is a generic function: methods can be defined for it directly or via the
#' \code{\link{Summary}} group generic. For this to work properly, the arguments
#' \code{...} should be unnamed, and dispatch is on the first argument.
sum <- function(..., na.rm = TRUE) {}
```
`\code{}` and `\link{}` are formatting commands that are discussed further in the *formatting* section. 

You can add arbitrary sections to the documentation with the `@section` tag. This is a useful way of breaking a long details section into multiple chunks with useful headings. Sections titles should be in sentence case, must be followed by a colon, and can only be one line long:
```
#' @section Warning:
#' Do not operate heavy machinery within 8 hours of using this function.
```
There are two tags that make it easier for people to navigate between help files:
* `@seealso` allows you to point to other useful resources, either on the web (`\url{http://www.r-project.org}`), in your package (`\code{\link{functioname}}`), or in another package (`\code{\link[packagename]{functioname}}`).
* If you have a family of related functions where every function should link to every other function in the family, use `@family`. The value of `@family` should be plural. 
For `sum()`, these components might look like:
```
#' @family aggregate functions
#' @seealso \code{\link{prod}} for products, \code{\link{cumsum}} for cumulative
#'   sums, and \code{\link{colSums}}/\code{\link{rowSums}} marginal sums over
#'   high-dimensional arrays.
```


## Documenting functions
In addition to the introduction block, most functions have three tags: `@param`, `@examples`, and `@return`. 

* `@param name description` describes the function's parameters, or inputs. The description should provide a succinct summary of the parameter's type (e.g., string, numeric vector, etc.) and, if not obvious from the name, what the parameter does.
  
  The description should start with a capital letter and end with a full stop (aka a period). It can span multiple lines (or even paragraphs) if necessary. **All parameters must be documented**. 
  
* `@examples` provides executable R code showing how to use the function in practice. This is a very importany part of the documentation because many users look at the examples first. Example code must work without errors as it is run automatically as part of the `R CMD` check.

  For the purpose of illustration, it is often helpful to include code that causes an error. `\dontrun{}` allows you to include code in the example that is not run. 
  
* `@return description` describes that output from the function.

An example function with roxygen documentation is below:
```r
#' Sum of vector elements.
#'
#' \code{sum} returns the sum of all the values present in its arguments.
#'
#' This is a generic function: methods can be defined for it directly
#' or via the \code{\link{Summary}} group generic. For this to work properly,
#' the arguments \code{...} should be unnamed, and dispatch is on the
#' first argument.
#'
#' @param ... Numeric, complex, or logical vectors.
#' @param na.rm A logical scalar. Should missing values (including NaN)
#'   be removed?
#' @return If all inputs are integer and logical, then the output
#'   will be an integer. If integer overflow
#'   \url{http://en.wikipedia.org/wiki/Integer_overflow} occurs, the output
#'   will be NA with a warning. Otherwise it will be a length-one numeric or
#'   complex vector.
#'
#'   Zero-length vectors have sum 0 by definition. See
#'   \url{http://en.wikipedia.org/wiki/Empty_sum} for more details.
#' @examples
#' sum(1:10)
#' sum(1:5, 6:10)
#' sum(F, F, F, T, T)
#'
#' sum(.Machine$integer.max, 1L)
#' sum(.Machine$integer.max, 1)
#'
#' \dontrun{
#' sum("a")
#' }
sum <- function(..., na.rm = TRUE) {}
```
Pressing `CTRL + Shift + D` (or running `devtools::document()`) will generate a `man/add.Rd` that looks something like this:
```
% Generated by roxygen2 (4.0.0): do not edit by hand
\name{add}
\alias{add}
\title{Add together two numbers}
\usage{
add(x, y)
}
\arguments{
  \item{x}{A number}

  \item{y}{A number}
}
\value{
The sum of \code{x} and \code{y}
}
\description{
Add together two numbers
}
\examples{
add(1, 1)
add(10, 1)
}
```
When you use `?add`, `help("add")`, or `example("add")`, R looks for an `.Rd` file containing `\alias{"add"}`. It then parses the file, converts it into HTML, and displays it. 


## Documenting multiple functions in the same file
While you are *able* to document multiple function in the same file, it is a practice best used with caution: documenting too many functions in one place leads to confusing documentation. It should only be used when functions have very similar arguments or have complimentary effects (e.g., `open() and `close()` methods). 

The `@rdname` or `@describeIn` tags enable this feature. 

`@describeIn` is designed for the most common cases:
* Documenting methods in a generic.
* Documenting methods in a class.
* Documenting functions with the same (or similar) arguments

It generates a new section, named either "Methods (by class)", "Methods (by generic)", or "Functions". The section contains a bulleted list describing each function. They're labelled so that you know what function or method it's talking about. Here's an example, documenting an imaginary new generic:
```r
#' Foo bar generic
#'
#' @param x Object to foo.
foobar <- function(x) UseMethod("foobar")

#' @describeIn foobar Difference between the mean and the median
foobar.numeric <- function(x) abs(mean(x) - median(x))

#' @describeIn foobar First and last values pasted together in a string.
foobar.character <- function(x) paste0(x[1], "-", x[length(x)])
```

An alternative to `@describeIn` is `@rdname`. It overrides the default file name generated by roxygen and merges documentation for multiple objects into one file. This gives you complete freedom to combine documentation as you see fit. 

There are two ways to use `@rdname`. You can add documentation to an existing function:
```r
#' Basic arithmetic
#'
#' @param x,y numeric vectors.
add <- function(x, y) x + y

#' @rdname add
times <- function(x, y) x * y
```
Or, you can create a dummy documentation file by documenting `NULL` and setting an informative `@name`:
```r
#' Basic arithmetic
#'
#' @param x,y numeric vectors.
#' @name arith
NULL
```
```
## NULL
```
```r
#' @rdname arith
add <- function(x, y) x + y

#' @rdname arith
times <- function(x, y) x * y
```


# Text formatting reference sheet
With roxygen tags, you use `.Rd` syntax to format text. Note that `\` and `%` are special characters in the `.Rd` format. In order to insert a literal `\` or `%`, escape them with a backslash: `\\`, `\%`

### Character formatting
* `\emph{italics}`: *italics*
* `\strong{bold}`: **bold**
* `\code{r_function_call(with = "arguments")}`: `r_function_call(with = "arguments")` (formats inline code)
* `\preformatted{}`: format text as-is, can be used for multi-line code

### Links
To other documentation:
* `\code{\link{function}}`: function in this package
* `\code{\link[MASS]{abbey}}`: function in another package
* `\link[=dest]{name}`: link to dest, but show name
* `\code{\link[MASS:abbey]{name}}`: link to function in another package, but show name
* `\linkS4class{abc}`: link to an S4 class

To the web:
* `\url{http://rstudio.com}`: a url
* `\href{http://rstudio.com}{Rstudio}`: a url with custom link text
* `\email{hadley@@rstudio.com}`: an email address (note the double `@`)

### Lists
* Ordered (numbered) lists:
  ```
  #' \enumerate{
  #'   \item First item
  #'   \item Second item
  #' }
  ```
* Unordered (bulleted) lists:
  ```
  #' \itemize{
  #'   \item First item
  #'   \item Second item
  #' }
  ```
* Definition (named) lists:
  ```
  #' \describe{
  #'   \item{One}{First item}
  #'   \item{Two}{Second item}
  #' }
  ```
  
### Mathematics
You can use standard LaTeX math (with no extensions):
* `\eqn{a + b}`: an inline equation
* `\deqn{a + b}`: a display (block) equation

### Tables
Tables are created with `\tabular{}`. It takes two arguments:
1. Column alignment, specified by letter for each column (`l` = left, `r` = right, `c` = center)
2. Table contents, with columns separated by `\tab` and rows separated by `\cr`. 

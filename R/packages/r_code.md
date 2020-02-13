# R Code
This document outlines the [**R Code** Page from R Packages by Hadley Wickham](http://r-pkgs.had.co.nz/r.html). The style guide referenced here is based on [Google's R style guide](https://google.github.io/styleguide/Rguide.html).

## Organizing functions
Functions should have logical organization. **However**, the two extremes are bad: don't put all functions into one file and don't put each function in its own separate file. (It's OK to put a large function or function that contains a lot of documentation in its own file).

## Code style
Good coding style is like using correct punctuation. You can manage without it, but it sure makes things easier to read. Good style is important because while your code only has one author, it will usually have multiple readers.

### Object names
* Variable and function names should be lowercase
* Use an underscore (`_`) to separate words within a name (reserve `.` for S3 methods)
* Camel case is a legitimate alternative, but be consistent with your style!
* generally, variable names should be nouns and function names should be verbs.
* Strive for names that are concise and meaningful!
```r
# Good
day_one
day_1

# Bad
first_day_of_the_month  # Too long
DayOne                  # Hard to read
dayone                  # Even harder to read
djm1                    # What????
```
* Avoid using names of existing functions and variables
```r
# Bad
T <- FALSE  # T can be shorthand for TRUE
c <- 10
mean <- function(x) sum(x)
```

### Spacing
* Place spaces around infix operators (`=`, `+`, `-`, `<-`, etc.)
  * The same rule applies when using `=` in fucntion calls.
  * The exception to this rule: `:`, `::`, and `:::` don't need spaces around them.
* Always put a space after a comma, but never before.
```r
# Good
average <- mean(feet / 12 + inches, na.rm = TRUE)
x <- 1:10
base::get

# Bad
average <- mean(feet/12+inches,na.rm=TRUE)
x <- 1 : 10
base :: get
```
* Put a space before left parenthesis, except in a function call:
```r
# Good
if (debug) do(x)
plot(x, y)

# Bad
if(debug)do(x)
plot (x, y)
```
* Extra spacing (i.e., more than one space in a row) is OK if it improves alignment of equal signs or assignments (`<-`):
```r
list(
  total = a + b + c
  mean  = (a + b + c) / n
```
* Do not place spaces around code in parenthesis or square brackets (unless there's a comma, in which case see above):
```r
# Good
if (debug) do(x)
diamonds[5, ]

# Bad
if ( debug ) do(x)  # Spaces around debug
diamonds[5,]        # Need a space after the comma
x[1 ,]              # Space goes after the comma, not before
```


### Curly braces
* An opening curly brace should **never** go on its own line and should **always** be followed by a new line
* A closing curly brace should always go on its own line, unless it's followed by an `else`
```r
# -- Good ---

if (y < 0 && debug) {
  message("Y is negative")
}

if (y == 0) {
  log(x)
} else {
  y ^ x
}

# -- Bad --

if (y < 0 && debug)
message("Y is negative")

if (y == 0) {
  log(x)
}
else {
  y ^ x
}
```
* It's ok to leave a very short statement on the same line:
```r
if (y < 0 && debug) message("Y is negative")
```

### Line length
Strive to limit line length to 80 characters per line. This fits confortably on a printed page with a reasonably-sized font.

### Indentation
When indenting code, use **2 spaces**. Never use tabs or mix tabs and spaces. 

### Assignment
Use `<-`, not `=`, for assignment
```r
# Good 
x <- 5

# Bad
x = 5
```

### Commenting
* **Comment your code**.
* Each line of a comment should begin with the comment symbol ans a single space: `# `.
* Comments should explain the *why*, not the *what*
* Use commented lines of `-` and `=` to break up your file into easily-readable chunks:
```r
# Load data ----------------------------

# Plot data ----------------------------
```

### The R landscape
* **Don't use `library()` or `require()`**. These modify the search path, affecting what functions are available from the global environment
  * It's better to use the `DESCRIPTION` file to specify your package's requirements. This also makes sure those packages are installed when your package is installed.
* **Never use `source()`** to load code from a file. `source()` modifies the current environment, inserting the results of executing the code.
  * Instead, rely on `devtools::load_all()`, which automatically sources all files in `R/`.
  * If you're using `source()` to create a dataset, instead switch to `data/` as described in the **datasets** section. 

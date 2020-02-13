# R Package Metadata
This document outlines the [**Package Metadata** Page from R Packages by Hadley Wickham](http://r-pkgs.had.co.nz/description.html)

## `DESCRIPTION` File
The `DESCRIPTION` file stores important metadata about your package. **Every** package must contain a `DESCRIPTION` file, as it's seen as a defining feature of an R package. `devtools::create("mypackage")` automatically creates a bare-bones description file.

A minimal, bare-bones `DESCRIPTION` file will look something like this:
```
Package: mypackage
Title: What The Package Does (one line, title case required)
Version: 0.1
Authors: persion("First", "Last", email = "first.last@example.com", role = c("aut", "cre"))
Description: What the package does (one paragraph)
Depends: R (>= 3.1.0)
License: What license is it under?
LazyData: true
```

`DESCRIPTION` uses a simple file format called the Debian Control Format (DCF). Each line consists of **one** field name and a value, separated by a colon. When values span multiple lines, they need to be indented:
```
Description: The description of a package is usually long,
    spanning multiple lines. The second and subsequent lines
    should be indented, usually with four spaces.
```

## Dependencies
The `DESCRIPTION` file lists the packages that your package needs in order to work. For example, the following indicates that your package needs both `ggvis` and `dplyr` to work:
```
Imports:
  dplyr,
  ggvis
```

Whereas, the lines below indicate that while your package *can* take advantage of `ggvis` and `dplyr`, they're not required to make it work:
```
Suggests:
  dplyr,
  ggvis
```
Both `Imports` and `Suggests` take a comma-separated list of package names. It's recommended that you put one package on each line, keeping them in alphabetical order as this makes them easier to skim and locate specific packages. 

`Imports` and `Suggests` differ in their strength of dependency:
* `Imports`: packages listed here *must* be present for your package to work. Any time your package is installed, these packages will also be installed if they are not already present. 
* `Suggests`: your package can use these packages, but doesn't require them in order to work. You might use suggested packages for example datasets, to run tests, build vignettes, or maybe there's only one function that needs the package. Packages in `Suggests` are **not** automatically installed alongside your package. 

### Versioning
If your package requires a specific version of a package, specify it in parenthesis after the package name:
```
Imports:
  ggvis (>= 0.2)
  dplyr (>= 0.3.0.1)
Suggests:
  MASS (>= 7.3.0)
```
You almost always want to specify a minimum version version rather than an exact version (`MASS (== 7.3.0)`). Since R can't have multiple versions of the same package loaded at the same time, specifying exact dependency versions dramatically increases the chance of conflicting versions. 

### Other dependencies
There are three other fields within the `DESCRIPTION` file that allow you to express more specialized dependencies:
* `Depends`: Despite the name, you should almost always use `Imports` instead of `Depends`. This will be covered more in the *namespaces* section.
* `LinkingTo`: packages listed here rely on C or C++ code in another package. More on this in the *compiled code* section.
* `Enhances`: packages here are "enhanced" by your package. Typically, this means you provide methods for classes defined in another package (a sort of reverse `Suggests`). It's hard to define what that means, so it's generally not recommended. 

## LazyData
`LazyData` makes it easier to access data in your package. Because it's so important, it's included in the minimal description created by `devtools`. More on this in the *external data* section.

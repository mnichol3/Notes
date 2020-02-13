# R Package Structure
This document outlines the [**Package Structure** Page from R Packages by Hadley Wickham](http://r-pkgs.had.co.nz/package.html)

## What is a package?
There are 5 states a package can be in across its lifecycle: source, bundled, binary, installed, and in-memory.

### Source packages
A **source** package is the development version of a package. Essentially, its just a directory that contains components such as the `R/` directory, `DESCRIPTION` file, and so on.

### Bundled packages
A **Bundled** package is a package that has been compressed into a single file. By Linux convention, R package bundles use the extension `.tar.gz`, meaning multiple files have been reduced to a single `.tar` file and compressed using gzip (`.gz`). 

While bundles are not that useful on their own, they are useful intermediaries between the other package states. Bundles can be build with `devtools::build()`.

### Binary packages
**Binary** packages are useful for distributing packages to users that do not have development tools. Like a bundled package, a binary package is a single compressed file. However, when uncompressed, the internal structure is quite different:
* There are no `.R` files in the `R/` directory. Instead, there are three files that store the parsed functions in an efficient file format. 
* A `Meta/` directory contains a number of `.Rds` files that contain cached metadata about the package, like what topics the help files cover and parsed versions of the `DESCRIPTION` files. 
* An `html/` directory contains files needed for HTML help.
* If there was any code in `src/`, there will now be a `libs/` directory that contains the results of compiling 32 bit (`i386/`) and 64 bit (`x64/`) code.

### Installed packages
An **installed** package is just a binary package that has been decompressed into a package library. A **library** is simply a directory that contains installed packages. 

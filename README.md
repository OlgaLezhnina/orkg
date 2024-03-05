
<!-- README.md is generated from README.Rmd. Please edit that file -->

# orkg

<!-- badges: start -->
<!-- badges: end -->

The orkg package provides the R users with a friendly way to interact
with the ORKG API. The user can load ORKG templates, create their
instances, and write JSON-LD files suitable for harvesting into the ORKG
with Python.

## Installation

You can install the development version of orkg from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
library(devtools)
# from the TIB GitLab
devtools::install_gitlab("TIBHannover/orkg/orkg-r")
# or from the maintainer's GitHub
# devtools::install_github("OlgaLezhnina/orkg")
```

## Example

This is a basic example which shows you how to work with an ORKG
template. This is the simplest template created for illustration
purposes. You need to know the hostname (the default is
“<https://incubating.orkg.org/>”). Please use the template ID (in this
example, “R937648”) to work with a template.

``` r
library(orkg)
## see the currently used hostname 
orkg::show_hostname()
#> [1] "https://incubating.orkg.org/"
## if necessary, change it to the hostname you need
orkg::change_hostname("https://incubating.orkg.org/")
#> [1] "https://incubating.orkg.org/"
## load reference classes for a template
tp <- orkg::load_reference_classes("R937648")  
## check which templates are included 
names(tp)
#> [1] "measurement_scale"
## see information about any template you need
tp$measurement_scale
#> Generator for class "measurement_scale_orkg":
#> 
#> Class fields:
#>                                                                   
#> Name:           label  template_name template_class     components
#> Class:      character      character      character           list
#> 
#> Class Methods: 
#>      "initialize", "field", "trace", "getRefClass", "initFields", "copy", 
#>      "callSuper", ".objectPackage", "export", "untrace", "getClass", "show", 
#>      "usingMethods", ".objectParent", "import"
#> 
#> Reference Superclasses: 
#>      "envRefClass"
## see which fields you can use for writing an instance
orkg::show_fields(tp$measurement_scale)
#> [1] "label"
## write your instance using fields of your choice
my_instance <- tp$measurement_scale(label = "my_scale")
## apply this function to write it as a JSON string
my_result <- orkg::to_orkg_jsonld(my_instance)
## write it as a file
## write(my_result, "my_result.json")
## harvest into the ORKG with Python
```

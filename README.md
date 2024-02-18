
# orkg

<!-- badges: start -->
<!-- badges: end -->

This is a replacement of the ORKG-R package. 
The user can load the ORKG templates, create their instances, and write JSON-LD files. 
The resulting JSON-LD files are suitable for harvesting into the ORKG with Python.

## Installation

You can install the development version of orkg from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("OlgaLezhnina/orkg")
```

## Example

This is a basic example which shows you how to work with an ORKG template.
This is the simplest template created for illustration purposes.
You need to know the hostname (the default is "https://incubating.orkg.org/").
Please use the template ID (in this example, "R937648") to work with a template.

``` r
library(orkg)
## see the currently used hostname 
orkg::show_hostname()
## if necessary, change it to the hostname you need
orkg::change_hostname("https://incubating.orkg.org/")
## load reference classes for a template
tp <- orkg::load_reference_classes("R937648")  
## check which templates are included 
names(tp)
## see information about any template you need
tp$measurement_scale
## see which fields you can use for writing an instance
orkg::show_fields(tp$measurement_scale)
## write your instance using fields of your choice
my_instance <- tp$measurement_scale(label = "my_scale")
## apply this function to write it as a JSON string
my_json <- orkg::turn_json_orkg(my_instance)
## write it as a file
write(my_json, "my_json.json")
## harvest into the ORKG with Python
```


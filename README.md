---
title: "VM0047-LULC-Disturbance-Check"
author: "Murphy, S."
date: "2024-10-17"
output:
  html_document:
    keep_md: yes
---



# Environment Setup

For replication purposes, a list of package `requirements` is derived and tallied against the local library loaded on the user's current local environment. Any `missing.packages` are then installed and loaded in the same code. To enable, simply hit the green arrow icon in the top right corner of the code chunk showing in your rstudio to **Run Current Chunk**.


``` r
# derive list of required packages
requirements <- c(
  "ggplot2", "Rcpp", "sits", "pak", "usethis", "sf", "rmarkdown", "devtools", 
  "s2", "gdalcubes", "rsat", "latex2exp", "readxl", "magrittr", "janitor", 
  "dplyr", "RColorBrewer", "psych", "tmap", "useful", "caret", "tibble", 
  "DescTools", "animation", "ModelMetrics", "knitr", "kableExtra", "basemaps", 
  "htmltools", "gtsummary", "data.table")

# derive function to check & load
setup <- function(requirements){
  missing.packages <- requirements[!(requirements %in% installed.packages()[,"Package"])];
    if(length(missing.packages)) {
        install.packages(missing.packages);
    }
    for(package_name in requirements){
        library(package_name,character.only=TRUE,quietly=TRUE);
    }
}

# call function to setup required packages
setup(requirements);
```


# Import AOI

For visualization purposes, the package `tmap` is used throughout this workflow. 
The shapefile of this task's area of interest is loaded as follows.


``` r
tmap::tmap_mode("view")
tmap_options(check.and.fix = T)

aoi = read_sf("./test-polygon/test polygon.shp") 
tm_shape(st_geometry(aoi)) + 
  tm_borders(col="red") +
  tm_scale_bar(position = c("left", "bottom"), width = 0.15) +
  tm_compass(position = c("left", "top"), size = 2)
```

preserve51366f06fcde3f50

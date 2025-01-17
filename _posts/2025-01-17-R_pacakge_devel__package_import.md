---
title: "R Devel 1 : Importing R Packages for Package Development"
output:
  html_document: default
date: "2025-01-17"
---

# 1. `@importFrom` rather than `@import`

When developing a Bioconductor package, it is required to selectively import a function or an object from an existing package that your new package uses.

That is, in roxygen2 documentation, instead of using import,

```{r}
#' @import ComplexHeatmap
```

you should use importFrom as much as possible for non-.
```{r}
#' @importFrom ComplexHeatmap Heatmap RowAnnotation HeatmapAnnotation
```


# 2. Day-to-day code development on interactive environment
But it maybe inefficient when you develop codes, testing them in the interactive mode.
Therefore, I would suggest this practice before you finally write them in the roxygen2 document.

```{r}
Heatmap = ComplexHeatmap::Heatmap
RowAnnotation = ComplexHeatmap::RowAnnotation
HeatmapAnnotation = ComplexHeatmap::HeatmapAnnotation
```

You use it instead of `library(ComplexHeatmap)`. And when you wrap up and translate it into roxygen2 document, it will be much easier.


# 3. Finding which objects and functions are from certain package.

If you haven't using importFrom much, then it will be very laborious to find which function and object to import from which package.

Here is an example code that may help you find them with ease.

```{r}

# required functions
`%>%` = magrittr::`%>%`
str_replace = stringr::str_replace
str_view = stringr::str_view
str_extract_all = stringr::str_extract_all

# list of R script files to check
Rscripts = list.files("newpackage/R/",full.names = TRUE) %>% structure(.,names=basename(.))

# set the package name to find which objects and functions belong to it.
target_package = "ggplot2";library(ggplot2)

# build regular expression that covers all objects
obj_patterns = 
  ls(paste0("package:",target_package)) %>%
  str_replace("[.]","[.]") %>%
  paste(collapse = "|")


# a list of unique objects and functions in the R scripts
Rscripts %>%
  lapply(\(x) str_extract_all(readLines(x),obj_patterns) %>% unlist) %>% unlist %>% unique

### [1] "glue" "trim"

# locate all objects and functions within each file
Rscripts %>%
  lapply(\(x) str_view(readLines(x),obj_patterns))

### $main.R
###  [12] ? #' @rawNamespace import(<glue>, except=c(<trim>))
###  [25] ?         dot_info <- capture_params_<glue>(...)
###  [28] ?             title_txt <- (<glue>("{fun_name} Depth Distribution"))
###  [30] ?             title_txt <- (<glue>("{fun_name} {dot_info} Depth Distribution"))
###  [49] ? capture_params_<glue> <- function(...) {

```


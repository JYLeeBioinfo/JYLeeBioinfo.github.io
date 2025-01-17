---
title: "R Devel 1 : Importing R Packages for Package Development"
output:
  html_document: default
date: "2025-01-17"
---

When developing a Bioconductor package, it is required to selectively import a function or an object from an existing package that your new package uses.

That is, in roxygen2 documentation, instead of using import,

```{r}
#' @import ComplexHeatmap
```

you should use importFrom as much as possible for non-.
```{r}
#' @importFrom ComplexHeatmap Heatmap RowAnnotation HeatmapAnnotation
```



But it maybe inefficient when you develop codes, testing them in the interactive mode.
Therefore, I would suggest this practice before you finally write them in the roxygen2 document.

```{r}
Heatmap = ComplexHeatmap::Heatmap
RowAnnotation = ComplexHeatmap::RowAnnotation
HeatmapAnnotation = ComplexHeatmap::HeatmapAnnotation
```

You use it instead of `library(ComplexHeatmap)`. And when you wrap up and translate it into roxygen2 document, it will be much easier.

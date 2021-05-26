
<!-- README.md is generated from README.Rmd. Please edit that file -->

# kairos

<!-- badges: start -->

[![R-CMD-check](https://github.com/tesselle/kairos/workflows/R-CMD-check/badge.svg)](https://github.com/tesselle/kairos/actions)
[![codecov](https://codecov.io/gh/tesselle/kairos/branch/master/graph/badge.svg)](https://codecov.io/gh/tesselle/kairos)

[![Project Status: WIP – Initial development is in progress, but there
has not yet been a stable, usable release suitable for the
public.](https://www.repostatus.org/badges/latest/wip.svg)](https://www.repostatus.org/#wip)
<!-- badges: end -->

## Overview

A toolkit for absolute dating and analysis of chronological patterns.
This package includes functions for chronological modeling and dating of
archaeological assemblages from count data.

**Initial development is in progress.**

## Installation

You can install the released version of **kairos** from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("kairos")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("remotes")
remotes::install_github("tesselle/kairos")
```

## Usage

``` r
## Load packages
library(kairos)

library(folio) # Datasets
library(ggplot2)
library(magrittr)
```

**kairos** uses a set of S4 classes that represent different special
types of matrix. Please refer to the documentation of the
[**arkhe**](https://github.com/tesselle/arkhe) package where these
classes are defined.

*It assumes that you keep your data tidy*: each variable (type/taxa)
must be saved in its own column and each observation (sample/case) must
be saved in its own row.

This package provides an implementation of the chronological modeling
method developed by Bellanger and Husi
([2012](https://doi.org/10.1016/j.jas.2011.06.031)). This method is
slightly modified here and allows the construction of different
probability density curves of archaeological assemblage dates (*event*,
*activity* and *tempo*). Note that this implementation is experimental
(see `vignette("dating")`).

``` r
## Coerce dataset to abundance (count) matrix
zuni_counts <- as_count(zuni)
## Assume that some assemblages are reliably dated (this is NOT a real example)
## The names of the vector entries must match the names of the assemblages
zuni_dates <- c(
  LZ0569 = 1097, LZ0279 = 1119, CS16 = 1328, LZ0066 = 1111,
  LZ0852 = 1216, LZ1209 = 1251, CS144 = 1262, LZ0563 = 1206,
  LZ0329 = 1076, LZ0005Q = 859, LZ0322 = 1109, LZ0067 = 863,
  LZ0578 = 1180, LZ0227 = 1104, LZ0610 = 1074
)

## Model the event date for each assemblage
event <- date_event(zuni_counts, dates = zuni_dates, cutoff = 90)

## Plot activity and tempo distributions
plot_event(event, type = "activity", select = "LZ1105") +
  ggplot2::labs(title = "Activity plot") +
  ggplot2::theme_bw()
plot_event(event, type = "tempo", select = "LZ1105") +
  ggplot2::labs(title = "Tempo plot") +
  ggplot2::theme_bw()
```

![](man/figures/README-date-1.png)![](man/figures/README-date-2.png)

## Contributing

Please note that the **kairos** project is released with a [Contributor
Code of Conduct](https://www.tesselle.org/conduct.html). By contributing
to this project, you agree to abide by its terms.

<!-- README.md is generated from README.Rmd. Please edit that file -->

# leafpm - Interactively Edit Spatial Vector Features in R

[![Travis build
status](https://travis-ci.org/r-spatial/leafpm.svg?branch=master)](https://travis-ci.org/r-spatial/leafpm)
[![monthly](http://cranlogs.r-pkg.org/badges/leafpm)](https://www.rpackages.io/package/leafpm)
[![total](http://cranlogs.r-pkg.org/badges/grand-total/leafpm)](https://www.rpackages.io/package/leafpm)
[![CRAN](http://www.r-pkg.org/badges/version/leafpm?color=009999)](https://cran.r-project.org/package=leafpm)
[![status](https://tinyverse.netlify.com/badge/leafpm)](https://CRAN.R-project.org/package=leafpm)

`leafpm` is a plugin for [`leaflet`](https://github.com/rstudio/leaflet)
to provide map editing and drawing in R with
[`Leaflet.pm`](https://github.com/codeofsumit/leaflet.pm). It is based
closely off of
[`leaflet.extras`](https://github.com/bhaskarvk/leaflet.extras)
`addDrawToolbar()`. `leafpm` is intended to supplement `leaflet.extras`
with better support for snapping and holes.

## Installation

You can install the released version of leafpm from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("leafpm")
```

## Example

``` r
library(mapview)
library(leafpm)
library(sf)

outer1 = matrix(c(0,0,10,0,10,10,0,10,0,0),ncol=2, byrow=TRUE)
hole1 = matrix(c(1,1,1,2,2,2,2,1,1,1),ncol=2, byrow=TRUE)
hole2 = matrix(c(5,5,5,6,6,6,6,5,5,5),ncol=2, byrow=TRUE)
outer2 = matrix(c(11,0,11,1,12,1,12,0,11,0),ncol=2, byrow=TRUE)

pts1 = list(outer1, hole1, hole2)
pts2 = list(outer2)

pl1 = st_sf(geom = st_sfc(st_polygon(pts1)))
pl2 = st_sf(geom = st_sfc(st_polygon(pts2)))

mpl = st_sf(geom = st_combine(rbind(pl1, pl2)))

addPmToolbar(
  mapview(mpl)@map,
  targetGroup = "mpl"
)
```

## mapedit Integration

`leafpm` was designed to work as an editor in
[`mapedit`](https://github.com/r-spatial/mapedit), so you can get your
edits back into the `R` session. For instance,

``` r
#install.packages("mapedit")
library(mapedit)

drawFeatures(editor = "leafpm")
```

### Code of Conduct

Please note that the ‘leafpm’ project is released with a [Contributor
Code of Conduct](CODE_OF_CONDUCT.md). By participating in this project
you agree to abide by its terms.

### Acknowledgment

This project has been realized with financial
[support](https://www.r-consortium.org/projects) from the

<a href="https://www.r-consortium.org/projects/awarded-projects">
<img src="http://pebesma.staff.ifgi.de/RConsortium_Horizontal_Pantone.png" width="400">
</a>

---
title: "Spatial Intro 01: Intro"
teaching: 30
exercises: 10
questions:
- "What common formats contain spatial data?"
objectives:
- "Cover the basics of key data formats that may contain spatial information including shapefile, GeoTIFF and .csv."
- "Provide a brief overview of other formats that you may encounter when working with spatial data.'"
keypoints:
- "shapfile, GeoTIFF and .csv are common formats."
output:  
      html_document
---



> ## Prerequisites
> 
> - install `R`
> - install. packages: `raster`, `rgdal`, `sp`
{: .prereq}


raster, rgdal, sp


This tutorial introduces issues associated with spatial data management.

**R Skill Level:** Beginner


### Goals / Objectives

After completing this activity, you will:

- know stuff

### Install R Packages

```r
install.packages("raster")
install.packages("rgdal")
install.packages("sp")

# Or install multiple packages at once:
install.packages(c("raster", "rgdal", "sp"))
```

Now that we have installed the `R` packages, we need to load them.

```r
library("raster")
```

```
## Loading required package: methods
```

```
## Loading required package: sp
```

```r
library("rgdal")
```

```
## rgdal: version: 1.2-5, (SVN revision 648)
##  Geospatial Data Abstraction Library extensions to R successfully loaded
##  Loaded GDAL runtime: GDAL 1.11.5, released 2016/07/01
##  Path to GDAL shared files: /usr/local/Cellar/gdal/1.11.5_1/share/gdal
##  Loaded PROJ.4 runtime: Rel. 4.9.3, 15 August 2016, [PJ_VERSION: 493]
##  Path to PROJ.4 shared files: (autodetected)
##  Linking to sp version: 1.2-3
```

```r
library("sp")
```

## Additional Resources

- [Wikipedia article on GIS file formats](https://en.wikipedia.org/wiki/GIS_file_formats)

This should introduce the user to spatial data management issues - that we will discuss in this series.

## Get Started With Your Project -  File Organization

When we work with large, spatio-temporal data, it is a good idea to store large data sets in a general data directory that you can easily access from many projects. If you are working in a collaborative environment, use a shared data directory.

## One Dataset - Many Files

While text files often are self contained (one `CSV`) is composed of one unique file, many spatial formats contain several files. For instance, a shapefile (discussed below) contains 3 or more files, all of which must retain the same NAME and be stored in the same file directory, in order for you to be able to work with them.
We will discuss these issues as they related to two key spatial data formats - .shp (shapefile) which stores **vector** data and .tif (geotiff) which stores **raster** data in more detail, below.


# Basic Raster vs Vector overview

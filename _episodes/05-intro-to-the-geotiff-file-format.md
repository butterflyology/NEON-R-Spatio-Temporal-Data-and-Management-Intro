---
title: "Embedded Metadata - Into To the GeoTiff in R"
date:   2015-10-27
authors: [Leah Wasser]
contributors: [NEON Data Skills]
dateCreated: 2016-09-27
lastModified: 2016-12-29
packagesLibraries: [raster, rgdal, eml, devtools]
category: [course-materials]
excerpt: "This tutorial explains the geotiff file format that can be used to store raster data. It also covers metadata embedded within a geotiff - stored as tif tags."
permalink: course-materials/spatial-data/embedded-metadata-geotiff
class-lesson: ['intro-spatial-data-r']
sidebar:
  nav:
author_profile: false
nav-title: 'the geotiff format'
comments: false
order: 5
---


This tutorial covers embedded emtadata stored in the GeoTiff file format.

**R Skill Level:** Beginner

<div class="notice--success" markdown="1">


# Goals / Objectives

After completing this activity, you will:

* Understand the concept of metadata and be familiar with file formats that support embedded metadata.

### Install R Packages


**OPTIONAL** This tutorial uses these `R` packages in the examples.
 If you want to follow along, please make sure the following packages
 are installed:

* **raster:** `install.packages("raster")`
* **rgdal:** `install.packages("rgdal")`

* [More on Packages in R - Adapted from Software Carpentry.]({{site.baseurl}}R/Packages-In-R/)

****


### Additional Resources


* Information on the
<a href="http://cran.r-project.org/web/packages/raster/raster.pdf" target="_blank"> `raster` R package</a>

</div>

## Embedded Metadata - GeoTIFF

If we want to automate workflows, it's ideal for key metadata required to
process our data to be embedded directly in our data files. The **GeoTIFF**
(`fileName.tif`) is one common spatio-temporal format that can store
**metadata** directly in the `.tif` file itself.

### What is a GeoTIFF??

A **GeoTIFF** file stores metadata or attributes about the file as embedded
`tif tags`. A GeoTIFF is a standard `.tif` image format with additional spatial
(georeferencing) information embedded in the file as tags. These tags can
include the following raster metadata:

1. A Coordinate Reference System (`crs()`)
2. Spatial Extent (`extent()`)
3. Values for when no data is provided (NoData Value)
4. The resolution of the data

<i class="fa fa-star"></i> **Data Note:**  Your camera uses embedded tags to store
information about pictures that you take including the camera make and model,
and the time the image was taken.
{: .notice }

More about the  `.tif` format:

* <a href="https://en.wikipedia.org/wiki/GeoTIFF" target="_blank"> GeoTIFF on Wikipedia</a>
* <a href="https://trac.osgeo.org/geotiff/" target="_blank"> OSGEO TIFF documentation</a>


The `raster` package in `R` allows us to directly access `.tif tags`
programmatically. We can quickly view the spatial **extent**,
**coordinate reference system** and **resolution** of the data.

NOTE: not all geotiffs contain tif tags!

Next, let's explore the metadata associated with  a **Digital Surface Model** created
using LiDAR data for the NEON Harvard Forest field site.


The code below provides an example of how we can access spatial metadata
in `R`. We cover this in more detail, in the
[*Intro to Raster Data in R* tutorial](http://www.neondataskills.org/R/Introduction-to-Raster-Data-In-R).


```r
# load libraries
library(raster)
library(rgdal)

# set working directory to ensure R can find the file we wish to import
# setwd("working-dir-path-here")

# read in a GeoTIFF raster file (.tif) using the raster() function
DSM_HARV <- raster("NEON-DS-Airborne-Remote-Sensing/HARV/DSM/HARV_dsmCrop.tif")
```

```
## Error in .rasterObjectFromFile(x, band = band, objecttype = "RasterLayer", : Cannot create a RasterLayer object from this file. (file does not exist)
```

```r
# view Coordinate Reference System (note, this often contains horizontal units!)
crs(DSM_HARV)
```

```
## Error in crs(DSM_HARV): object 'DSM_HARV' not found
```

### Spatial Classes in R

There are specific classes designed to store some of the spatial metadata
associated with spatial data in R. Let's have a look.



```r
# assign crs to an object (class) to use for reprojection and other tasks
myCRS <- crs(DSM_HARV)
```

```
## Error in crs(DSM_HARV): object 'DSM_HARV' not found
```

```r
myCRS
```

```
## Error in eval(expr, envir, enclos): object 'myCRS' not found
```

```r
# what class is the new CRS object?
class(myCRS)
```

```
## Error in eval(expr, envir, enclos): object 'myCRS' not found
```

```r
# view spatial extent
extent(DSM_HARV)
```

```
## Error in extent(DSM_HARV): object 'DSM_HARV' not found
```

```r
# view spatial resolution
res(DSM_HARV)
```

```
## Error in res(DSM_HARV): object 'DSM_HARV' not found
```

The spatial `extent()` is a class as well. Let's have a look.


```r
# view object extent
myExtent <- extent(DSM_HARV)
```

```
## Error in extent(DSM_HARV): object 'DSM_HARV' not found
```

```r
myExtent
```

```
## Error in eval(expr, envir, enclos): object 'myExtent' not found
```

```r
class(myExtent)
```

```
## Error in eval(expr, envir, enclos): object 'myExtent' not found
```

```r
# print object name to return object metadata & attribute data

DSM_HARV
```

```
## Error in eval(expr, envir, enclos): object 'DSM_HARV' not found
```


We can use embedded metadata to programmatically perform processing tasks
on our data including reprojections, cropping and more.


<div class="notice--warning" markdown="1">
## Challenge - Explore GeoTiff Metadata

Open the file `NEON-DS-Airborne-Remote-Sensing/HARV/CHM/HARV_chmCrop.tif`. This
file is a Canopy Height Model (CHM) for the Harvard Forest Field site.

1. Create an **extent** and a **crs** object from the file.
2. Is the extent and CRS of the CHM different from the extent and CRS of the DSM
that we just opened above?
3. Now, open the file `NEON-DS-Landsat-NDVI/HARV/2011/ndvi/005_HARV_ndvi_crop.tif`.
Compare the extent and crs to the CHM and DSM. Are they different?

</div>


```
## Error in .rasterObjectFromFile(x, band = band, objecttype = "RasterLayer", : Cannot create a RasterLayer object from this file. (file does not exist)
```

```
## Error in crs(CHM.HARV): object 'CHM.HARV' not found
```

```
## Error in extent(CHM.HARV): object 'CHM.HARV' not found
```

```
## Error in .rasterObjectFromFile(x, band = band, objecttype = "RasterLayer", : Cannot create a RasterLayer object from this file. (file does not exist)
```

```
## Error in crs(ndvi1.HARV): object 'ndvi1.HARV' not found
```

```
## Error in extent(ndvi1.HARV): object 'ndvi1.HARV' not found
```

It appears as if there are some differences between the objects **extent** and
**crs**. What does this mean for us as we work with these data in the coming
tutorials? HINT: we will find out!


We will work with embedded metadata in both the
[*Introduction to Working With Vector Data in R*]( http://www.neondataskills.org/tutorial-series/vector-data-series/)
and
[*Introduction to Working With Raster Data in R*]( http://www.neondataskills.org/tutorial-series/raster-data-series/)
series!

## Embedded Metadata - Hierarchical Data Formats (HDF5)

HDF5 is another file type that supports embedded metadata format. Check out the
[NEON Data Skills HDF5 tutorials](http://www.neondataskills.org/tutorial-series/intro-hdf5-r-series/)
to learn more about how HDF5 stores metadata.

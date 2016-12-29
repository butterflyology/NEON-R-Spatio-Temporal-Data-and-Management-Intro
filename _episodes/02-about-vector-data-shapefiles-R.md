---
layout: single
title: "Intro to Vector Data & Shapefiles in R"
authors: [Leah Wasser]
contributors: [NEON Data Skills]
dateCreated: 2016-09-25
lastModified: 2016-12-29
packagesLibraries: [raster, rgdal, sp]
category: [course-materials]
excerpt: "This tutorial introduces the vector spatial data format, stored in
shapefile format."
permalink: course-materials/spatial-data/about-shapefiles
class-lesson: ['intro-spatial-data-r']
sidebar:
  nav:
nav-title: 'vector intro'
author_profile: false
comments: false
order: 2
---

<div class="notice--success" markdown="1">


# Goals / Objectives

After reading this post, you will:

* Understand the key files associated with a shapefile: shp, dbf, shx.


### Install R Packages

* **raster:** `install.packages("raster")`
* **rgdal:** `install.packages("rgdal")`


****

### Additional Resources

* Wikipedia article on
<a href="https://en.wikipedia.org/wiki/GIS_file_formats" target="_blank">
GIS file formats.</a>

</div>

# Types of Spatial Data

Spatial data are represented in different ways and are stored using different structures and within different file formats. In this tutorial, we will focus on vector data - data that are composed of points, lines and/or polygons.

## Vector Data - Points, Lines, Polygons

Vector data, are often used to store elements on the earth's surface that
can be described using discrete shapes or locations. Examples of this include:

 * The path or centerline of a road
 * The location of a study area.
 * Plot locations,
 * Boundaries of states, countries, census areas,
 * Water body boundaries (lakes and oceans).

Vector data are composed of discrete geometric locations (x, y values) known as
**vertices** that define the "shape" or location of the spatial object. The organization
of the vertices determines the type of vector that we are working
with: **point**, **line** or **polygon**.

<figure>
    <a href="{{ site.baseurl }}/images/dc-spatial-intro/pnt_line_poly.png">
    <img src="{{ site.baseurl }}/images/dc-spatial-intro/pnt_line_poly.png"></a>
    <figcaption> There are 3 types of vector objects: points, lines or
    polygons. Each vector object type has a different structure.
    Image Source: National Ecological Observatory Network (NEON)
    </figcaption>
</figure>

* **Points:** Each individual point is defined by a **single x, y coordinate**.
There can be many points in a vector point file. Examples of point data include:
	+ sampling locations,
	+ the location of individual trees or
	+ the location of plots.
* **Lines:** Lines are composed of **many (at least 2) vertices that
are connected**. For instance, a road or a stream may be represented by a line.
This line is composed of a series of segments, each "bend" in the road or stream
represents a vertex that has defined `x, y` location.
* **Polygons:** A polygon consists of **3 or more vertices that are connected
and "closed"**. Occasionally, a polygon can have a hole in the middle of it
(like a doughnut), this is something to be aware of but not an issue we will
deal with in this tutorial series. Objects often represented by polygons
include:
	+ outlines of plot boundaries,
	+ lakes,
	+ oceans and
	+ states or country boundaries.


<i class="fa fa-star"></i> **Data Tip:** A shapefile will only contain **one
type of vector data**: points, lines or polygons.
{: .notice}


```r

# load libraries required to work with spatial data
library(raster) # commands to view metadata from vector objects
library(rgdal) # library of common GIS functions

# Open shapefile
roads_HARV <- readOGR("NEON-DS-Site-Layout-Files/HARV","HARV_roads")
## Error in ogrInfo(dsn = dsn, layer = layer, encoding = encoding, use_iconv = use_iconv, : Cannot open file

# view slots available for the object
slotNames(roads_HARV)
## Error in is(x, "classRepresentation"): object 'roads_HARV' not found

# view all methods available for that object
# methods(class = class(roads_HARV))
```


## Stucture of a Lines Feature

If we are working with a shapefile containing **line** data, then each line
consists of 2 or more vertices that are connected. We can view each set of coordinates
for that object using `R`.


```r

# view the coordinates for each vertex, for the last feature in the spatial object
roads_HARV@lines[13]
## Error in eval(expr, envir, enclos): object 'roads_HARV' not found

# view the coordinates for the last feature in the spatial object
roads_HARV@lines[14]
## Error in eval(expr, envir, enclos): object 'roads_HARV' not found
```


<div class="notice--warning" markdown="1">
## Challenge

* Why didn't `roads_HARV@lines[14]` return any vertex coordinates?

</div>

## Spatial Data Attributes

Each object in a shapefile, is called a `feature`. Each `feature` has one or
more `attributes` associated with it.

Shapefile attributes are similar to fields or columns in a spreadsheet. Each row
in the spreadsheet has a set of columns associated with it that describe the row
element. In the case of a shapefile, each row represents a spatial object - for
example, a road, represented as a line in a line shapefile, will have one "row"
of attributes associated with it. These attributes can include different types
of information that describe shapefile `features`. Thus, a road,
may have a name, length, number of lanes, speed limit, type of road and other
attributes stored with it.

<figure>
    <a href="{{ site.baseurl }}/images/dc-spatial-intro/attribute_table.png">
    <img src="{{ site.baseurl }}/images/dc-spatial-intro/attribute_table.png"></a>
    <figcaption>Each spatial feature in an R spatial object has the same set of
    associated attributes that describe or characterize the feature.
    Attribute data are stored in a separate *.dbf file. Attribute data can be
    compared to a spreadsheet. Each row in a spreadsheet represents one feature
    in the spatial object.
    Image Source: National Ecological Observatory Network (NEON)
    </figcaption>
</figure>



```r
# view all attributes for a spatial object
# note, the code below just looks at the first 3 features
head(roads_HARV@data, 3)
## Error in head(roads_HARV@data, 3): object 'roads_HARV' not found
```

In the map below of the Harvard Forest field site, there are different features
that are stored as different spatial object types. Check out the NEON / Data
Carpentry
[*Introduction to Working with Vector Data in R* tutorial series]({{ site.basurl }}/tutorial-series/vector-data-series/) to learn more about making these types
of maps in `R`.

<figure>
    <a href="{{ site.baseurl }}/images/dc-spatial-intro/plot-color.png">
    <img src="{{ site.baseurl }}/images/dc-spatial-intro/plot-color.png"></a>
    <figcaption>The map above is created using both point and linevector data
    layers.
    </figcaption>
</figure>

<div class="notice--warning" markdown="1">

## Challenge: Shapefiles

Have a look at the map above:  **Study Plots by Soil Type**. What is the minimum number of
shapefiles that are required to create this map? How do you know?

</div>





### Vector Data in .CSV Format

The shapefile format is one (very common) way to store vector data. However,
you may encounter is in other formats. For example, sometimes, point data are
stored as a Comma Separated Value (.CSV) format.


Check out the NEON / Data Carpentry tutorial on
[converting from .csv to a Shapefile in R.](http://neondataskills.org/Vector 04: Convert from .csv to a Shapefile in R).

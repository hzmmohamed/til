---
date: 15-02-2022
title: Splitting a linestring with shapely (accurately)
tags: ['shapely', 'data-processing', 'geospatial']
draft: true
---

It's a nightmare!

We spent a full day trying to get the split function to work correctly with geometries in a projected CRS in meters. And it didn’t work.

Is it a python problem? Is the split function implemented entirely in python. What are the primitives that C libraries (PROJ and GEOS) limit themselves to? Can something like ST_linelocatepoint be implemented in shapely?
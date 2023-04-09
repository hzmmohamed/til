---
date: 09-04-2023
title: Histograms for vector layers in QGIS
tags: ['qgis', 'eda']
---
Today, I learned [three ways to create historgrams in QGIS](https://youtu.be/6NX5ybdoHoo).

## First Method: Histogram tab in Symbology Settings
When the symbology is set to graduated, the histogram tab appears. It lets you visualize the distribution, your breakpoints and lets you edit them.

## Use the Histogram tool from Processing Toolbox
This generates the result as an HTML page that contains the histogram.

## Use the Data Plotly plugin
This one is the most featureful and dynamic way to exploring the data through the histogram. It has other kinds of visualizations as well.
For the histogram, a cool feature is how you can click on a bin in the histogram to "select" the corresponding features on the map canvas. It's a pretty interesting feature, this one.

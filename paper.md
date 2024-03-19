---
title: 'Cutview: A NetCDF Viewer and Transecting Tool'
tags:
  - Python
  - Oceanography
  - Atmospheric Sciences
  - NetCDF
  - visualization
authors:
  - name: Robin Chartrand
    orcid: 0000-0001-6948-8380
    affiliation: 1
  - name: Robert Fajber
    affiliation: 2
  - name: Georgy Manucharyan
    affiliation: 1
affiliations:
  - name: University of Washington, Seattle, WA, USA
    index: 1
  - name: ????
    index: 2
date: 22 September 2023
bibliography: paper.bib
---

# Statement of Need

CutView is a simple yet flexible NetCDF file and image viewer that is designed to require no programming or GIS 
experience to use. It is a GUI meant to be used to get a “quick” visualization of NetCDF data, but CutView additionally 
allows a user to view and produce plots of transects of NetCDF data along various dimensions. This is a commonly 
performed task in oceanography and atmospheric sciences research used to understand the vertical composition of a 
section of ocean or atmosphere. For example, @Sivkov:2021 used such a vertical transect (Fig. 1) to study 
the vertical distributions of suspended particulate matter across the Atlantic ocean.

![Figure 1: Distribution of the SPM volume concentration (ppm) on the Ioffe-2000 transect, done with Ocean Data View 
[@odv]. Figure and discription from @Sivkov:2021](images/figure1.png)

In another example, @Gutjahr:2022 used vertical transects of modeled climate and ocean data in Greenland to 
study air-sea interactions during a Katabatic storm.

![Figure 2: Vertical transects (daily means) along the Ikertivaq valley and Sermilik Trough: (a) wind speed, (b) 
turbulent kinetic energy in ocean, (c) atmospheric vertical velocity with cloud cover (10% dashed and 50% solid 
contours), (d) ocean potential temperature, (e) atmospheric potential temperature, and (f) ocean density (σΘ = σ – 1,000 
kg m⁻³, σΘ = 27.6 kg m⁻³ as white contour). The green line in (b, d, and f) marks the depth of the mixed layer (σΘ = 0.03 
kg m⁻³). Figure and discription from @Gutjahr:2022](images/figure2.png)

Such transect selecting tools are a feature common in GIS software [@qgis, @transectizer, @grass_gis] and are present in 
some more complex viewers that work with unstructured data [@odv], but these options are all either meant for more 
complicated data formats or require a user to spend a great amount of time learning how to use the software before they 
can do any meaningful data analysis. CutView intends to bring this transecting functionality to users who aren’t 
interested in serious data analysis tools but are just trying to get a quick look at a NetCDF file. There are many 
simple NetCDF viewers that already serve this audience [@NcView, @Panoply, @ncvue], but none of these simpler viewers 
allow users to take transects across NetCDF data.

![Figure 3: An overview graphic of the various functionalities of CutView.](images/cutviewgraphic.png)

# Functionality

As per the name, CutView’s functions can be divided into two main categories:

## View

CutView allows users to load and view any image or Netcdf file in a .JPG, .PNG, .JPEG, or .NC format, and has adjustable 
graphics to adapt to different file sizes. In the case of NetCDF files, the user can choose between different variables 
and dimensions of the data to view. The user can select which dimensions to use as the x, y and z dimensions for the 
viewer, and once displayed the user can switch between different displays of the x, y dimensions at different z values. 
This is intuitive for many NetCDF files which contain three-dimensional datasets with data arrays at different vertical 
heights or depths. The data is displayed as an image mapped to a color map, which can be changed by the user as well as 
the contrast of the image. Once loaded and configured users can drag, rotate, flip, and zoom in on the file however they 
please.

## Cut

Using CutView users can mark out and plot transects onto loaded images or NetCDF data using two tools:

The first is the simple transect tool, where users can click on two endpoints and a line will be drawn between them. If the loaded file is an image, the mean of the RGB values of each pixel along that line will be selected. The pixels are interpolated using linear interpolation to improve the accuracy of the pixel selection. If the loaded file is a NetCDF file, the data values from the original dataset (also interpolated) are selected along that line. Multiple such transects can be drawn and plotted all together. 

The second is the transect marker tool. Using this tool users click points along a feature and transects of a set width will be made orthogonal to the line marked out by the user. This width can be adjusted at any point in the marking process and multiple markers can be drawn on the same file and plotted together. For use on large projects worked on over multiple sessions, the marker data saved from the plotting menu can be reuploaded back into CutView and continued.

In the plotting menu users can select which transects/markers to plot, and if the file is a NetCDF file the user can additionally plot multiple variables and values along the chosen z dimension. Additionally, users can see a plot of the transect data values for all z values shown as an image, which can be done for multiple variables at once. From here users can choose to save the data to a .JSON file as well as save the plot to either a .PNG or .PDF format. The JSON file groups the pixel data and their coordinates together and labels them by the transect number shown on the viewer. If the marker tool was used, the transects are further grouped and labeled by their marker number. This labeled and organized data structure aims to be easily loaded and understood using minimal programming experience in a language like Python or R.


# References
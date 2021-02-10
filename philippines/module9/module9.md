# **Module 9 - Raster processing and analysis**

**Author**: Codrina

## Pedagogical Introduction

This module is focused on a specific type of geographical data model: raster geodata.

By the end of this module, learners will have the basic understanding of the following concepts:

*   raster data model
*   grid point vs grid cell
*   bands of a raster dataset
*   map algebra 
*   the four resolutions of a raster (spatial, temporal, spectral and radiometric)
*   Resampling
*   Batch processing
*   change detection


## **Required Tools and Resources**

*   This module has been prepared using [QGIS version 3.16.1 - Hannover](https://qgis.org/en/site/forusers/download.html)
*   The datasets used for all exercises detailed in this module are presented in the table below:
*   The coordinate reference system used is the PRS92 / Philippines zone 3, EPSG 3123. 

## Prerequisites: 

*   Basic knowledge of operating a computer
*   A robust understanding of modules 0, 1, 2, 6 and 8 of this curriculum. 


## Thematic introduction

## Breakdown of the concepts

### The raster data model

A raster is a regular matrix of values, as in figure 9.1.


![A matrix of values](media/fig91.png "A matrix of values")

Figure 9.1 - A matrix of values

Values can be assigned either to** grid points**, mostly to the centroids, and in this case the raster can be referred to as a lattice. The second option is for the values to be assigned to the whole of the **grid cell **- called pixels (see figure 9.2). For the first case, the raster usually represents a continuous field, such as elevation, temperature, precipitations, chemical concentrations etc. For the second case, when the values are assigned to the entire area of the pixel, the raster usually represents an image - a satellite image, a scanned map, converted vector maps (see Phase 2). It must be noted that this data model is not particularly efficient for networks and other types of data heavily dependent on lines, such as property boundaries. 


![On the left side, the values are assigned to centroids. On the right, values are assigned to the grid cell area - the pixel.](media/fig92.png "On the left side, the values are assigned to centroids. On the right, values are assigned to the grid cell area - the pixel.")

Figure 9.2 - On the left side, the values are assigned to centroids. 

On the right, values are assigned to the grid cell area - the pixel. 				


### Rational of raster processing

As in the case of vector data processing, the rationale behind the raster data processing is based on the very same capacity of the geographical information systems to store, process  and represent information of the real world phenomena, just that the way in which this is accomplished differs. Instead of having distinct points, lines and polygons stored as collections of x and y coordinates, we have a matrix of values that drapes over a specific area like a mesh. To have a clearer picture in mind, imagine the temperature maps shown on TV. Temperature is a continuous field, there are no places on the surface of the Earth without temperature, be it positive, negative or 0.

Many operations can be performed on raster datasets, the concept of geoprocessing detailed in module 8 applies here as well. The term used to encompass the operations that can be performed on rasters is _map algebra_. 

**Map algebra** represents a set of primitive operations[^1] in a GIS which allows two or more raster layers of _similar dimensions_ to produce a new raster layer (map) using various operations such as addition, subtraction, comparison etc.  

There are four categories of operations that can be performed on rasters, as follows: 

*   Arithmetic operations: addition, subtraction, multiplication, division.
*   Statistical operations: minimum, maximum, average, median.
*   Relational operations provide comparisons between cells using functions such as greater than, smaller than or equal to.
*   Trigonometric operations: sine, cosine, tangent, arcsine between two or more raster datasets.
*   Exponential and logarithmic operations use exponent and logarithm functions.

For each of these operations, there are algorithms implemented in most GIS environments that allow a user to apply them on her data. In the following, we will also implement some of the most common operations to get a sense of how to work with and what should one expect from this kind of data processing. 

The concept of _similar dimensions_ refers to the characteristics of the raster datasets. That is, the operations detailed above can not be performed with meaningful results on 2 raster datasets with different spatial, temporal or spectral resolutions. In the following, we will very shortly introduce all four resolutions that are relevant for raster imagery.

Remembering what are the 4 types of resolutions of a satellite imagery (raster with values assigned to cell area - pixels): 

1. **Spatial resolution** corresponds to the elementary size of the ground surface measured, it is expressed in units of length and it represents the length of a pixel side (see figure 9.3). For example, as you’ve seen in module 3, the High Resolution Settlement Layer Data has a spatial resolution of 30 meters, i.e. each pixel of the dataset estimates the number of people living within a 30-meter. 

2. **Temporal resolution** is associated with overhead imagery (images acquired by satellites, planes, helicopters, drones) and it corresponds to the period between 2 consecutive images of the exact same point on Earth, taken in the same conditions (as much as possible), such as the same aircraft, same altitude etc. For example, Landsat 8 has a temporal resolution of 16 days, i.e. each point on Earth is revisited by the Landsat 8 satellite each 16 days[^2]. 

3. **Spectral resolution** - the sensors onboard of satellites or airplanes capture electromagnetic radiance coming from all objects on Earth - water, settlements, forests, roads, buildings, bare land etc. - and the sensors are specifically built to capture it at a given known spectral band (or wavelength). The human eye can see a very small part of the electromagnetic spectrum - the visible light (red, green and blue), but sensors can ‘see’ much more! (see figure 9.4)


![Electromagnetic spectrum (photo credit [NASA Science](https://science.nasa.gov/ems/01_intro))](media/fig94.png "Electromagnetic spectrum (photo credit [NASA Science](https://science.nasa.gov/ems/01_intro))")

Figure 9.4 - Electromagnetic spectrum (photo credit NASA Science - [https://science.nasa.gov/ems/01_intro](https://science.nasa.gov/ems/01_intro))

4. **Radiometric resolution** is determined by the number of bits into which the recorded radiation is divided. In 8-bit data, the digital numbers (DN) can range from 0 to 255 for each pixel (28 ¼ 256 total possible numbers). Clearly, more bits means that the sensor can detect more subtle changes in the energy it captures, that leads to a ‘clearer’ image, a  higher radiometric accuracy of the sensor but also requires more space to store the data. 

**Spectral bands**

A raster dataset contains one or more layers called bands. Each band stores another set of information on the area the raster covers. Each band has the exact same extent and coordinates, but not necessarily the same spatial resolution. Also, aside from the values stored, there are other key properties contained, such as: maximum, minimum and mean cell values and _histogram_ of cell values. 

A **histogram** is an approximate representation of the distribution of numerical data (see figure 9.5), in other ways is a manner in which one can get a sense of the data at hand.


![Example of a histogram, where x is a raster layer](media/fig95.png "Example of a histogram, where x is a raster layer")

Figure 9.5 - Example of a histogram, where x is a raster layer

Why is this important in our context? Because, as mentioned at the beginning, a raster is a matrix of continuous numerical values (remember the temperature example) and a histogram helps the user understand how the values of his rasters are distributed. Each bar groups the cell values that fall in a specific range, higher the bar more cells have values in that specific range. In case, the raster has more than one band, then the histogram will be computed for each one. There are no gaps between the ranges depicted on a histogram, the histogram is used only for continuous data.  


## Main content 

### Phase 1: Understanding your raster data.

In the last two decades, the number of satellites capturing data from Earth has grown exponentially. Furthermore, an open data access policy that has been adopted by different space agencies, such as NASA for the [Landsat program](https://www.usgs.gov/core-science-systems/nli/landsat/landsat-data-access?qt-science_support_page_related_con=0#qt-science_support_page_related_con) or the European Space Agency for the [Copernicus program](https://www.copernicus.eu/en/access-data), has opened the door for an overwhelming stream of Earth Observation data. As a natural consequence, the scientific progress of algorithms, methodologies and the development of more powerful tools to process raster data - especially satellite imagery - has been impressive and extensive in fields such as agriculture, forestry, urban development, humanitarian activities, ocean and sea water monitoring, security and so many more. In the following 3 phases, we will introduce some of the most common processing techniques and what results to expect from them. 


#### Step 1. Prepare your working environment. 

We will strat by adding to your QGIS project all the raster datasets that we will be working with, as follows: 

*   High Resolution Settlement Layer Data 
*   ALOS Global Digital Surface Model "ALOS World 3D - 30m (AW3D30)"
*   Moderate Dynamic Land Cover: the 5 available epochs 2015, 2016, 2017, 2018 and 2019. 

As the High Resolution Settlement Layer Data has been presented in a previous module, we will also detail information on the other 2 dataset we will employ in this module. 

1. ALOS Global Digital Surface Model (AW3D30) is a global digital surface model (DSM) dataset with a horizontal resolution of approximately 30 meters (1 arcsec mesh). A DSM includes ground surface, vegetation and man-made objects, such as buildings, bridges etc. as opposed to the digital elevation model that considered strictly the terrain. 
2. Dynamic Land Cover Map is a  Copernicus Global Land Service (CGLS) product derived from the PROBA-V 100 m time-series and several other land cover datasets.  The product provides primary land cover discrete classes, as well as continuous field layers for all basic land cover classes that provide proportional estimates for vegetation/ground cover for the land cover types. The product has 3 bands: discrete_classification, forest_type and urban_coverfraction. The following 2 tables present the values for each discrete class: 

Tabel 1 Discrete_classification band value table

<table>
  <tr>
   <td><strong>Value</strong>
   </td>
   <td><strong>Color</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>0
   </td>
   <td>282828
   </td>
   <td>Unknown. No or not enough satellite data available.
   </td>
  </tr>
  <tr>
   <td>20
   </td>
   <td>FFBB22
   </td>
   <td>Shrubs. Woody perennial plants with persistent and woody stems and without any defined main stem being less than 5 m tall. The shrub foliage can be either evergreen or deciduous.
   </td>
  </tr>
  <tr>
   <td>30
   </td>
   <td>FFFF4C
   </td>
   <td>Herbaceous vegetation. Plants without persistent stem or shoots above ground and lacking definite firm structure. Tree and shrub cover is less than 10 %.
   </td>
  </tr>
  <tr>
   <td>40
   </td>
   <td>F096FF
   </td>
   <td>Cultivated and managed vegetation / agriculture. Lands covered with temporary crops followed by harvest and a bare soil period (e.g., single and multiple cropping systems). Note that perennial woody crops will be classified as the appropriate forest or shrub land cover type.
   </td>
  </tr>
  <tr>
   <td>50
   </td>
   <td>FA0000
   </td>
   <td>Urban / built up. Land covered by buildings and other man-made structures.
   </td>
  </tr>
  <tr>
   <td>60
   </td>
   <td>B4B4B4
   </td>
   <td>Bare / sparse vegetation. Lands with exposed soil, sand, or rocks and never has more than 10 % vegetated cover during any time of the year.
   </td>
  </tr>
  <tr>
   <td>70
   </td>
   <td>F0F0F0
   </td>
   <td>Snow and ice. Lands under snow or ice cover throughout the year.
   </td>
  </tr>
  <tr>
   <td>80
   </td>
   <td>0032C8
   </td>
   <td>Permanent water bodies. Lakes, reservoirs, and rivers. Can be either fresh or salt-water bodies.
   </td>
  </tr>
  <tr>
   <td>90
   </td>
   <td>0096A0
   </td>
   <td>Herbaceous wetland. Lands with a permanent mixture of water and herbaceous or woody vegetation. The vegetation can be present in either salt, brackish, or fresh water.
   </td>
  </tr>
  <tr>
   <td>100
   </td>
   <td>FAE6A0
   </td>
   <td>Moss and lichen.
   </td>
  </tr>
  <tr>
   <td>111
   </td>
   <td>58481F
   </td>
   <td>Closed forest, evergreen needle leaf. Tree canopy >70 %, almost all needle leaf trees remain green all year. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>112
   </td>
   <td>9900
   </td>
   <td>Closed forest, evergreen broad leaf. Tree canopy >70 %, almost all broadleaf trees remain green year round. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>113
   </td>
   <td>70663E
   </td>
   <td>Closed forest, deciduous needle leaf. Tree canopy >70 %, consists of seasonal needle leaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>114
   </td>
   <td>00CC00
   </td>
   <td>Closed forest, deciduous broad leaf. Tree canopy >70 %, consists of seasonal broadleaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>115
   </td>
   <td>4E751F
   </td>
   <td>Closed forest, mixed.
   </td>
  </tr>
  <tr>
   <td>116
   </td>
   <td>7800
   </td>
   <td>Closed forest, not matching any of the other definitions.
   </td>
  </tr>
  <tr>
   <td>121
   </td>
   <td>666000
   </td>
   <td>Open forest, evergreen needle leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, almost all needle leaf trees remain green all year. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>122
   </td>
   <td>8DB400
   </td>
   <td>Open forest, evergreen broad leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, almost all broadleaf trees remain green year round. Canopy is never without green foliage.
   </td>
  </tr>
  <tr>
   <td>123
   </td>
   <td>8D7400
   </td>
   <td>Open forest, deciduous needle leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, consists of seasonal needle leaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>124
   </td>
   <td>A0DC00
   </td>
   <td>Open forest, deciduous broad leaf. Top layer- trees 15-70 % and second layer- mixed of shrubs and grassland, consists of seasonal broadleaf tree communities with an annual cycle of leaf-on and leaf-off periods.
   </td>
  </tr>
  <tr>
   <td>125
   </td>
   <td>929900
   </td>
   <td>Open forest, mixed.
   </td>
  </tr>
  <tr>
   <td>126
   </td>
   <td>648C00
   </td>
   <td>Open forest, not matching any of the other definitions.
   </td>
  </tr>
  <tr>
   <td>200
   </td>
   <td>80
   </td>
   <td>Oceans, seas. Can be either fresh or salt-water bodies.
   </td>
  </tr>
</table>



Tabel 2 forest_type band value table

<table>
  <tr>
   <td>Value
   </td>
   <td>Color
   </td>
   <td>Description
   </td>
  </tr>
  <tr>
   <td>0
   </td>
   <td>282828
   </td>
   <td>Unknown
   </td>
  </tr>
  <tr>
   <td>1
   </td>
   <td>666000
   </td>
   <td>Evergreen needle leaf
   </td>
  </tr>
  <tr>
   <td>2
   </td>
   <td>9900
   </td>
   <td>Evergreen broad leaf
   </td>
  </tr>
  <tr>
   <td>3
   </td>
   <td>70663E
   </td>
   <td>Deciduous needle leaf
   </td>
  </tr>
  <tr>
   <td>4
   </td>
   <td>A0DC00
   </td>
   <td>Deciduous broad leaf
   </td>
  </tr>
  <tr>
   <td>5
   </td>
   <td>929900
   </td>
   <td>Mix of forest types
   </td>
  </tr>
</table>



To organize your layers better, group them by category, as follows: for the land cover 5 raster layers, make one group named Land Cover (in the TOC, click on the Add group pictogram). For the digital surface model, make one group named JAXA[^3] DSM. 

Don’t forget to also add the boundary of the working area, province of Pampanga, which is a vector dataset. 

Your QGIS map window should look like in figure 9.6, maybe in slightly different colors. 


![Loaded raster datasets](media/fig96.png "Loaded raster datasets")

Figure 9.6 - Loaded raster datasets


#### Step 2. Understand what you are looking at. 

Next, we will use a series of tools that will allow us to get a sense of the data we are working with. 

After loading all the datasets, we will check the coordinate reference system in which all our datasets are in.  As we know from previous modules, QGIS offers the possibility to reproject all datasets loaded into the project on the fly, however that could lead to geoprocessing issues along the way. Thus, even if all layers are correctly overlaid, as can one say by visual inspection, we will proceed in reprojecting them all in the official coordinate system of our region of interest, Pampanga province - EPSG: 3123. 

There are several ways to get information on the loaded layers in QGIS, some providing the user with more details than others. For a quick overview of a dataset’s metadata, one must select the layer - double click and open `Properties ‣ Information. `

For layer hrsl_phl_pop, the information window would look like in figure 9.7. 


![Extracting basic metadata from a raster layer](media/fig97.png "Extracting basic metadata from a raster layer")

Figure 9.7 - Extracting basic metadata from a raster layer

With regard to our first question on what CRS is being used for the datasets we have loaded, we can observe that even if the HRSL is correctly overlaid, the dataset native’s projection is EPSG 4326 - WGS 84 - Geographic, with units measured in degrees. We also identify that this specific raster layer has only one band, yet the pixel size is difficult to read as the measurement is in degrees and not meters, which would make it easier to understand. 

Thus, the first thing to do is to reproject all datasets we will work with in the same coordinate system - EPSG 3123.

Starting with the HRSL datasets, we go to `Raster ‣ Projections ‣ Warp (Reproject) `(see figure 9.8).` `


![Reproject functionality in QGIS](media/fig98.png "Reproject functionality in QGIS")

Figure 9.8 - Reproject functionality in QGIS

After selecting the Warp functionality, a new window will appear allowing the user to set the correct parameters (see figure 9.9). 


![Warp (reproject) QGIS window](media/fig99.png "Warp (reproject) QGIS window")

Figure 9.9 - Warp (reproject) QGIS window

You will notice that unlike when you reprojected vector datasets, there is a new parameter that you can set “Resampling method to use”. 

**Resampling **represents the interpolation of the cell values so that it transforms the raster as indicated by the user. There are multiple resampling methods available within the warp functionality, each with its own mathematical support. Yet, detailed explanations on each one is not the scope of this exercise. Further reading is available at references. 

In this particular case, we want to reproject population data - numerical values. 

and based on the selected resampling method (nearest neighbour),  the coordinate of each output pixel will be used to calculate a new value from close-by pixel values in the input layer (see figure 9.10). 


![Resample method - nearest neighbour](media/fig910.png "Resample method - nearest neighbour")

Figure 9.10 - Resample method - nearest neighbour (photo credit: ILWIS documentation - [(http://spatial-analyst.net/ILWIS/htm/ilwisapp/resample_functionality.htm](http://spatial-analyst.net/ILWIS/htm/ilwisapp/resample_functionality.htm))

Input pixels are represented by dashed black lines, coordinates of input pixels by black dots; output pixels are represented by red solid lines, coordinates of output pixels by red plus signs. The grey arrows indicate how output values are determined. It can be seen in figure 9.10, some values of the input map may be used twice in the output map, while other input values may not be used at all. That is why, although one of the fastest methods to resample,  it is not appropriate in our case, as we are working with numerical data - population data. This resampling method is suitable for categorical data - such as land cover values. 

To reproject our population raster dataset, we will use the bilinear interpolation method to resample the pixel values (see figure 9.11).


![Resample method - bilinear](media/fig911.png "Resample method - bilinear")

Figure 9.11 - Resample method - bilinear (photo credit: ILWIS documentation - [(http://spatial-analyst.net/ILWIS/htm/ilwisapp/resample_functionality.htm](http://spatial-analyst.net/ILWIS/htm/ilwisapp/resample_functionality.htm))

The bilinear method determines the new value of a cell based on a weighted distance average of the four nearest input cell centers. It is useful for continuous data and will cause some smoothing of the data. 

We proceed in checking the CRS of the 5 land cover datasets that we have loaded into our QGIS project. Accessing `Layer properties ‣ information`, we can see that all 5 land cover layers are projected in EPSG:3857 - WGS 84 / Pseudo-Mercator. One solution would be to use the Reproject tool and configure for each layer individually. Yet, a faster way is to use the reproject functionality running as a _batch process_.

**Batch processing** is the ability of running repetitive processes on data, with minimum user interaction. Most QGIS functionalities have this option available and it can be activated in the process window by switching to the Run batch process tab (see figure 9.12). 


![Batch processing tab on a QGIS functionality window](media/fig912.png "Batch processing tab on a QGIS functionality window")

Figure 9.12 - Batch processing tab on a QGIS functionality window


For the 5 land cover raster layers, we will use the batch processing and as resample method nearest neighbour. To add a new layer, click on the + pictogram. To automatically fill the CRS and resampling method parameters, click on autofill button on top of the corresponding columns and select `Fill down`. Rename the reprojected rasters by adding the EPSG code at the end of the name, for example LandCover2015, will become landCover2015_3123. Set your parameters as in figure 9.13: source CRS: EPSG: 3857, target CRS EPSG 3123, resampling method to use: nearest neighbour (we explained in the paragraph above why), nodata value for output bands: 255 (from the information window, we see the data type - yte - 8bit unsigned integer - which means that the maximum value can be 255), output resolution:100 m (as the initial land cover rasters). After setting all parameters, check the box in the left corner of the window -` Load layers on completion.` Hit `Run`. 


![Batch processing to reproject the land cover rasters](media/fig913.png "Batch processing to reproject the land cover rasters")

Figure 9.13 - Batch processing to reproject the land cover rasters

Next comes the digital surface model rasters. As one can observe, to cover our region of interest, we needed several _raster tiles_. When raster files become too large - imagine one single DSM file at 30 m for Europe which has over 10 million square kilometers - they are splitted into **tiles **because, in smaller areas, they are more easily manageable. 

Although we could use the wrap tool in batch mode to reproject all the DSM raster files, at a visual inspection, one can also notice that the delimitations between each tile is fairly visible, making it, at least, visually unattractive. What would be useful is to have a complete overview of the terrain, as a continuous phenomena - as it is, in fact - without artificial disruptions. To obtain that, we will use the GDAL merge tool, available in the Processing toolbar to merge all DSM rasters together. To open it, go to `Processing ‣ Toolbox `and in the search bar write merge (see figure 9.14)`.`


![Finding the GDAL merge tool in the Processing Toolbox](media/fig914.png "Finding the GDAL merge tool in the Processing Toolbox")

Figure 9.14 - Finding the GDAL merge tool in the Processing Toolbox 

In the merge window that opens, select the DSM raster files that we want to mosai and click run. Save the result as DSM_mosaic. The result should look like in figure 9.15. 


![Mosaic of all DSM files corresponding to our work region](media/fig915.png "Mosaic of all DSM files corresponding to our work region")

Figure 9.15 - Mosaic of all DSM files corresponding to our work region

Now, we can proceed to reprojecting the mosaic - one file, instead of 6 files. Go to `Raster ‣ projection ‣ Wrap (reproject)` and set the known parameters: Source CRS EPSG 4326, Target CRS: EPSG:3123, Resampling method: Nearest neighbour, output file resolution - 30 m. Save the result as DSM_mosaic_3123. 

At his point, we should have all layers in the same CRS - EPSG 3123. 

We can do another check to make sure that all rasters we are working with are projected as well as getting any additional information on the data by running a batch process of Raster Information on all. To open the functionality window, go to `Raster ‣ Miscellaneous ‣ Raster Information`. Your batch processing raster information window should look as in figure 9.16. 


![Batch process to extract information in a separate HTML file for multiple raster layers](media/fig916.png "Batch process to extract information in a separate HTML file for multiple raster layers")

Figure 9.16 - Batch process to extract information in a separate HTML file for multiple raster layers

A raster information HTML file should look like below. A HTML file can be open with any text editor or web browser of your choice. 


```
        Driver: GTiff/GeoTIFF
        Files: /Users/codrinamariailie/Google Drive/02_OK/Gov_Geospatial_Trainings/Data/module9/LandCover2019_3123.tif
        Size is 678, 570
        Coordinate System is:
        PROJCRS["PRS92 / Philippines zone 3",
            BASEGEOGCRS["PRS92",
                DATUM["Philippine Reference System 1992",
                    ELLIPSOID["Clarke 1866",6378206.4,294.978698213898,
                        LENGTHUNIT["metre",1]]],
                PRIMEM["Greenwich",0,
                    ANGLEUNIT["degree",0.0174532925199433]],
                ID["EPSG",4683]],
            CONVERSION["Philippines zone III",
                METHOD["Transverse Mercator",
                    ID["EPSG",9807]],
                PARAMETER["Latitude of natural origin",0,
                    ANGLEUNIT["degree",0.0174532925199433],
                    ID["EPSG",8801]],
                PARAMETER["Longitude of natural origin",121,
                    ANGLEUNIT["degree",0.0174532925199433],
                    ID["EPSG",8802]],
                PARAMETER["Scale factor at natural origin",0.99995,
                    SCALEUNIT["unity",1],
                    ID["EPSG",8805]],
                PARAMETER["False easting",500000,
                    LENGTHUNIT["metre",1],
                    ID["EPSG",8806]],
                PARAMETER["False northing",0,
                    LENGTHUNIT["metre",1],
                    ID["EPSG",8807]]],
            CS[Cartesian,2],
                AXIS["easting (X)",east,
                    ORDER[1],
                    LENGTHUNIT["metre",1]],
                AXIS["northing (Y)",north,
                    ORDER[2],
                    LENGTHUNIT["metre",1]],
            USAGE[
                SCOPE["unknown"],
                AREA["Philippines - zone III"],
                BBOX[3,119.7,21.62,122.21]],
            ID["EPSG",3123]]
        Data axis to CRS axis mapping: 1,2
        Origin = (430713.282723263022490,1690115.897022359305993)
        Pixel Size = (100.000000000000000,-100.000000000000000)
        Metadata:
          AREA_OR_POINT=Area
        Image Structure Metadata:
          INTERLEAVE=PIXEL
        Corner Coordinates:
        Upper Left  (  430713.283, 1690115.897) (120d21'17.68"E, 15d16'55.47"N)
        Lower Left  (  430713.283, 1633115.897) (120d21'23.24"E, 14d46' 0.88"N)
        Upper Right (  498513.283, 1690115.897) (120d59'10.17"E, 15d16'58.81"N)
        Lower Right (  498513.283, 1633115.897) (120d59'10.29"E, 14d46' 4.10"N)
        Center      (  464613.283, 1661615.897) (120d40'15.34"E, 15d 1'30.61"N)
        Band 1 Block=678x4 Type=Byte, ColorInterp=Red
          Description = discrete_classification
            Computed Min/Max=0.000,200.000
          Minimum=0.000, Maximum=200.000, Mean=67.557, StdDev=35.613
          NoData Value=255
          Metadata:
            STATISTICS_MAXIMUM=200
            STATISTICS_MEAN=67.556567003835
            STATISTICS_MINIMUM=0
            STATISTICS_STDDEV=35.612833384649
            STATISTICS_VALID_PERCENT=99.72
        Band 2 Block=678x4 Type=Byte, ColorInterp=Green
          Description = forest_type
            Computed Min/Max=0.000,2.000
          Minimum=0.000, Maximum=2.000, Mean=0.473, StdDev=0.850
          NoData Value=255
          Metadata:
            STATISTICS_MAXIMUM=2
            STATISTICS_MEAN=0.47292184572588
            STATISTICS_MINIMUM=0
            STATISTICS_STDDEV=0.84981681513547
            STATISTICS_VALID_PERCENT=99.72
        Band 3 Block=678x4 Type=Byte, ColorInterp=Blue
          Description = urban-coverfraction
            Computed Min/Max=0.000,100.000
          Minimum=0.000, Maximum=100.000, Mean=14.485, StdDev=30.631
          NoData Value=255
          Metadata:
            STATISTICS_MAXIMUM=100
            STATISTICS_MEAN=14.484993486711
            STATISTICS_MINIMUM=0
            STATISTICS_STDDEV=30.631074729814
            STATISTICS_VALID_PERCENT=99.72
```


After preparing the rasters by reprojecting them into the CRS we are working with and reading their metadata to better understand the files, it is time to delve in the actual data. To achieve that, we will calculate and interpret the histograms (see Breakdown of concepts section for details) of our rasters. 

To calculate a histogram, select the raster layer you are interested in, open by double clicking the `Properties` dialog window and go to `Histogram` (see figure 9.17). 


![Histogram window](media/fig917.png "Histogram window")

Figure 9.17 - Histogram window

Hit the `Compute histogram` button and QIS quill automatically compute it. 

After computing the histogram, we can see that the mouse turns into a loupe. It is a tool that allows inspection of the histogram, seeing how the frequency of different value ranges. Zooming in and you can see something like in figure 9.18. 

To go back to full view, click left. 


![Zooming in on the DSM_mosaic_3123 computed histogram](media/fig918.png "Zooming in on the DSM_mosaic_3123 computed histogram")

Figure 9.18 - Zooming in on the DSM_mosaic_3123 computed histogram

More than just seeing the distribution of the numerical values of the pixels, the histogram allows the user to reclassify the values for visualisation of the raster. To do that use the 2 tools to pinpoint on the histogram the new min and max values (see figure 9.19). 


![Selecting min and max values to reclassify the raster](media/fig919.png "Selecting min and max values to reclassify the raster")

Figure 9.19 - Selecting min and max values to reclassify the raster

After pressing apply, the raster will be represented using the new selected min-max range. This functionality allows the user to ignore extreme values that can stretch ab-normally the raster. 

Even though the next tool we use is a plugin (see module 1 for plugin details), we consider it very useful in starting working with raster. We are referring to the `Value Tool` that allows immediate identification of cell values by hovering over raster layers. 

Go to` Plugin ‣ Manage and Install Plugins` and search for the `Value Tool` plugin and click install. Afterwards, right click on the QGIS main window bar to open all available Panels and Toolbars in your QGIS installation (see figure 9.20). 


![Panels and toolbars availability in QGIS](media/fig920.png "Panels and toolbars availability in QGIS")

Figure 9.20 - Panels and toolbars availability in QGIS 

Select the `Value Tool` panel, then check your QGIS interface to see where it opened, in your case.  As seen in picture 9.20, Value Tool opened in the left downside corner, for me. 

The practicality of this tool resides in its simplicity of use, with just a few clicks, one can very easily extract value cells in the exact areas of interest. Furthermore, it allows this for all loaded raster layers. 

The Value Tool has 3 tabs: Table, Graph, Options (see figure 9.21).


![Loaded value tool - highlight on first tab - Table](media/fig921.png "Loaded value tool - highlight on first tab - Table")

Figure 9.21 - Loaded value tool - highlight on first tab - Table

The first tab - Tabel - presents a list of all loaded raster layers and the values of cells, as the user moves the mouse. There is also the possibility of selecting with how many decimals the values should be displayed. If the mouse is hovered outside a raster layer extent, instead of a value, a message will be displayed: “out of extent”. 

The second tab - Graph - displays in a united graph all values it reads at the position of the mouse. It allows the user to insert values for min and max on the Y axis - that is the axis of cell values. The X axis lists all bands of the raster it displays in the tabel, with the corresponding order numbers: the band that has number 1 in first tab, will also be number 1 in the graph. 

The third tab allows the user to customize what the `Value Tool` displays: what layers (all, only the visible ones or the selected ones) and which bands to show. 


### Quiz questions

1. Can raster layers be reprojected in other coordinate systems?
*   _<span style="text-decoration:underline;">Yes.</span>_
*   _No. _
2. Can there be any gaps between the value ranges of a histogram computed for a raster layer?
*   Yes. 
*   <span style="text-decoration:underline;">No.</span>
3. Can different bands of the same raster dataset have different resolutions? 
*   _Yes._ 
*   No. 


## **Phase 2: Working Intro to working with raster data**

Now that we’ve learned how to extract basic information on the loaded raster datasets, we will continue with a more in-depth raster data processing in order to obtain new derived rasters and, in consequence, more information.

As you may have noticed, due to the raster data model structure, the layers we have loaded are expanding over our region of interest - Pampanga province. That is undesirable due to several reasons but mainly because you end up processing more data than you actually need, which translates in bigger storage and computer processing needs. That is why, before moving forward to any other steps, we will make sure that we process exactly as much data as we need. **Be aware **as you will start working on your own datasets, that the size of your files is an important factor when it comes to processing times. The bigger the files, more time will be required. Because of the model data structure - raster vs vector - raster files are usually much larger. 

As you have noticed by now, the datasets we load into a GIS - in our case into QGIS - can be processed together even if they are of different nature, such as joining csv tables to vector layers to add information to geometries. The same applies to raster and vector data, as we will see. 

To work only with raster layers that are relevant to our Pampanga province, we will use the vector extent layer (Pampanga3123) to cut/clip all relevant raster layers. Go to` Raster ‣ Extraction ‣ Clip Raster by Mask Layer` (see figure 9.22)`.`


![Using a vector mask to extract the raster data on a specific region](media/fig922.png "Using a vector mask to extract the raster data on a specific region")

Figure 9.22 - Using a vector mask to extract the raster data on a specific region

Given that we will work with 7 raster layers - the 5 Land Cover layers - the digital surface model and the HRSLl, we will use Batch processing to clip all layers at once. **Be aware,** if you have skipped the reprojecting step you have layers in different projections and the algorithm will either not work or produce unexpected results. 

Your batch processing window setup should look like in figure 9.23. 


![Batch process cliping all required raster layers by Pampanga Province geometry](media/fig923.png "Batch process cliping all required raster layers by Pampanga Province geometry")

Figure 9.23 - Batch process cliping all required raster layers by Pampanga Province geometry

The parameters setup are the following: mask layer: Pampanga3123, both source and target CRS is EPSG 3123, select yes to: `match the extent of the clipped raster to the mask layer` and `keep resolution of input layer`. Be aware, for the DSM_mosaic we will also select yes` to create an output alpha band`. Load layers at completion. 

If everything went smoothly, your QGIS main window should look like in figure 9.24. 


![Raster layers clipped by Pampanga province contour](media/fig924.png "Raster layers clipped by Pampanga province contour")

Figure 9.24 - Raster layers clipped by Pampanga province contour.  

Now, imagine that you have to present a report on where most people are living but with consideration to the altitude[^4]. You must know how many people live between 0 and 200 m altitude in the Pampanga province. There are a few elements to consider. Firstly, what is the data we will use and what are its characteristics. For population, we have the High Resolution Settlement Layer Data and for relief, we have the ALOS World 3D - 30m (AW3D30). Both raster layers have a spatial resolution of 30m, which allows us to proceed to other considerations. Relief is a continuous phenomena, the spread of the population is not, yet the report would make no sense to be done by the 30m pixel. We need to identify all the pixels with cell values from 0 to 200. Considering the histogram of the DSM_mosaic for our region of interest, we’ve seen that most cell values are between 0 and 200m. We can proceed to making a basic relief map based on the following divisions: 

1. 0 - 50m
2. 51 - 100m
3. 101 - 150m
4. 151 - 200m
5. 250 - 600m
6. 600 - 1300m

Using your knowledge acquired in module 4, you can style the DSM layer by these categories. Your map should look like in figure 9.25.


![DSM_mosaic_clipped representation](media/fig925.png "DSM_mosaic_clipped representation")

Figure 9.25 - DSM_mosaic_clipped representation

In order to calculate the number of people based on the raster data HRSL that live up to 200 meters in Pampanga province, we must see which pixels fall in each of those categories. To do that, we will use `Raster Calculator`. This is a functionality allowing the user to perform calculations on the basis of existing raster pixel values. The results are written to a new raster layer in a GDAL[^5]-supported format.

To open the Raster Calculator go to `Raster ‣ Raster Calculator. `The functionality window should now be on your screen (see figure 9.26). 


![Raster calculator](media/fig926.png "Raster calculator")

Figure 9.26 - Raster calculator

In this window, we can recognize the operations detailed in the Concepts section, substractions, additions, comparisons and all the others (see page 3). Next, we will ‘slice’ our DSM_mosaic_clipped raster layer to extract only the pixels with values up to 200 meters. We know that the value cells of the DSM-mosaic_clipped represent a continuous numerical data (not discrete values, such as LandCover). Therefore, the operation we need to employ in this case is a comparison one - cell values &lt; 200 meters. To obtain this, we will write the following the Raster Calculator: 

`"DSM_mosaic_clipped@1" &lt; 200.` The naming convention for the rasters can be observed: what comes before the @ is the name of the raster layer, what comes after the @ is the number of the band. Save the calculator result as DSM_clipped200.tiff. Your Raster Calculator should look like in figure 9.27. 


![Inserting a formula into the Raster Calculator](media/fig927.png "Inserting a formula into the Raster Calculator")

Figure 9.27 - Inserting a formula into the Raster Calculator. 

Your result should look like in figure 9.28. 


![Result of identify all pixel values that are below 200 meters using the Raster Calculator](media/fig928.png "Result of identify all pixel values that are below 200 meters using the Raster Calculator")

Figure 9.28 - Result of identify all pixel values that are below 200 meters using the Raster Calculator

As we can see in the TOC, the raster layer we have obtained has only 2 values 0 and 1. That is because we have used a rational operation, a comparison, therefore every pixel that is below 200 meters received value = 1 and all above, value = 0. We can test this by using the `Value Tool`. Figure 9.29 presents only pixels of value 1, in other words the pixels we are interested in for our exercise. 


![Spatial distribution of all pixels of value 1, meaning with altitude lower than 200 meters](media/fig929.png "Spatial distribution of all pixels of value 1, meaning with altitude lower than 200 meters")

Figure 9.29 - Spatial distribution of all pixels of value 1, meaning with altitude lower than 200 meters 

Going further, we can show the spatial distribution of population at the 30 m spatial resolution only in this specific geographical region, we’ve selected - Pampanga province, below 200m. To do that, we again employ Raster Calculator. 

The formula is fairly simple, given that all DSM cell values we are interested in have value 1. 

Open the Calculator and insert the following formula: `"DSM_clipped200@1"*"hsrl_clipped@1"`


![Using raster calculator to identify population distribution classes based on altitude of up to 200m](media/fig930.png "Using raster calculator to identify population distribution classes based on altitude of up to 200m")

Figure 9.30 - Using raster calculator to identify population distribution classes based on altitude of up to 200m

As opposed to previous raster calculator use, we have used 2 different raster datasets to obtain the desired result, yet you will observe that even if there are pixels that fall outside the DMS_clipped200.tif in the result, their value is 0. Use Value Tool to check (see figure 9.31). 


![Using Value Tool to check results of Raster Calculator](media/fig931.png "Using Value Tool to check results of Raster Calculator")

Figure 9.31 - Using Value Tool to check results of Raster Calculator

You can see that even if hrsl_clipped has values in this specific mouse location, the raster obtained with Raster Calculator hrsl_dsm_clipped has value 0. 

Next, we present the spatial distribution of the population that lives below 200m in Pampanga province. To choose an appropriate classification, we calculate the histogram. We can notice that most values are between 0.1 and 200 people per 30m. The classification we’ve chosen is visible in figure 9.32. 


![Distribution of population that lives below 200m in Pampanga province, represented at a 30m resolution](media/fig932.png "Distribution of population that lives below 200m in Pampanga province, represented at a 30m resolution")

Figure 9.32 - Distribution of population that lives below 200m in Pampanga province, represented at a 30m resolution. 

If we are interested in the total number of people living below 200m in Pampanga province and not the geographical distribution per 30 m spatial resolution, then we need to sum up all pixel values of the raster layer hrsl_dsm_clipped. One way to obtain this number is to transform the DSM_clipped200 from raster to vector and them [....]

To do that go to `Raster ‣ Conversion ‣ Polygonize (Raster to Vector) `(see figure 9.33). 


![Raster to vector conversion](media/fig933.png "Raster to vector conversion")

Figure 9.33 - Raster to vector conversion

Remember that this raster layer had only 2 values - 0 and 1, so choose as the parameter by which to construct the vector the DN (digital number). Save the result as DSM_clipped200.geojson. Your result should look like in figure 9.34. 


![Result of converting a raster dataset to a vector dataset](media/fig934.png "Result of converting a raster dataset to a vector dataset")

Figure 9.34 -  Result of converting a raster dataset to a vector dataset. 

Delete the geometry of value 0. 

To find our answer we will use `Zonal Statistics`. To quickly find this functionality, open the Processing Toolbox and type in the search box “zonal” (see figure 9.35).


![Identifying Zonal Statistics in the Processing Toolbox](media/fig935.png "Identifying Zonal Statistics in the Processing Toolbox")

Figure 9.35 - Identifying Zonal Statistics in the Processing Toolbox

In the window that has opened, select the parameters like in figure 9.36. As statistics calculated, select: count, sum, min and max. 


![Setting the parameters for Zonal Statistics](media/fig936.png "Setting the parameters for Zonal Statistics")

Figure 9.36 - Setting the parameters for Zonal Statistics

The resulting layer is a vector layer that has as attributes the statistics that we have selected (see figure 9.37). 


![Resulting vector layer of Zonal Statistics](media/fig937.png "Resulting vector layer of Zonal Statistics")

Figure 9.37 - Resulting vector layer of Zonal Statistics

And with this final step, we answered our exercise, how many people (and where) are living below 200m in Pampanga province. 


### Quiz questions 

1. Can raster data be clipped? 
*   _<span style="text-decoration:underline;">Yes</span>. _
*   _No._
2. Can one use vector datasets loaded in the QGIS project in Raster Calculator?
*   _Yes. _
*   _<span style="text-decoration:underline;">No.</span>_
3. Can raster datasets be converted to vector datasets?
*   _<span style="text-decoration:underline;">Yes</span>. _
*   _No._


## **Phase 3: Working with raster and vector data.**

*   Resampling HRSL to LandCover dimension - 30m to 100m
*   Change detection exercise for land cover


# References:

Center for International Earth Science Information Network - CIESIN - Columbia University. 2018. Gridded Population of the World, Version 4 (GPWv4): Population Density, Revision 11. Palisades, NY: NASA Socioeconomic Data and Applications Center (SEDAC). [https://doi.org/10.7927/H49C6VHW](https://doi.org/10.7927/H49C6VHW).

Resampling methods: [https://gisgeography.com/raster-resampling/](https://gisgeography.com/raster-resampling/)


<!-- Footnotes themselves at the bottom. -->
## Notes

[^1]: A primitive operation is a basic computation performed by an algorithm.  

[^2]: The temporal resolution depends on latitude. 

[^3]: JAXA is the Japan Aerospace Exploration Agency 

[^4]: For the sake of this exercise we will consider the DSM as a digital elevation model. For more details on the differences please see the Breakdown of concepts section (page

[^5]: The Geospatial Data Abstraction Library (GDAL) is a computer software library for reading and writing raster and vector geospatial data formats. 
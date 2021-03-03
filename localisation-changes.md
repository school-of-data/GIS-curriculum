**LIST OF CHANGES FOR LOCALISATION OF MODULES**

# TIPS
* Utilize Search and Replace
    * Search and replace *Pampanga province* with the name of your area of interest (e.g. for Sri Lanka, I replaced *Pampanga province* with *Colombo district*)
    * Search and replace *Philippines* with the name of your country of interest (e.g. for Sri Lanka, I replaced *Philippines* with *Sri Lanka*)

# Module 0

## media
* **true-size-of.png** -> replace with screenshot showing the country
* **spatial-model.png** -> replace with screenshot showing the country
* **vector.png** -> replace with screenshot showing a country vector file (geometry and attribute table)

## module0
* **line 268 and 269** -> replace with common CRS used in the country


# Module 1

## media
* **change-theme.png** -> replace with screenshot of local/translated QGIS (if available)
* **ex01-01.png** -> replace with screenshot of local/translated QGIS (if available)
* **ex01-02.png** -> replace with screenshot of local/translated QGIS (if available)
* **ex01-03.png** -> replace with screenshot of local/translated QGIS (if available)
* **manage-and-install-plugins-dialog.png** -> replace with screenshot of local/translated QGIS (if available)
* **manage-and-install-plugins-dialog-2.png** -> replace with screenshot of local/translated QGIS (if available)
* **memory-layer-saver-plugin.png** -> replace with screenshot of local/translated QGIS (if available)
* **plugins-menu.png** -> replace with screenshot of local/translated QGIS (if available)
* **plugins-menu-2.png** -> replace with screenshot of local/translated QGIS (if available)
* **qgis-interface.png** -> replace with screenshot of local/translated QGIS (if available)
* **qgis-interface-custom.png** -> replace with screenshot of local/translated QGIS (if available)
* **qgis-interface-parts.png** -> replace with screenshot of local/translated QGIS (if available)
* **quickosm-plugin.png** -> replace with screenshot of local/translated QGIS (if available)
* **settings-1.png** -> replace with screenshot of local/translated QGIS (if available)
* **settings-2.png** -> replace with screenshot of local/translated QGIS (if available)
* **user-profiles-1.png** -> replace with screenshot of local/translated QGIS (if available)
* **user-profiles-2.png** -> replace with screenshot of local/translated QGIS (if available)
* **user-profiles-3.png** -> replace with screenshot of local/translated QGIS (if available)


# Module 2

## data
* ***.shp** -> use shapefile of province or country 
* ***.geojson** -> use geojson admin boundary 1 level higher than the shapefile (i.e. if shapefile is level 0, geojson should be level 1)
* ***.fgb** -> use flatgeobuf admin boundary 1 level (2 levels) higher than the geojson (shapefile) (i.e. if the shapefile is level 0, the flatgeobuf should be level 2)
* ***.gpkg** -> Geopapackage containing a DEM and a point vector.
    * ***_SRTM_DEM**
        1. Same extent as the shapefile.
        2. Can be generated using the **SRTM Downloader** plugin, merging the loaded rasters, and clipping the resulting merged raster using the shapefile polygon/mask.
        3. Save the output of step 2 in a geopackage.
    * ***_hospitals**
        1. This can be generated using the **QuickOSM plugin** with key: amenity and value: hospital. Get points only.
        2. Save the loaded layer into the same geopackage as the DEM.
* ***_schools.csv** -> CSV file of school locations.
    1. This can be generated using the **QuickOSM plugin** with key: amenity and value: schools. get points only. 
    2. Add the X/Y field to the generated vector file using the **Add X/Y fields to layer** algorithm.
    3. Save the output of step 2 as a CSV file.

## media
* **data-source-manager-csv.png** -> replace with screenshot using the localised data
* **data-source-manager-raster.png** -> replace with screenshot using the localised data
* **data-source-manager-vector.png** -> replace with screenshot using the localised data
* **layer-properties.png** -> replace with screenshot using the localised data
* **layer-panel-1.png** -> replace with screenshot using the localised data
* **layer-panel-2.png** -> replace with screenshot using the localised data
* **map-canvas-1.png** -> replace with screenshot using the localised data
* **metadata-1.png** -> replace with screenshot using the localised data
* **metadata-2.png** -> replace with screenshot using the localised data
* **metadata-3.png** -> replace with screenshot using the localised data
* **qgis-browser-2.png** -> replace with screenshot using the localised data
* **qgis-browser-3.png** -> replace with screenshot using the localised data
* **qgis-browser-layer-properties.png** -> replace with screenshot using the localised data
* **vector-layers-loaded-1.png** -> replace with screenshot using the localised data
* **xyz-3.png** -> replace with screenshot using the localised data

## module2
* **line 157 to 163** -> replace names of files (e.g. NCR_admin_boundary to LKA_admin_boundary)
* **line 182** -> replace names of files
* **line 260, 263, 265** -> replace name fo files
* **line 308, 311** -> replace name of files
* **line 321, 324** -> replace name of files
* **line 342, 345** -> replace name of files
* **line 398-399, 407, 411, 417** -> replace with sample of local tile server (XYZ), if not available, use ESRI World Imagery (see [Sri Lanka example](sri-lanka/module2/module2.md), lines 398-417)
* **line 449-450, 458, 460, 462, 466, 468** -> replace with sample of local WMS server, if not available, use GeoServer Demo (see [Sri Lanka example](sri-lanka/module2/module2.md), lines 438-459)


# Module 3

## data
* **module3.gpkg** -> replace content of geopackage with admin boundary of 1 large (e.g. province/district) and 1 small (e.g. city/division) admin boundary
* **HRSL_*_Population.tif** -> High Resolution Settlement Layer raster data covering the larger admin area
    -> can be found at https://data.humdata.org/search?organization=facebook&q=%22High%20Resolution%20Population%20Density%20Maps%20%2B%20Demographic%20Estimates%22

## media
* **hrsl-1.png** -> replace with screenshot using the localised data
* **osm.png** -> replace with screenshot showing the country on OSM
* **overpass-1.png** -> replace with screenshot using the localised data
* **overpass-2.png** -> replace with screenshot using the localised data
* **overpass-3.png** -> replace with screenshot using the localised data
* **quickosm-1.png** -> replace with screenshot using the localised data
* **quickosm-2.png** -> replace with screenshot using the localised data
* **quickosm-3.png** -> replace with screenshot using the localised data
* **quickosm-4.png** -> replace with screenshot using the localised data
* **quickosm-5.png** -> replace with screenshot using the localised data
* **quickosm-6.png** -> replace with screenshot using the localised data
* **quickosm-7.png** -> replace with screenshot using the localised data


## module3
* **line 26** -> replace name of layers
* **line 105, 107, 109** -> replace name of layers 
* **line 134, 138, 142, 144** -> replace name of layers
* **line 159, 163, 167, 169** -> replace name of layers 
* **line 232, 234, 236** -> replace name of layers
* **line 254** -> replace name of layer 
* **line 268, 270, 272, 274, 276, 278** -> check if the overpass query returns a layer. if not, replace with a different query (e.g. use a different fast food name).


# Module 4

## data
* **module4.gpkg** -> same content with module3.gpkg + a clinics layer
    * clinics layer can be generated using QuickOSM with parameters key: amenity, value: clinic
* **HRSL_*_Population.tif** -> High Resolution Settlement Layer raster data covering the larger admin boundary layer (same as module 3)

## media
* **blur-effect.png** -> replace with screenshot using localised data
* **blurry-result.png** -> replace with screenshot using localised data
* **centroid.png** -> replace with screenshot using localised data
* **centroid-result.png** -> replace with screenshot using localised data
* **default-vector-render.png** -> replace with screenshot using localised data
* **draw-effects.png** -> replace with screenshot using localised data
* **drop-shadow-result.png** -> replace with screenshot using localised data
* **final-vector-render.png** -> replace with screenshot using localised data
* **hrsl-style.png** -> replace with screenshot using localised data
    * color ramp is viridis, inverted, quantile, 5 classes
* **initial-workspace.png** -> replace with screenshot using localised data
* **layer-styling.png** -> replace with screenshot using localised data
* **new-effects-dialog** -> replace with screenshot using localised data
* **no-fill-render.png** -> replace with screenshot using localised data
* **qgis9.png** -> replace with screenshot using localised data
* **vector-style.png** -> replace with screenshot using localised data
* **zoom-in.png** -> replace with screenshot using localised data

## module4
* **line 20, 21, 22** -> replace name of layers (e.g. Pampanga -> Colombo)


# Module 5

## data
* **module5.gpkg** -> same content with module4.gpkg + province/district admin layer vector
* **HRSL_*_Population.tif** -> High Resolution Settlement Layer raster data covering the province/district of interest boundary layer (same as module 3 and 4)

## media
* **atlas-attr.png** -> replace with screenshot using localised data 
* **atlas-controlled.png** -> replace with screenshot using localised data 
* **atlas-coverage.png** -> replace with screenshot using localised data 
* **atlas-outputs.png** -> replace with screenshot using localised data 
* **atlas-preview.png** -> replace with screenshot using localised data 
* **atlas-print-layout.png** -> replace with screenshot using localised data 
* **atlas-toolbar-nav.png** -> replace with screenshot using localised data 
* **attribution.png** -> replace with screenshot using localised data 
* **controlled_by_atlas.png** -> replace with screenshot using localised data 
* **coverage-layer.png** -> replace with screenshot using localised data 
* **exported-map.png** -> replace with screenshot using localised data 
* **exported-map-canvas.png** -> replace with screenshot using localised data 
* **export-map-canvas.png** -> replace with screenshot using localised data 
* **export-map-canvas-image.png** -> replace with screenshot using localised data 
* **generate-atlas.png** -> replace with screenshot using localised data 
* **img-parameters.png** -> replace with screenshot using localised data 
* **legend.png** -> replace with screenshot using localised data 
* **legend_scalebar_added.png** -> replace with screenshot using localised data 
* **newprint_composer.png** -> replace with screenshot using localised data 
* **new-print-layout.png** -> replace with screenshot using localised data 
* **new-print-layout-name.png** -> replace with screenshot using localised data 
* **new-print-layout-window.png** -> replace with screenshot using localised data 
* **print_comp2.png** -> replace with screenshot using localised data 
* **print-layout-map.png** -> replace with screenshot using localised data 
* **print-layout-with-title.png** -> replace with screenshot using localised data 
* **scale-bar.png** -> replace with screenshot using localised data 

## module5
* **line 26-30** -> replace name of files
* **line 49** -> replace name of area and country
* **line 91** -> replace name of area and country
* **line 198** -> replace name of area and country
* **line 208** -> replace number of maps to be generated
* **line 223** -> replace number of maps/areas (e.g. 81 provinces -> 25 districts)
* **line 235** -> replace number of maps to be generated
* **line 241** -> replace number of maps to be generated
* **line 248** -> replace kind of area (e.g. provinces -> districts)


# Module 6

## data
* **module6.gpkg** -> same as module 5.gpkg
* **HRSL_*_Population.tif** -> High Resolution Settlement Layer raster data covering the province/district of interest boundary layer (same as module 3, 4, and 5)

## media
* **add-layers.png** -> replace with screenshot using localised data 
* **area.png** -> replace with screenshot using localised data 
* **attribute-tab.png** -> replace with screenshot using localised data 
* **dock-attr-btn.png** -> replace with screenshot using localised data 
* **docked-attribute-tab.png** -> replace with screenshot using localised data 
* **field_calculator.png** -> replace with screenshot using localised data 
* **gen-settings.png** -> replace with screenshot using localised data 
* **many-polygons.png** -> replace with screenshot using localised data
* **select.png** -> replace with screenshot using localised data 
* **selected-attr.png** -> replace with screenshot using localised data 
* **selected-canvas.png** -> replace with screenshot using localised data

## module6
* **line 29-32** -> replace name of files
* **line 113** -> replace name of area and country
* **line 133** -> replace name of country and CRS
* **line 180** -> replace name of area
* **line 184-187** -> replace name of files
* **line 196, 199** -> replace if needed (e.g. current expression is invalid or does not return results)
* **line 205** -> replace number of selected clinics based on result of query


# Module 7

## data
* **(topo map or any map of the country to be georeferenced)**

## media
* **digitize-1.png** -> replace with screenshot using localised data
* **digitize-2.png** -> replace with screenshot using localised data
* **digitize-3.png** -> replace with screenshot using localised data
* **digitize-zoom.png** -> replace with screenshot using localised data
* **georef-1.png** -> replace with screenshot using localised data
* **georef-2.png** -> replace with screenshot using localised data
* **georef-3.png** -> replace with screenshot using localised data
* **georef-4.png** -> replace with screenshot using localised data
* **georef-5.png** -> replace with screenshot using localised data
* **georeferencer.png** -> replace with screenshot using localised data
* **new-geopackage-dialog.png** -> replace with screenshot using localised data
* **new-shapefile-dialog.png** -> replace with screenshot using localised data
* **transformation-settings.png** -> replace with screenshot using localised data
* **xyz-1.png** -> replace with screenshot using localised data
* **xyz-2.png** -> replace with screenshot using localised data
* **xyz-3.png** -> replace with screenshot using localised data

## module7
* **line 14** -> replace with file to be georeferenced
* **line 254** -> replace name of map image file to that of the file to be georeferenced


# Module 8

## data
* **module8.gpkg** -> contains the following OSM layers downloaded from GeoFabrik, clipped to the province/district/state of interest, and projected to a projected CRS used by the country. For example, for the Philippines, layers are clipped to the province of Pampanga with EPSG 3123. For Sri Lanka, the district of Colombo is used with EPSG 5235.
   * pois (point)
   * pofw (point)
   * road (line)
   * waterways (line)
   * buildings (polygon)
   * landuse (polygon)

**NOTE:** There's a possibility that module8.gpkg can exceed the 100MB single file size limit when pushing to GitHub. If this is the case, just put a text file inside the data folder with a link to where the data can be found or save the individual layers as shapefiles (or other vector formats) or save the layers into separate geopackages if these individual files will be less than 100MB.

## media
* **fig81.png** -> replace with screenshot showing OSM routing using local places
* **fig85.png** -> replace with screenshot using localised data
* **fig86.png** -> replace with screenshot using localised data
* **fig87.png** -> replace with screenshot using localised data
* **fig88.png** -> replace with screenshot using localised data
* **fig810.png** -> replace with screenshot using localised data
* **fig811.png** -> replace with screenshot using localised data
* **fig812.png** -> replace with screenshot using localised data
* **fig813.png** -> replace with screenshot using localised data
* **fig814.png** -> replace with screenshot using localised data
* **fig815.png** -> replace with screenshot using localised data
* **fig816.png** -> replace with screenshot using localised data
* **fig817_b.png** -> replace with screenshot using localised data
* **fig818_a.png** -> replace with screenshot using localised data
* **fig818_b.png** -> replace with screenshot using localised data
* **fig818_c.png** -> replace with screenshot using localised data
* **fig819_a.png** -> replace with screenshot using localised data
* **fig819_b.png** -> replace with screenshot using localised data
* **fig820_a.png** -> replace with screenshot using localised data
* **fig821.png** -> replace with screenshot using localised data
* **fig822.png** -> replace with screenshot using localised data
* **fig824.png** -> replace with screenshot using localised data
* **fig825.png** -> replace with screenshot using localised data
* **fig826_b.png** -> replace with screenshot using localised data
* **fig827_b.png** -> replace with screenshot using localised data
* **fig828_a.png** -> replace with screenshot using localised data
* **fig828_b.png** -> replace with screenshot using localised data
* **fig828_d.png** -> replace with screenshot using localised data
* **fig829_b.png** -> replace with screenshot using localised data
* **fig830_b.png** -> replace with screenshot using localised data
* **fig832.png** -> replace with screenshot using localised data
* **fig833.png** -> replace with screenshot using localised data
* **fig834_b.png** -> replace with screenshot using localised data
* **fig834_c.png** -> replace with screenshot using localised data
* **fig834_e.png** -> replace with screenshot using localised data
* **fig835_a.png** -> replace with screenshot using localised data
* **fig835_b.png** -> replace with screenshot using localised data
* **fig836_a.png** -> replace with screenshot using localised data
* **fig836_b.png** -> replace with screenshot using localised data
* **fig837_b.png** -> replace with screenshot using localised data
* **fig837_d.png** -> replace with screenshot using localised data
* **fig837_e.png** -> replace with screenshot using localised data
* **fig838_b.png** -> replace with screenshot using localised data
* **fig838_c.png** -> replace with screenshot using localised data
* **fig839.png** -> replace with screenshot using localised data
* **fig840_a.png** -> replace with screenshot using localised data
* **fig840_b.png** -> replace with screenshot using localised data
* **fig840_c.png** -> replace with screenshot using localised data
* **fig840_d.png** -> replace with screenshot using localised data
* **fig841.png** -> replace with screenshot using localised data
* **fig842.png** -> replace with screenshot using localised data
* **fig843.png** -> replace with screenshot using localised data
* **fig844.png** -> replace with screenshot using localised data
* **fig845.png** -> replace with screenshot using localised data
* **fig846.png** -> replace with screenshot using localised data
* **fig847.png** -> replace with screenshot using localised data
* **fig849.png** -> replace with screenshot using localised data
* **fig850.png** -> replace with screenshot using localised data

## module8
* **line 36** -> replace with coordinate reference system used in the country (e.g. *PRS92 / Philippines zone 3, EPSG 3123* becomes *SLD 99 / Sri Lanka Grid 1999, EPSG 5235*)
* **line 59** -> replace area with local places (e.g. *Angeles, Pampanga, Philippines* becomes *Colombo, Sri Lanka*) 
* **lines 135, 150, 169** -> replace with local EPSG code used (e.g. *3123* becomes *5235*)
* **lines 201-221, 227-236** -> replace with output of Basic Statistics of Field algorithm using localised data
* **line 239** -> replace with outputs of Basic Statistics of Field algorithm using localised data (e.g. *827657* becomes *158500*)
* **line 287, 377, 563, 596, 601, 603, 608, 610, 618, 620, 623, 625, 666, 855, 859, 878, 898, 900, 923, 929** -> replace name of area with local area of interest (e.g. *Pampanga* becomes *Colombo*, *province* becomes *district*) 
* **line 328** -> replace number of features with output from localized data (e.g. *2727* becomes *394*) 
* **line 414-457** -> replace with outputs of List unique values algorithm using localized data 
* **line 484** -> replace name of area (*Pampanga* to *Colombo*) and values based on GroupStats computation (*3270 buildings* to *303 buildings*) 
* **line 788 - 813** -> depending on the POI dataset, replace the fclass to be queried. If public buildings fclasses exist in the data (e.g. town_hall, hospital, etc.), no need to replace type of POI. If not, as with Sri Lanka which has different fclasses on the POI layer, replace with the appropriate POI class. In the case of Sri Lanka, I used towns and cities instead (Philippines uses public buildings POI classes like hospitals, schools, etc.). 


# Module 9

## Downloading data for Module 9
- For the SRTM DEM, you can use the SRTM Downloader plugin in QGIS and download the tiles covering your area of choice. Save the downloaded layers as TIFF files.
- For the Copernicus Global Land Cover layers, the easiest way to download is to use Google Earth Engine.
    1. Get the extent of your Area of Interest (AOI)
    2. Use the following script to download the LC data from 2015 to 2019 (the script below does 1 download per run, feel free to modify it to run as a loop)

    ```javascript
    // Select geometry to extract PROBA-V Landcover data
    // Replace the vertices with the vertices of the extent of your area
    var geometry = ee.Geometry.Polygon([ [ [ 79.8397728261881383, 6.7136763269970103 ], [ 80.2238350772961866, 6.7136763269970103 ], [ 80.2238350772961866, 6.9797629738920230 ], [ 79.8397728261881383, 6.9797629738920230 ], [ 79.8397728261881383, 6.7136763269970103 ]]]);

    // Location
    var area = ee.FeatureCollection(geometry);
    // Set study area as map center.

    Map.centerObject(area);

    // Select dataset from the Copernicus Landcover Proba-V
    // Just replace the year at the end of the URL (e.g. replace Global/2015 to Global/2016 to download the 2016 data)
    var landcover = ee.Image("COPERNICUS/Landcover/100m/Proba-V-C3/Global/2015").select('discrete_classification','forest_type','urban-coverfraction').clip(area);

    // Check the console for the result of the data selection
    print (landcover);

    // Add dataset to the map
    Map.addLayer(landcover, {}, "Land Cover");

    // Export files as cloud-optimized GeoTIFFs.
    Export.image.toDrive({
    image: landcover, 
    description: 'LandCover_2015', 
    scale: 30, 
    region: area, 
    maxPixels: 1e10, 
    fileFormat: 'GeoTIFF', 
    formatOptions: {cloudOptimized: true}
    });
    ```

## data
* **module9.gpkg** - contains admin boundary of Area of Interest (e.g. Pampanga province, Colombo district)
* **SRTM_DEM** - folder contains the SRTM DEM layers (.tiff)
* **Dynamic_Land_Cover_Map** - folder contains the Copernicus Land Cover maps downloaded using the GEE script above
* **HRSL_area_Population.tif** - HRSL of the Area of Interest

## media
* **fig96.png** -> replace with screenshot using localised data
* **fig97.png** -> replace with screenshot using localised data
* **fig98.png** -> replace with screenshot using localised data
* **fig99_a.png** -> replace with screenshot using localised data
* **fig99_b.png** -> replace with screenshot using localised data
* **fig912.png** -> replace with screenshot using localised data
* **fig913_a.png** -> replace with screenshot using localised data
* **fig913_b.png** -> replace with screenshot using localised data
* **fig913_c.png** -> replace with screenshot using localised data
* **fig914.png** -> replace with screenshot using localised data
* **fig915_a.png** -> replace with screenshot using localised data
* **fig915_b.png** -> replace with screenshot using localised data
* **fig915_c.png** -> replace with screenshot using localised data
* **fig915_d.png** -> replace with screenshot using localised data
* **fig916.png** -> replace with screenshot using localised data
* **fig917.png** -> replace with screenshot using localised data
* **fig918.png** -> replace with screenshot using localised data
* **fig919.png** -> replace with screenshot using localised data
* **fig920.png** -> replace with screenshot using localised data
* **fig921.png** -> replace with screenshot using localised data
* **fig922.png** -> replace with screenshot using localised data
* **fig923.png** -> replace with screenshot using localised data
* **fig924.png** -> replace with screenshot using localised data
* **fig925.png** -> replace with screenshot using localised data
* **fig926_a.png** -> replace with screenshot using localised data
* **fig926_b.png** -> replace with screenshot using localised data
* **fig927.png** -> replace with screenshot using localised data
* **fig928.png** -> replace with screenshot using localised data
* **fig929.png** -> replace with screenshot using localised data
* **fig930.png** -> replace with screenshot using localised data
* **fig931.png** -> replace with screenshot using localised data
* **fig932.png** -> replace with screenshot using localised data
* **fig933_a.png** -> replace with screenshot using localised data
* **fig933_b.png** -> replace with screenshot using localised data
* **fig934.png** -> replace with screenshot using localised data
* **fig935.png** -> replace with screenshot using localised data
* **fig936.png** -> replace with screenshot using localised data
* **fig937.png** -> replace with screenshot using localised data
* **fig939.png** -> replace with screenshot using localised data
* **fig940.png** -> replace with screenshot using localised data
* **fig941.png** -> replace with screenshot using localised data
* **fig942.png** -> replace with screenshot using localised data
* **fig943.png** -> replace with screenshot using localised data
* **fig944.png** -> replace with screenshot using localised data
* **fig945.png** -> replace with screenshot using localised data
* **fig946_a.png** -> replace with screenshot using localised data
* **fig946_b.png** -> replace with screenshot using localised data
* **fig947.png** -> replace with screenshot using localised data
* **fig948_a.png** -> replace with screenshot using localised data
* **fig948_b.png** -> replace with screenshot using localised data
* **fig948_c.png** -> replace with screenshot using localised data
* **fig949.png** -> replace with screenshot using localised data
* **fig950_a.png** -> replace with screenshot using localised data
* **fig950_b.png** -> replace with screenshot using localised data
* **fig951.png** -> replace with screenshot using localised data
* **fig952.png** -> replace with screenshot using localised data
* **fig953_a.png** -> replace with screenshot using localised data
* **fig953_b.png** -> replace with screenshot using localised data
* **fig954.png** -> replace with screenshot using localised data
* **fig955.png** -> replace with screenshot using localised data
* **fig956.png** -> replace with screenshot using localised data
* **fig957.png** -> replace with screenshot using localised data
* **fig958.png** -> replace with screenshot using localised data
* **fig959.png** -> replace with screenshot using localised data
* **fig960.png** -> replace with screenshot using localised data
* **fig961.png** -> replace with screenshot using localised data
* **fig962.png** -> replace with screenshot using localised data

## module9
* **line 25, 26, 29, 394, 408, 412, 437, 708, 712, 724, 726, 729, 737, 739, 741, 757, 800, 807, 822, 824, 827, 829, 831, 877, 895, 911, 929, 963, 1024, 1068, 1087** -> replace name of area with local area of interest (e.g. *Pampanga* becomes *Colombo*, *province* becomes *district*)  
* **line 545** -> replace with output of raster information algorithm
* **line 29, 408, 421, 476, 523, 527, 653, 655, 730, 969, 1075** -> replace with coordinate reference system used in the country (e.g. *PRS92 / Philippines zone 3, EPSG 3123* becomes *SLD 99 / Sri Lanka Grid 1999, EPSG 5235*)



# Module 10

## data


## media


## module9



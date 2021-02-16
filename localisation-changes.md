**LIST OF CHANGES FOR LOCALISATION OF MODULES**

# Module 0

## media
* **true-size-of.png** -> replace with screenshot showing the country
* **spatial-model.png** -> replace with screenshot showing the country
* **vector.png** -> replace with screenshot showing a country vector file (geometry and attribute table)

## module0
* **line 268 and 269** -> replace with common CRS used in the country


# Module 1
None


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
* **HRSL_*_Population.tif** -> High Resolution Settlement Layer raster data covering the larger admin area (same as module 3)

## media
* **media/blur-effect.png** -> replace with screenshot using localised data
* **media/blurry-result.png** -> replace with screenshot using localised data
* **media/centroid.png** -> replace with screenshot using localised data
* **media/centroid-result.png** -> replace with screenshot using localised data
* **media/default-vector-render.png** -> replace with screenshot using localised data
* **media/draw-effects.png** -> replace with screenshot using localised data
* **media/drop-shadow-result.png** -> replace with screenshot using localised data
* **media/final-vector-render.png** -> replace with screenshot using localised data
* **media/hrsl-style.png** -> replace with screenshot using localised data
* **media/initial-workspace.png** -> replace with screenshot using localised data
* **media/layer-styling.png** -> replace with screenshot using localised data
* **media/new-effects-dialog** -> replace with screenshot using localised data
* **media/no-fill-render.png** -> replace with screenshot using localised data
* **media/qgis9.png** -> replace with screenshot using localised data
* **media/vector-style.png** -> replace with screenshot using localised data
* **media/zoom-in.png** -> replace with screenshot using localised data

## module4
* **line 20, 21, 22** -> replace name of layers (e.g. Pampanga -> Colombo)


# Module 5

## data


## media


## module5



# Module 6

## data


## media


## module6



# Module 7

## data


## media


## module7



# Module 8

## data


## media


## module8



# Module 9

## data


## media


## module9
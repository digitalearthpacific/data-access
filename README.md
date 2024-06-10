# Digital Earth Pacific (DEP) Data Access Documentation


<!-- ![image info](./images/dep.png) -->

<div align="center">
  <img src="images/dep.png" />
</div>

Documentation of Digital Earth Pacific data organisation and access mechanisms via AWS Open Data Program

## Data Organisation

Digital Earth Pacific's earth observation derived products are made accessible via the following integration services :

- **Spatial Temporal Asset Catalog (STAC)** specification was designed to establish a standard, unified language to talk about geospatial data, allowing it to more easily searchable and queryable. An overarching goal in having this common standard is to eliminate the need to puruse through APIs of many satellite providers in order to access all the needed data.

- **OGC Webservices (WMS, WFS, WCS)** defines web service standards for accessing and utilizing geospatial data online. These standards, known as OGC Web Services (OWS), ensure interoperability between different software and platforms. 

| Product Type                    | Data Format | Service        |
|---------------------------------|-------------|----------------|
| Cloud Optimised Geotiffs (COGs) | Raster      | STAC, WMS, WCS |
| Coastlines Multi-year PolyLines | Vector      | WFS, WMS       |

### STAC Data Description ###

STAC item records for the following COG products are available @ https://stac-browser.dep.datacube.world

The includes data descriptions for the following DEP products:

| Product | Temporal Scale |
|---------|----------------|
|Water Observations from Space (WoFS)|2013-2021|
|Mangroves Extent and Density|2017-202|
|Sentinel-2 GeoMAD|2017-2023|
|LandSat GeoMAD|?|
|Sentinel 1 Cloudless Mosaics|2017-2023|

The DEP Coastlines Product from 2000-2023 is available via WFS and WMS services via https://dep-geoserver.westeurope.cloudapp.azure.com



https://stac.dep.datacube.world/api.html

https://stac.dep.datacube.world/api

## Data Access Tutorials

- Jupyter Notebook and PySTAC-Client
- OGC Web Services (GeoServer)
- QGIS STAC Plugin

### Coastlines

https://dep-public-test.s3.us-west-2.amazonaws.com/coastlines_0-7-0-47_3832.gpkg


### Water Observations from Space

### Mangroves

### GeoMADs

### Sentinel-1 Annual Mosaics

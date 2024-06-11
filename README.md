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
| Coastlines Multi-Year PolyLines | Vector      | WFS, WMS       |

### Data Descriptions ###

>The data service URLs in this document will change in the near future, please refer back here for updated links and information.

STAC item records for the following COG products are available at [DEP STAC Catalog Browser](https://stac-browser.dep.datacube.world).

The includes data descriptions for the following DEP products:

| Product | Temporal Scale |
|---------|----------------|
|Water Observations from Space (WoFS)|2013-2021|
|Mangroves Extent and Density|2017-202|
|Sentinel-2 GeoMAD|2017-2023|
|LandSat GeoMAD|?|
|Sentinel 1 Cloudless Mosaics|2017-2023|

The DEP Coastlines Product from 2000-2023 is available via WFS and WMS services via [DEP GeoServer](https://dep-geoserver.westeurope.cloudapp.azure.com).

## Data Access Tutorials

### Jupyter, Python and PySTAC-Client

STAC data items can be queried, visualised and/or downloaded using PySTAC-Client API within the [DEP Analytical Hub](https://hub.dep.datacube.world/) or local Python/Jupyter environment.

The full STAC API for Digital Earth Pacific is documentated at [DEP STAC API](https://stac.dep.datacube.world/api.html).

Below is an example for querying, plotting and downloading DEP Managroves Extent and Density product at a particular area of interest across all years.

```
from pystac_client import Client
from odc.stac import load
import xarray as xr
import numpy as np
import odc.geo 

catalog = "https://stac.dep.datacube.world/api"
collection = "dep_s2_mangroves" # collection_name

# Define Coordinates
lower_left = (-10.590125, 149.844629)
upper_right = (-10.360110, 150.195631)

bbox = (lower_left[1], lower_left[0], upper_right[1], upper_right[0])

# Find STAC Items
client = Client.open(catalog)
items = client.search(collections=[collection], bbox=bbox).items()
items = [i for i in items]
print(f"Found {len(items)} items")

# Load STAC Items
config = {
    collection: {
        "assets": {
            "mangroves": {"data_type": "int16"}
        }
    }
}
data = load(items, bbox=bbox, bands=["mangroves"], stac_cfg=config)

# Plot Mangroves
data.mangroves.plot.imshow(
    col="time",
    col_wrap=4,
    levels=[0, 1, 2, 3],
    colors=["white", "yellow", "green", "darkgreen"],
)

# Save Mangroves as COG Tiles
for idx, x in enumerate(data):
    x.rio.to_raster(collection + "_" + str(idx) + ".tif", driver="COG")
```
A comprehensive tutorial on using PySTAC Client is available at [https://pystac-client.readthedocs.io/](https://pystac-client.readthedocs.io/en/latest/tutorials/pystac-client-introduction.html)


### OGC Web Services (GeoServer)

DEP data is also available as WMS, WFS and WCS services, and can be visualised using GIS Desktop tools such as QGIS.

For QGIS, relevant web service links below can be registered and used without authenication via the Data Source Manager.

- [WMS](https://dep-geoserver.westeurope.cloudapp.azure.com/geoserver/ows?service=WMS&version=1.3.0&request=GetCapabilities)
- [WFS](https://dep-geoserver.westeurope.cloudapp.azure.com/geoserver/ows?service=WFS&acceptversions=2.0.0&request=GetCapabilities)
- [WCS](https://dep-geoserver.westeurope.cloudapp.azure.com/geoserver/ows?service=WCS&acceptversions=2.0.1&request=GetCapabilities)

### QGIS STAC Plugin

- Pending

### Coastlines Data Download

The latest iteration of the DEP multi-year coastlines change data can be downloaded in GeoPackage from [AWS S3 Storage](https://dep-public-test.s3.us-west-2.amazonaws.com/coastlines_0-7-0-47_3832.gpkg).

### Support

For support and assistance on DEP data access, please contact [dep@spc.int](dep@spc.int).


<!-- 
### Water Observations from Space

### Mangroves

### GeoMADs

### Sentinel-1 Annual Mosaics
 -->

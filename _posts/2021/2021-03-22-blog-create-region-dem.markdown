---
layout: post
title: Create regional DEM
categories: blog
datasource: dem
datasource: Null
biophysical: Null
excerpt: "Identify and defined a regional DEM"
tags:
  - DEM
  - region
  - hydrografi
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2021-03-22 T18:17:25.000Z'
modified: '2021-03-22 T18:17:25.000Z'
comments: true
share: true
figure1: soil-moisture-avg_SPL3SMP_global_2015-2018@D001_005
fig2a: soil-moisture-am_SPL3SMP_global_20160122_005
fig2b: soil-moisture-avg_SPL3SMP_global_20160122_005
fig2c: soil-moisture-pm_SPL3SMP_global_20160122_005
figure3: soil-moisture-avg_SPL3SMP_global_2016009_005
movie1: soil-moisture-avg_SPL3SMP_global_2015121-2018345_005
movie2: soil-moisture-avg_SPL3SMP_global_2015-2018@16D_005


SMAP-0100_search-daac_20150331-20150807: SMAP-0100_search-daac_20150331-20150807

---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

## Introduction

This post covers how to define a region for hydrological modeling using DEM.

## Defining a regional DEM

1. Identify
2. Adjust region to projection system
3. Define a default region and system in the Framework
4. Define a user project for the default region and system
5. Link DEM tiles to the default region
6. Mosaic a regional DEM


### Identify DEM region

As the objectiv of creating the DEM os to create input data for hydrological modelling, you need to amnually identiry the boundaries (corners) of the DEM.  

### Adjust region to projection system

To align different DEM regions you need to set the corners of your DEM such that they fit the pixels of your original DEM tiles.

### Define a default region and system

Once your have identified and adjusted the corners of the DEM region, user the Framework process _DefaultRegionFromCoords_ to add the region to the Framework.


```
{
  "userproject": {
    "userid": "karttur",
    "projectid": "karttur",
    "tractid": "karttur",
    "siteid": "*",
    "plotid": "*",
    "system": "ease2n"
  },
  "period": {
    "timestep": "static"
  },
  "process": [
    {
      "processid": "DefaultRegionFromCoords",
      "overwrite": false,
      "parameters": {
        "regioncat": "global",
        "regionid": "nordichydroease2n",
        "regionname": "Nordic hydro ease2n",
        "parentid": "globe",
        "parentcat": "globe",
        "epsg": 6931,
        "stratum": "1",
        "minx": 0,
        "miny": -3500000,
        "maxx": 1822500,
        "maxy": -1718000,
        "version": "1.0",
        "title": "Nordic hydro ease2n",
        "label": "Nordic hydrological region for ease2n."
      },
      "dstpath": {
        "volume": "volume"
      },
      "dstcomp": [
        {
          "nordichydro": {
            "masked": "N",
            "measure": "N",
            "source": "karttur",
            "product": "pubroi",
            "content": "roi",
            "layerid": "hydroreg",
            "prefix": "hydroreg",
            "suffix": "v010-ease2n",
            "dataunit": "boundary",
            "celltype": "vector",
            "cellnull": "0"
          }
        }
      ]
    }
  ]
}
```

### Define a user project for the default region and system

As the DEM region created in the previous step is a global default region, use the process _ManageDefRegProj_ to create a user project linking to this region.

```
{
  "userproject": {
    "userid": "karttur",
    "projectid": "karttur",
    "tractid": "karttur",
    "siteid": "*",
    "plotid": "*",
    "system": "system"
  },
  "period": {
    "timestep": "static"
  },
  "process": [  
    {
      "processid": "ManageDefRegProj",
      "overwrite": false,
      "parameters": {
        "defaultregion": "nordichydroease2n",
        "tractid": "karttur-nordichydro",
        "tractname": "karttur Nordic Hydrology",
        "projid": "karttur-nordichydro",
        "projname": "Karttur Nordic Hydrology",
        "tracttitle": "Karttur Nordic Hydrology",
        "tractlabel": "Karttur Nordic Hydrology",
        "projtitle": "Karttur Nordic Hydrology",
        "projlabel": "Karttur Nordic Hydrology"
      }
    }
  ]
}
```

### Link DEM tiles to the default region

Before you can create the regional DEM, the system tiles covering the new region must be identified and registered. The Framework process _LinkDefaultRegionTiles_ does that.

```
{
  "userproject": {
    "userid": "karttur",
    "projectid": "karttur",
    "tractid": "karttur",
    "siteid": "*",
    "plotid": "*",
    "system": "ease2n"
  },
  "period": {
    "timestep": "static"
  },
  "process": [
    {
      "processid": "LinkDefaultRegionTiles",
      "version": "0.9",
      "verbose": 2,
      "parameters": {
        "defregmask": "global"
        },
      "srcpath": {
        "volume": "MODIS56",
        "hdr": "shp",
        "dat": "shp"
      },
      "srccomp": [
        {
          "regions": {
            "source": "karttur",
            "product": "roi",
            "content": "pubroi",
            "layerid": "defreg",
            "prefix": "defreg",
            "suffix": "v010"
          }
        }
      ]
    }
  ]
}
```

### Mosaic a regional DEM

Create the regional DEM with the process __, that mosaics the tiles to a regional layer.

```
{
  "userproject": {
    "userid": "karttur",
    "projectid": "karttur-nordichydro",
    "tractid": "karttur-nordichydro",
    "siteid": "*",
    "plotid": "*",
    "system": "ease2n"
  },
  "period": {
    "timestep": "static"
  },
  "process": [
    {
      "processid": "MosaicTiles",
      "version": "1.3",
      "overwrite": true,
      "parameters": {
        "tr_xres": 90,
        "tr_yres": 90,
        "resample": "near",
        "asscript": false,
        "fillnodata": true,
        "fillmaxdist": 3,
        "fillsmooth": 0
      },
      "srcpath": {
        "volume": "MODIS56"
      },
      "dstpath": {
        "volume": "MODIS56"
      },
      "srccomp": [
        {
          "dem90": {
            "source": "ESA-DUE",
            "product": "panarcticdem",
            "content": "dem",
            "layerid": "panarcticdem90",
            "prefix": "dem90",
            "suffix": "v01"
          }
        }
      ],
      "dstcopy": [
        {
          "dem90": {
            "srccomp": "dem_dem90",
            "layerid": "panarcticdem90"
          }
        }
      ]
    }
  ]
}

```

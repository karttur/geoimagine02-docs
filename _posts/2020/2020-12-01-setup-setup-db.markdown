---
layout: article
title: Set up the database (setup_db)
categories: setup
excerpt: "Run the setup_db package to setup the postgres database for Karttur's GeoImagine Framework"
previousurl: null
nexturl: setup/setup-processes
image: avg-trmm-3b43v7-precip_3B43_trmm_2001-2016_A
date: '2020-12-01 T18:17:25.000Z'
modified: '2021-10-17 T14:17:25.000Z'
comments: true
share: true
---
<script src="https://karttur.github.io/common/assets/js/karttur/togglediv.js"></script>

## Introduction

In Karttur's GeoImagine Framework both the processes and the data are stored in a postgreSQL (psotgres) database. The database is built up with schemas associated with typical processes and data sources. This post explains how to setup the complete database by using the special package (<span class='package'>setup_db</span>) and prepared json files defining all the schemas and tables.

## Prerequisites

You must have the complete Spatial Data Integrated Development Environment (SPIDE) installed as described in the blog [Install and setup spatial data IDE](https://karttur.github.io/setup-ide/). This post is a step by step manual for downloading and running the Framework python package <span class='package'>setup_db</span>. You can also [clone the complete Framework - TO BE ADDED](#) and then run <span class='package'>setup_db</span>.

## Setup database

The blogpost [Connect Python and PostgreSQL using psycopg2](https://karttur.github.io/setup-ide/blog/connect-with-psycopg2/) contains a python script for creating databases in postgres using Python. And the blogpost [Postgres setup with Python & xml](https://karttur.github.io/setup-ide/blog/setup-db-karttur/) describes how to combine **xml** and python to create tables. More recent versions of the Framework instead use <span class='file'>json</span> objects for parameterisation. But if you want to understand the principles behind the framework package <span class='package'>setup_db</span>, the blog posts above explains just that.

## db_setup python package

The framework v2.0 package [setup_db is available on GitHub](https://github.com/karttur/geoimagine02-setup_db/) (click the link or see the figure below) and contains the complete structure for setting up the Framework postgres database.

The [<span class='package'>db_setup</span>](https://github.com/karttur/geoimagine02-setup_db/) package contains five <span class='file'>.py</span> files, the standard modules <span class='package'>\_\_init\_\_.py</span> and <span class='package'>version.py</span>, plus one main module, one class module and one module that reads <span class='file'>json</span> files:

- setup_db_main.py
- setup_db_class.py
- paramjson_mini.py

The package also contains a subfolder called [<span class='file'>doc</span>](https://github.com/karttur/geoimagine-setup_db/tree/master/doc/) that contains two text files:

- db_karttur_dbusers_YYYMMDD.txt
- db_karttur_setup_YYYYMMD.txt

The file <span class='file'>db_karttur_dbusers_YYYMMDD.txt</span> contains all the database roles (users), and the file <span class='file'>db_karttur_setup_YYYYMMD.txt</span> lists, in sequence, all the json objects (files) to execute.

Under the <span class='file'>doc</span> directory there is also a sub-directory, <span class='file'>jsonsql</span>, that contain all the json files listed in <span class='file'>db_karttur_setup_YYYYMMD.txt</span>. The sub-folder  <span class='file'>jsonsql_todo</span> lists json objects not yet completed for setup.

### Download the package

Go to the GithUb repo for [geoimagine02-setup_db](https://github.com/karttur/geoimagine02-setup_db/). Click the <span class='button'>Code</span> button and then <span class='textbox'>Download ZIP</span>.

<figure>
<img src="../../images/github_code_download_setup-db.png">
<figcaption>Download setup_db from GitHub</figcaption>
</figure>

### Create a hierarchical python package in eclipse

Start <span class='app'>Eclipse</span>. Create a project (call it what you want):

<span class='menu'>File : New : Project : PyDev project</span>

Create a new PyDev Package and call it 'geoimagine':

<span class='menu'>File : New : PyDev Package</span>

Create a new sub-package and call it 'db_setup':

<span class='menu'>File : New : PyDev Package</span>

In the dialog window you should see the main package ('geoimagine') already filled (<span class='textbox'>geoimagine</span>). Use Python syntax and add a dot (.) followed by the name of the sub-package ('db_setup') (<span class='textbox'>geoimagine.db_setup</span>).

Use the <span class='app'>Finder</span> and navigate to the download/clone of the <span class='package'>setup_db</span> package, mark all of the content and drop in the newly created sub-package in the navigation frame of <span class='app'>Eclipse</span>.

You should now have a sub-package with the following file structure:

```
.
|____version.py
|____setup_db_main.py
|____LICENSE
|______init__.py
|____paramjson_mini.py
|____setup_db_class.py
|____doc
| |____db_karttur_setup_20211018.txt
| |____db_karttur_dbusers_20211018.txt
| |____jsonsql
| | |____compositions_sentinel_v090_sql.json
| | |____modis_tilecoords_v090_sql.json
| | |____compositions_system_v090_sql.json
| | |____compositions_smap_v090_sql.json
| | |____user_super_v090_sql.json
| | |____general_processeschain_v090_sql.json
| | |____general_schema_v090_sql.json
| | |____layout_v090_sql.json
| | |____general_records_v090_sql.json
| | |____sentinel_template_v090_sql.json
| | |____compositions_regions_v090_sql.json
| | |____landsat_scenes_bands_v090_sql.json
| | |____sentinel_tilecoords_v090_sql.json
| | |____soilmoisture_v090_sql.json
| | |____modis_template_v090_sql.json
| | |____user_projects_v090_sql.json
| | |____compositions_export_v090_sql.json
| | |____users_v090_sql.json
| | |____climateindexes_v090_sql.json
| | |____all_system_regions_v090_sql.json
| | |____modis_tile_regions_v090_sql.json
| | |____landsat_scenecoords_v090_sql.json
| | |____landsat_templates_v090_sql.json
| | |____compositions_modis_v090_sql.json
| | |____compositions_landsat_v090_sql.json
| | |____system_regions_v090_sql.json
| | |____SMAP_products_v090_sql.json
| | |____SMAP_template_v090_sql.json
| | |____general_processes_v090_sql.json
| | |____sentinel_scenes_bands_v090_sql.json
| | |____regions_v090_sql.json
| | |____general_grant_karttur_v090_sql.json
| | |____compositions_ancillary_v090_sql.json
| | |____compositions_specimen_v090_sql.json
| | |____ancillary_v090_sql.json
| | |____general_GDALtypes_v090_sql.json
| | |____modis_scenes_bands_v090_sql.json
| |____jsonsql_todo
| | |____endmember_v090_sql.json
| | |____compositions_ease2_v090_sql.json
| | |____specimen_v090_sql.json
| | |____specimen_satdata_v090_sql.json
| | |____landsat_tilecoords_v090_sql.json
| | |____general_grant_sql_v090_sql.json
```

### Package processes

The database setup is accomplished through a set of special processes:

- createschema
- createtable
- tableinsert
- tableupdate
- grant

These processes are **not** defined in the database itself and can only be run from the package <span class='package'>setup_db</span>.

### setup_db_main.py

In <span class='module'>setup_db_main.py</span> there are predefined commands and links in the main section that are used to setup the entire database. You do not need to edit any of these files unless you want to change the default roles (users) as explained in the preparation post on [Database connections](../../prep/prep-dblink/).

#### Create main production db

If you did not create a production db as described in the post [Postgres setup with Python & xml](https://karttur.github.io/setup-ide/setup-ide/setup-db-karttur/) you have to create it now. The default name of the database is _postgres_, but it can be set to any other name.

To create the production database uncomment the first lines under the "\_\_main\_\_" section, and then run the module from the <span class='app'>Eclipse</span> menu <span class='menu'>Run : run</span>.

```
if __name__ == "__main__":
    '''
    This module only needs to be run at the very startup of building the Karttur Geo Imagine framework.
    To run, remove the comment "#prodDB" and set the name of your production DB ("YourProdDB")
    '''
    verbose = 1
    #prodDB = 'YourProdDB' #'postgres

    # SetUpProdDb creates an empty Postgres db cluster
    # Change 'YourProdDB' to the name of your db
    SetUpProdDb(prodDB,verbose)
```

You should now have a production database. If you want to check the database or change/add superuser(s) please refer to the post on [Install PostgreSQL and postGIS](https://karttur.github.io/setup-ide/setup-ide/install-postgres/).

#### Setup schemas and tables

The next lines of the "\_\_main\_\_" section link to the files in <span class='file'>doc</span> subfolder and loops through them to setup all the schemas and tables. All you need to do is to uncomment the lines as shown below.

```
    '''
    SetupSchemasTables creates schemas and tables from json files, with the relative path to the
    json files given in the plain text file "projFPN".
    '''
    projFPN = path.join('doc','db_karttur_setup_20211018.txt')
    SetupSchemasTables(projFPN,prodDB)
```

The file <span class='file'>db_karttur_setup_20211018.txt</span> only contains links to the json files to loop over.

<button id= "togglesetuptxt" onclick="hiddencode('setuptxt')">Hide/Show db_karttur_setup_YYYYMMDD.txt</button>

<div id="setuptxt" style="display:none">

{% capture text-capture %}
{% raw %}

```
# general_schema_vXX_sql.json installs the default database schemas
jsonsql/general_schema_v090_sql.json

# general_processes_vXX_sql.json installs the tables for handling paths and processes
jsonsql/general_processes_v090_sql.json

#general_records_vXX_sql.json adds records for super users and the process for managing all other processes
jsonsql/general_records_v090_sql.json

# general_GDAL_vXX_sql.json installs and fills the tables that defines the different
# cell types and file types that the system can handle
jsonsql/general_GDALtypes_v090_sql.json

# general_processeschain_vXX_sql.json installs the automated processing chains tables
jsonsql/general_processeschain_v090_sql.json

# compositions_ancillary_vXX_sql.json installs the tables for defining ancillary compositions
jsonsql/compositions_ancillary_v090_sql.json

# compositions_system_vXX_sql.json installs the tables for defining system compositions
jsonsql/compositions_system_v090_sql.json

# compositions_specimen_vXX_sql.json installs the tables for defining specimen compositions
jsonsql/compositions_specimen_v090_sql.json

# compositions_smap_vXX_sql.json installs the tables for defining smap compositions
jsonsql/compositions_smap_v090_sql.json

# compositions_sentinel_vXX_sql.json installs the tables for defining sentinel compositions
jsonsql/compositions_sentinel_v090_sql.json

# compositions_regions_vXX_sql.json installs the tables for defining region compositions
jsonsql/compositions_regions_v090_sql.json

# compositions_modis_vXX_sql.json installs the tables for defining modis compositions
jsonsql/compositions_modis_v090_sql.json

# compositions_landsat_vXX_sql.json installs the tables for defining landsat compositions
jsonsql/compositions_landsat_v090_sql.json

# compositions_export_vXX_sql.json installs the tables for defining export compositions
jsonsql/compositions_export_v090_sql.json

# all_system_regions_vXX_sql.json installs the region tables for the different systems
jsonsql/all_system_regions_v090_sql.json

# ancillary_vXX_sql.json installs the tables that defines ancillary data sources
jsonsql/ancillary_v090_sql.json

# SKIPPED FOR NOW
# endmember_vXX_sql.json tables for soil line and vegetation spectral extraction
##NotNow/endmember_v090_sql.json

# SKIPPED FOR NOW
# speclib_vXX_sql.json tables for spectral library
#NotNow/speclib_v090_sql.json

#landsat_tilecoord_vXX_sql.json adds the coordinates for landsat tiles
jsonsql/landsat_scenecoords_v090_sql.json

# landsat_scenes_bands_vXX_sql.json installs the tables for landsat scenes, bands and masks
jsonsql/landsat_scenes_bands_v090_sql.json

# landsat_templates_vXX_sql.json installs the landsat template table
jsonsql/landsat_templates_v090_sql.json

# SKIPPED FOR NOW
# landsat_usgs_meta_vXX_sql.json installs the core landsat meta tables, the columns are installed later
#NotNow/landsat_usgs_meta_v090_sql.json

# layout_vXX_sql.json adds the tables for layout
jsonsql/layout_v090_sql.json

# MODIS regional tiles for land and continents
jsonsql/modis_tile_regions_v090_sql.json

# modis_scenes_bands_vXX_sql.json adds both the table for holding all scenes available at the
# datapool as well as the tables for local modis data holdings
jsonsql/modis_scenes_bands_v090_sql.json

# modis_template_vXX_sql.json installs the modis template table, and adds records for the MODIS products in use
jsonsql/modis_template_v090_sql.json

# modis_tilecoords_vXX_sql.json adds the table for modis tile coordinates
jsonsql/modis_tilecoords_v090_sql.json

# projects_vXX_sql.json installs the tables that defines user projects and project types
#NOT YET

# system_regions_vXX_sql.json installs the tables that hold system default regions and categories
jsonsql/system_regions_v090_sql.json

# regions_vXX_sql.json installs the tables that hold regions
jsonsql/regions_v090_sql.json

# SKIPPED FOR NOW
# specimen_vXX_sql.json adds the table for ground sampled data
##NotNow/specimen_v090_sql.json

# SKIPPED FOR NOW
# specimen_satdata_vXX_sql.json adds the table for linking sat data to sample points
##NotNow//specimen_satdata_v090_sql.json

# SKIPPED FOR NOW
# topo_vXX_sql.json adds the db for point elevation data
##NotNow//topo_v090_sql.json

# User projects - defines users and user projects
jsonsql/user_projects_v090_sql.json

# usersvXX_sql.json installs the tables that hold all the system users
jsonsql/users_v090_sql.json

# superuserprojs_vXX_sql.json adds the superusers of the system,
# NOTE - THE JSON FILE MUST BE EDITED TO SET THE PREFERED SUPER USERS
jsonsql/user_super_v090_sql.json

#climateindexes_vXX_sql.json adds the schema and table for climate indexes
jsonsql/climateindexes_v090_sql.json

#sentinel_scenes_bands_vXX_sql.json adds the schema for sentinel data
jsonsql/sentinel_scenes_bands_v090_sql.json

#sentinel_tilecoord_vXX_sql.json adds the coordinates for sentinel tiles
jsonsql/sentinel_tilecoords_v090_sql.json

#sentinel_template_vXX_sql.json adds the sentinel tile templates
jsonsql/sentinel_template_v090_sql.json

#SMAP_products_vXX_sql.json create a table for SMAp products and inserts records
jsonsql/SMAP_products_v090_sql.json

#SMAP_template_vXX_sql.json
jsonsql/SMAP_template_v090_sql.json

#soilmoisture_vXX_sql.json creates soilmoisture tables
jsonsql/soilmoisture_v090_sql.json
```

{% endraw %}
{% endcapture %}
{% include widgets/toggle-code.html  toggle-text=text-capture  %}
</div>

Run the module, and all the schemas and tables defined in the above json files will be created.

#### Add default users

The next lines under the \_\_main\_\_" section link to the text file <span class='file'>db_karttur_dbusers_20211018.txt</span>.

```
    '''
    #db_karttur_dbusers_YYYYMMDDX.xml adds db users for handling connections to postgres db
    '''
    projFPN = path.join('doc','db_karttur_dbusers_20211018.txt')
    SetupSchemasTables(projFPN,prodDB)
```

This links to a single json file <span class='file'>general_grant_karttur_v090_sql.json</span> that contains all the database roles and rights, including passwords. You need to edit the passwords to match the <span class='file'>.netrc</span> file that is used for accessing the database at runtime.

#### Superusers and process for setting up all other processes

The package <span class='package'>db_setup</span> also installs the system superuser and two processes: [_addrootproc_](../../subprocess/subproc-addrootproc/) and [_addsubproc_](../../subprocess/subproc-addsubproc/). Having access to the superuser and the two processes, all other processes can be installed using the package [<span class='package'>setup_processes</span>](../../package/package-setup_processes/).

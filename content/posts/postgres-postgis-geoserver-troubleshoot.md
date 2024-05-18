+++ 
date = 2024-05-15T15:16:42+01:00
title = "PostGIS - Geoserver full setup + troubleshoot"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

# Setup

## Prerequisites

Ubuntu OS. Install Postgres, Geoserver (independent binary), PGAdmin (optional).

## Create PostGIS extension

1. Download the necessary tools: `sudo apt install postgis postgresql-postgis`

2. Run the following query with in PGAdmin or psql(command line): `CREATE EXTENSION postgis;`

## Import GeoJson file:

1. Download the geojson file to import: https://data.gov.ie/dataset/pra-state-assets . If link is down, use [this](https://drive.google.com/file/d/1hiBLPcs_hV6Lmi-iMmYB6XHra92NloLn/view?usp=sharing).

2. Install geojson to postGIS conversion tool: `sudo apt install gdal`

3. Run the following command to import (PRA_State_Assets.geojson is the geojson filename, destination_table is the table name):

```bash
ogr2ogr -f "PostgreSQL" PG:"dbname=postgres user=postgres" "PRA_State_Assets.geojson" -nln destination_table -append
```

## Configure Geoserver

Filepath: `/usr/share/geoserver/webapps/geoserver/WEB-INF/web.xml`

1. Fix CORS issues. [Reference.](https://www.linkedin.com/pulse/fixing-cors-error-geoserver-krishna-lodha/)

Uncomment these block of code:

```xml
    <filter>
      <filter-name>cross-origin</filter-name>
      <filter-class>org.eclipse.jetty.servlets.CrossOriginFilter</filter-class>
      <init-param>
        <param-name>chainPreflight</param-name>
        <param-value>false</param-value>
      </init-param>
      <init-param>
        <param-name>allowedOrigins</param-name>
        <param-value>*</param-value>
      </init-param>
      <init-param>
        <param-name>allowedMethods</param-name>
        <param-value>GET,POST,PUT,DELETE,HEAD,OPTIONS</param-value>
      </init-param>
      <init-param>
        <param-name>allowedHeaders</param-name>
        <param-value>*</param-value>
      </init-param>
    </filter>
```

and these:

```xml
    <filter-mapping>
      <filter-name>Set Character Encoding</filter-name>
      <url-pattern>/*</url-pattern>
    </filter-mapping>
```

2. Enable JSONP. Uncomment the following lines.

```xml
<context-param>
    <param-name>ENABLE_JSONP</param-name>
    <param-value>true</param-value>
</context-param>
```

3. Update port number:

Edit `/usr/share/geoserver/start.ini` file: `jetty.http.port=8090`

4. Run Geoserver:

`./usr/share/geoserver/bin/startup.sh`

## Link Geoserver to PostGIS

1. Login with default username: `admin` password: `geoserver`

2. On the left menu, go to store > Add new store > PostGIS

3. Enter database details.

4. On the left menu, go to Layers > Add a new layer

5. Select the store created.

6. Enter the details, click compute from native bounds for the bounding boxes.

7. On the left menu, go to Layer Preview. Verify the layer created is there. Click on openlayers to verify it's working.

# Troubleshoot

## Peer authentication failed for user "postgres"

Login to postgresql with `psql`. For e.g. `psql -h localhost -U postgres`

```sql
SHOW hba_file;
```

The command will reveal a path to a file, edit that file with sudo (`sudo -i` or `sudoedit`)

In the file, replace all the peer/md5 column with `trust`. [Reference](https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge)

Run in PGAdmin or command line, run this query before importing any data:

## Compute bounding box not working in Geoserver / In Layer Preview, clicking openlayers downloads WMS file instead of opening in separate tab.

Ensure you run `CREATE EXTENSION postgis;` before importing the any data.

Try restarting postgresql too: `sudo systemctl restart postgresql`

+++ 
date = 2024-05-15T15:16:42+01:00
title = "Postgres - PostGIS - Geoserver setup troubleshoot"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

# Postgres

After downloading postgresql, login with `psql`

psql -h localhost -U postgres

```sql
SHOW hba_file;
```

The command will reveal a path to a file, edit that file with sudo:

```bash
sudo -i
```

In the file, replace all the peer/md5 column with `trust`. Reference
https://stackoverflow.com/questions/18664074/getting-error-peer-authentication-failed-for-user-postgres-when-trying-to-ge

# PostGIS

`sudo apt install postgis postgresql-postgis`

Run in PGAdmin or command line, run this query before importing any data:
`CREATE EXTENSION postgis;`

compute bounding box not working in geoserver: restart postgresql:

`sudo systemctl restart postgresql`

layer preview, clicking openlayers download wms instead of opening in portal.

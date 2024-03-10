# Map

The Map module allows viewing, and importing of OpenStreetMap PBF files. The map is rendered live as you are using it.
Previously renderd tiles (images) are stored on root disk of the system which prevents re-rendering of tiles that have
been viewed previously.

## Map

The Map tab is a simple iframe around the Apache2 service on port `:8084`

![Screenshot of the Map Viewer tab.](map-viewer.png)

## Manage

The files displayed in the Manage tab are those found in your media directory under `/map`.  **Time To Import** is
estimated by running many tests importing PBF files on a Raspberry Pi 4. The larger the file, the more inaccurate the
time will be.

> Select all map files you want to import, importing will erase any maps previously imported!

![Manage Map Page](map-manage.png)

### Downloading Map Files

Map files are available for download from the Geofabrick company. You can download them using the **Files Downloader**,
save them to the `map` directory. After they have been downloaded, you will need to import them.

![Downloading of a custom OSM PBF file.](pbf-file-downloader.png)

## Manually Importing

You can manually import a PBF file using the **import_map.sh** script:

```shell
/opt/wrolpi/scripts/import_map.sh /media/wrolpi/map/austria-231121.osm.pbf
```

Multiple maps can be imported like so:

```shell
/opt/wrolpi/scripts/import_map.sh /media/wrolpi/map/one.osm.pbf /media/wrolpi/map/two.osm.pbf /media/wrolpi/map/three.osm.pbf
```

## Reset Map

If your map is not working, maps cannot be imported, or some other reason, you can reset the map database using the
reset script:

```shell
/opt/wrolpi/scripts/reset_map.sh
```

Next, run the repair script:

```shell
/opt/wrolpi/repair.sh
```

Browse to your map, you should see the default map. If you do not, you may need to clear your browse's cache. Finally,
import your desired maps.
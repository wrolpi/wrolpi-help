# Special Directories

| Path                    | Purpose                                                  |
|-------------------------|----------------------------------------------------------|
| `/media/wrolpi/`        | The [Media Directory](#media-directory).                 |
| `/opt/wrolpi/`          | The [source code](#wrolpi-source-directory) of WROLPi.   |
| `/media/wrolpi/config/` | The [configuration files](#wrolpi-config) of the WROLPi. |
| `/opt/wrolpi-blobs/`    | Contains files necessary to the repair of a WROLPi.      |
| `/opt/wrolpi-help/`     | These help files.                                        |

## Media Directory

`/media/wrolpi/`

The media directory is a ubiquitous part of WROLPi. It is expected that an external drive will be mounted here. All
files that are downloaded by WROLPi will be saved within this directory.

The normal media directory is `/media/wrolpi`

## WROLPi Source Directory

`/opt/wrolpi/`

This directory contains the source code of the WROLPi API, app, etc.

## WROLPi Config

`/media/wrolpi/config/`

This directory contains the configuration files of the WROLPi. These files are considered the "source of truth" and
their contents will alter the behavior of the WROLPi.

## WROLPi Blobs

`/opt/wrolpi-blobs/`

This directory contains the files necessary to repair a WROLPi. For example, the `gis-map.dump.gz` file contains a
Postgresql dump of the map database.  **It is best to leave this directory as-is.**

## WROLPi Help

`/opt/wrolpi-help/`

This help file you are reading is contained in this directory.

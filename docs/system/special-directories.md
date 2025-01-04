# Special System Directories

| Path                    | Purpose                                                                              |
|-------------------------|--------------------------------------------------------------------------------------|
| `/media/wrolpi/`        | The [Media Directory](#media-directory).                                             |
| `/media/wrolpi/config/` | The [configuration files](#wrolpi-config) of the WROLPi.                             |
| `/media/wrolpi/tags/`   | The [Tags Directory](#tags-directory) contains links to files that have been tagged. |
| `/opt/wrolpi-blobs/`    | Contains files necessary to repair a WROLPi.                                         |
| `/opt/wrolpi-help/`     | These help files.                                                                    |
| `/opt/wrolpi/`          | The [source code](#wrolpi-source-directory) of WROLPi.                               |

## Media Directory

`/media/wrolpi/`

The media directory is a ubiquitous part of WROLPi. It is expected that an external drive will be mounted here. All
files that are downloaded by WROLPi will be saved within this directory.

The normal media directory is `/media/wrolpi`

## WROLPi Config

`/media/wrolpi/config/`

This directory contains the configuration files of the WROLPi. These files are considered the "source of truth" and
their contents will alter the behavior of the WROLPi.

## Tags Directory

`/media/wrolpi/tags`

This directory contains links to tagged files. It is automatically managed by WROLPi as you add or remove tags from
files.

**Warning!**  Do not store files in this directory, they will be automatically deleted.

## WROLPi Blobs

`/opt/wrolpi-blobs/`

This directory contains the files necessary to repair a WROLPi. For example, the `map-db-gis.dump` file contains a
Postgresql dump of the map database.  **It is best to leave this directory as-is.**

## WROLPi Help

`/opt/wrolpi-help/`

This help file you are reading is contained in this directory.

## WROLPi Source Directory

`/opt/wrolpi/`

This directory contains the source code of the WROLPi API, app, etc.

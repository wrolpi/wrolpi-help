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

This directory contains the configuration files of the WROLPi and the SQLite database (`wrolpi.db`). Config files
are considered the "source of truth" and their contents will alter the behavior of the WROLPi.
See [How Configs Work](configs.md) and [Databases](databases.md).

## Tags Directory

`/media/wrolpi/tags`

This directory contains links to tagged files. It is automatically managed by WROLPi as you add or remove tags from
files.  See [Tags](tags.md).

**Warning!**  Do not store files in this directory, they will be automatically deleted.

## WROLPi Blobs

`/opt/wrolpi-blobs/`

This directory contains files necessary to repair a WROLPi (for example map fonts and other offline assets).
**It is best to leave this directory as-is.**

## WROLPi Help

`/opt/wrolpi-help/`

This help file you are reading is contained in this directory.

## WROLPi Source Directory

`/opt/wrolpi/`

This directory contains the source code of the WROLPi API, app, etc.

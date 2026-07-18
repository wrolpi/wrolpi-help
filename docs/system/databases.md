# Database

WROLPi uses a single [SQLite](https://sqlite.org/) database stored in the media directory.
There is no separate database service — the API opens the file directly.

## Location

`/media/wrolpi/config/wrolpi.db`

The database lives next to the [YAML config files](configs.md) so a user's entire library
(files + configs + database) travels with the media drive. WAL sidecars (`wrolpi.db-wal`,
`wrolpi.db-shm`) may appear alongside it while the API is running.

The database is created automatically on first API start. To wipe and rebuild it (you will need
to refresh your files afterward), see [Reset API Database](getting-help.md#reset-api-database).

## Tables

| Name             | Purpose                                                 | Relations                    | `/opt/wrolpi` File             |
|------------------|---------------------------------------------------------|------------------------------|--------------------------------|
| alembic_version  | Tracks Alembic migration.                               |                              | `alembic`                      |
| archive          | Data about a FileGroup Archive.                         | file_group_id, domain_id     | `modules/archive/models.py`    |
| channel          | Data about a video Channel.                             |                              | `modules/videos/models.py`     |
| collection       | A logical grouping of FileGroups.                       | tag_id                       | `wrolpi/collections/models.py` |
| collection_item  | Links a FileGroup to a Collection.                      | collection_id, file_group_id | `wrolpi/collections/models.py` |
| directory        | Directories in the media directory.                     |                              | `wrolpi/files/models.py`       |
| domains          | Groups Archives by shared URL domain.                   |                              | `modules/archive/models.py`    |
| download         | Data about what should be downloaded and when.          |                              | `wrolpi/downloader.py`         |
| ebook            | Data about FileGroups that are books.                   | file_group_id                | `wrolpi/files/ebooks.py`       |
| file_group       | Each record is a group of files that share a stem.      |                              | `wrolpi/files/models.py`       |
| inventory        | A collection of items.                                  |                              | `modules/inventory/models.py`  |
| item             | An item in an inventory.                                | inventory_id                 | `modules/inventory/models.py`  |
| map_file         | Data about map files (if they have been imported, etc.) |                              | `modules/map/models.py`        |
| tag              | Data about a Tag (name, color, etc.)                    |                              | `wrolpi/tags.py`               |
| tag_file         | A FileGroup that has been tagged.                       | tag_id, file_group_id        | `wrolpi/tags.py`               |
| tag_zim          | An entry (article) that was tagged in a Zim file.       | tag_id, zim_id, zim_entry    | `modules/zim/models.py`        |
| video            | Data about a FileGroup Video                            | file_group_id, channel_id    | `modules/videos/models.py`     |
| wrolpi_flag      | Long-term flags that have occurred in the API.          |                              | `wrolpi/flags.py`              |
| zim              | A Zim file                                              |                              | `modules/zim/models.py`        |
| zim_subscription | A recurring download of a Zim file.                     |                              | `modules/zim/models.py`        |

Full-text search uses SQLite FTS5 virtual tables (created alongside the main schema).

## Maps

Map data is **not** stored in this database. Maps use PMTiles files under `/media/wrolpi/map/`,
served by Caddy. See the [Map module](../modules/map/index.md).

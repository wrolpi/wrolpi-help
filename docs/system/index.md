# Overview of WROLPi Systems

* WROLPi is based off [Debian OS](https://debian.org) and [Raspberry Pi OS](https://www.raspberrypi.com/software/)
* WROLPi has 4 user-facing services:
    * [API](#api)
    * [App](#app)
    * [Map](#map)
    * [Zim](#zim)

## Services

### API

| Software Project                                           | Purpose                                                                 |
|------------------------------------------------------------|-------------------------------------------------------------------------|
| [Python](https://python.org)                               | The language of the WROLPi API and scripts.                             |
| [Sanic](https://sanic.dev)                                 | An async web app framework, used for the API.                           |
| [SQLAlchemy](https://www.sqlalchemy.org/)                  | The database ORM.                                                       |
| [yt-dlp](https://github.com/yt-dlp/yt-dlp)                 | Used to download videos.                                                |
| [SingleFile](https://github.com/gildas-lormeau/SingleFile) | Used to create Archives.                                                |
| [Readability](https://github.com/mozilla/readability)      | Used to extract the article from an Archive.                            |
| [Chromium](https://chromium.org)                           | Used to create Archives.                                                |
| [FFMPEG](https://ffmpeg.org/)                              | Video processing software which is used by the API to manipulate videos |
| [libzim](https://pypi.org/project/libzim/)                 | Used to search the ZIM files                                            |

### DB

| Software Project                          | Purpose                                                              |
|-------------------------------------------|----------------------------------------------------------------------|
| [Postgresql](https://www.postgresql.org/) | Facilitates searching of files, scheduling downloads, and much more. |

### App

| Software Project                             | Purpose                                                            |
|----------------------------------------------|--------------------------------------------------------------------|
| [ReactJS](https://react.dev/)                | The framework which controls the App.  Built on-top of Javascript. |
| [SemanticUI](https://react.semantic-ui.com/) | The framework and style of the App's buttons, tables, etc.         |
| [NodeJS](https://nodejs.org)                 | The run-time environment which runs the ReactJS app.               |

### Map

| Software Project                                | Purpose                                  |
|-------------------------------------------------|------------------------------------------|
| [OpenStreetMap](https://www.openstreetmap.org/) | Provides the Map data                    |
| [osmium](https://osmcode.org/osmium-tool/)      | Used to merge map PBF files.             |
| [osm2pgsql](https://osm2pgsql.org/)             | Used to import PBF files into Postgresql |

### Zim

| Software Project                                      | Purpose                       |
|-------------------------------------------------------|-------------------------------|
| [Kiwix](https://kiwix.org)                            | Provides the ZIM files        |
| [Kiwix Server](https://github.com/kiwix/kiwix-tools/) | Hosts the ZIM files interface |

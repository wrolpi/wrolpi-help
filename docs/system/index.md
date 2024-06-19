# Overview of WROLPi Systems

* WROLPi is based off [Debian OS](https://debian.org) and [Raspberry Pi OS](https://www.raspberrypi.com/software/)
* WROLPi has several user-facing services:
    * [Web](#web) (`:80`)
    * [API](#api) (`:8081`)
    * [App](#react-app) (`:8082`)
    * [Map](#map) (`:8084`)
    * [Zim](#zim) (`:8085`)
    * [Help](#help) (`:8086`)
* WROLPi services are started and maintained by `systemd`.  [Logs](logs.md) are gathered by `systemd`.

## Services

### Web

The nginx service which facilitates communication between the other services (especially in the docker containers in
the development environment.)

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

### React App

| Software Project                             | Purpose                                                            |
|----------------------------------------------|--------------------------------------------------------------------|
| [ReactJS](https://react.dev/)                | The framework which controls the App.  Built on-top of Javascript. |
| [SemanticUI](https://react.semantic-ui.com/) | The framework and style of the App's buttons, tables, etc.         |
| [NodeJS](https://nodejs.org)                 | The run-time environment which runs the ReactJS app.               |

### Map

| Software Project                                | Purpose                                   |
|-------------------------------------------------|-------------------------------------------|
| [OpenStreetMap](https://www.openstreetmap.org/) | Provides the Map data.                    |
| [osmium](https://osmcode.org/osmium-tool/)      | Used to merge map PBF files.              |
| [osm2pgsql](https://osm2pgsql.org/)             | Used to import PBF files into Postgresql. |

### Zim

| Software Project                                      | Purpose                        |
|-------------------------------------------------------|--------------------------------|
| [Kiwix](https://kiwix.org)                            | Provides the ZIM files.        |
| [Kiwix Server](https://github.com/kiwix/kiwix-tools/) | Hosts the ZIM files interface. |

### Help

| Software Project                  | Purpose                                    |
|-----------------------------------|--------------------------------------------|
| [Mkdocs](https://www.mkdocs.org/) | Serves these Markdown documentation files. |

## Development Only Services

If using the Docker containers (the development environment), you may have additional services:

* [Web](#development-web) (`:8080`)
* [Archive](#archive) (`:8083`)

### Development Web

| Software Project            | Purpose                                                       |
|-----------------------------|---------------------------------------------------------------|
| [nginx](https://nginx.org/) | Facilitates integration between development docker containers |

### Archive

Separation of the API and the Archive service is necessary to prevent an overly complex API docker container.

| Software Project                                           | Purpose                                                                                             |
|------------------------------------------------------------|-----------------------------------------------------------------------------------------------------|
| [Python](https://python.org)                               | The language of the Archive service.                                                                |
| [Sanic](https://sanic.dev)                                 | An async web app framework, used to facilitate archiving of webpage in the development environment. |
| [SingleFile](https://github.com/gildas-lormeau/SingleFile) | Used to create Archives.                                                                            |
| [Readability](https://github.com/mozilla/readability)      | Used to extract the article from an Archive.                                                        |
| [Chromium](https://chromium.org)                           | Used to create Archives.                                                                            |

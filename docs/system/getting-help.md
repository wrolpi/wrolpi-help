# Getting Help

## Online

Help can be found online at these places:

* WROLPi Discord: [https://discord.gg/HrwFk7nqA2](https://discord.gg/HrwFk7nqA2)
* WROLPi Github: [https://github.com/lrnselfreliance/wrolpi](https://github.com/lrnselfreliance/wrolpi)
* WROLPi Youtube Channel: [https://www.youtube.com/@wrolpi](https://www.youtube.com/@wrolpi)

### `install.sh`

WROLPi may be repaired using the installation script which requires internet, run it like so:

`/opt/wrolpi/install.sh`

## Offline

### `repair.sh`

WROLPi has a repair script which will attempt to repair the WROLPi while offline. It copies configs, restarts services,
etc. Run the repair script like so:

`/opt/wrolpi/repair.sh`

### `help.sh`

WROLPi has a help script which checks common failure points on a WROLPi system, run it like so:

`/opt/wrolpi/help.sh`

Example output:

```text
WROLPi version: 0.13.1-beta

OK: Running on Raspberry Pi 5
OK: Found wrolpi user
OK: The WROLPi directory exists
OK: The WROLPi blobs directory exists
OK: The WROLPi main script exists
OK: The WROLPi config file exists

OK: Found wrolpi database at /media/wrolpi/config/wrolpi.db
OK: WROLPi database passes quick_check
OK: WROLPi database is initialized
OK: WROLPi database has files

OK: Controller Python virtual environment exists
OK: WROLPi Controller systemd exists
OK: WROLPi Controller service is up
OK: WROLPi Controller health check passed
OK: WROL Mode is inactive

OK: WROLPi Python virtual environment exists
OK: WROLPi main can be run
OK: Sanic can be run
OK: WROLPi API systemd exists
OK: WROLPi API service is up
OK: WROLPi API echoed correctly

OK: WROLPi app directory exists
OK: WROLPi app exists
OK: WROLPi app systemd exists
OK: WROLPi app service is up
OK: WROLPi app responded with UI

OK: Caddy is installed
OK: Caddy systemd exists
OK: Caddy service is running
OK: Caddy HTTPS proxy responded on :443

OK: Map viewer responded
OK: Map static assets exist
OK: Found 3 PMTiles map files

OK: The kiwix library file exists
OK: Kiwix app responded

OK: The media directory exists
OK: Can modify media directory
OK: Media directory is a mounted drive
OK: Media directory files are served by caddy
OK: Config can be fetched from caddy
OK: Media directory is owned by wrolpi user

OK: Singlefile can be run
OK: readability exists
OK: wget can be run
OK: yt-dlp can be run
OK: Chromium can be run
OK: ffmpeg can be run

OK: Help mkdocs can be run
OK: Help service is running

OK: Can ping 1.1.1.1
OK: Can ping one.one.one.one
```

The output above will help an experienced developer narrow down the cause of an issue.

## Reset

### Reset API Database

The SQLite database at `/media/wrolpi/config/wrolpi.db` contains the tables and indexes which allow you to search or
browse your WROLPi. A script is provided which will delete this database (the API recreates it on next start).
**Warning: you will need to refresh your files!** Run it if the repair script above fails:

`/opt/wrolpi/scripts/reset_api_db.sh`

# Upgrading WROLPi

WROLPi can upgrade itself from the internet. Your library, configs, and database are not touched by an upgrade —
only the WROLPi software in `/opt/wrolpi` is replaced.

Your WROLPi's current version is shown at the bottom of every page, and in the **Settings** page under **Upgrade**.

## Checking for Updates

> Open **Settings**, find the **Upgrade** section, and click **Check for Upgrades**.

When an upgrade is available, a green up-arrow appears in the navigation bar linking to the Upgrade section.

## Upgrading a Raspberry Pi or Debian WROLPi

Both Raspberry Pi and Debian WROLPi's upgrade the same way.

### From the browser (recommended)

1. Open **Settings** and find the **Upgrade** section.
2. Click **Check for Upgrades**, then **Upgrade Now**.
3. Your browser is redirected to the [Controller](../controller/index.md), which stays online during the upgrade so
   you can watch the progress and service logs.
4. When the upgrade completes and all services are running again, you are redirected back to the main interface.

### From the command line

```shell
sudo /bin/bash /opt/wrolpi/upgrade.sh
```

If the upgrade script is missing (very old WROLPi), run the installer instead — it also acts as an upgrade:

```shell
sudo /bin/bash /opt/wrolpi/install.sh
```

### What an upgrade does

1. The Controller is upgraded first, so you can monitor the rest of the upgrade even while other services are down.
2. The API and App services are stopped. **The interface will be unavailable for several minutes.**
3. The latest WROLPi code is downloaded. Every release is **GPG-signed** — the upgrade refuses to install code that
   is not signed by the WROLPi maintainer.
4. Dependencies are upgraded and database migrations are applied.
5. The upgrade finishes by running the [repair script](getting-help.md), then all services are restarted.

**Warning!** The upgrade requires the internet, and discards any manual changes you have made to files in
`/opt/wrolpi`. Your media files and [configs](configs.md) are never touched.

## Upgrading a WROLPi Portable USB

A WROLPi Portable USB is upgraded by re-flashing only the boot portion of the USB drive — your `persistence`
partition (library, database, and configuration) is preserved.

From any Linux computer:

1. Download the new `WROLPi-v*-amd64.iso` from [wrolpi.org](https://wrolpi.org).
2. Plug in your WROLPi Portable USB and identify its device with `lsblk`.
3. Run the upgrade tool from the WROLPi repository:
    * `sudo ./scripts/wrolpi-usb.sh upgrade WROLPi-v<version>-amd64.iso /dev/sdX`
4. Eject the drive and boot it to verify the upgrade.

## Upgrading Docker

In-app upgrades are not available in Docker environments; upgrade the containers manually:

1. `docker-compose stop`
2. `git pull origin master --ff`
3. `docker-compose build --parallel`
4. `docker-compose up -d db`
5. `docker-compose run --rm api db upgrade`
6. `docker-compose up -d`

## If Something Goes Wrong

* The upgrade log is written to `/opt/wrolpi/upgrade.log`, and can be followed live with:
    * `journalctl -fu wrolpi-upgrade.service`
* The [repair script](getting-help.md) is offline-safe and fixes most problems:
    * `sudo /opt/wrolpi/repair.sh`
* Check the health of your WROLPi with:
    * `/opt/wrolpi/help.sh`

See [Getting Help](getting-help.md) for more.

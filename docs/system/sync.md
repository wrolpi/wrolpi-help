# Sync: a Second WROLPi

A **secondary** WROLPi keeps an exact copy of a **primary** WROLPi's library: every file in its media directory (maps
and repositories too), its database, and its Tags, Channels, Domains, Playlists, Downloads and other settings. Use it
for a second copy of your library in another room, another building, or another vehicle.

Every WROLPi is a primary unless you make it a secondary. A primary needs no setup: it is ready to be copied.

> **Warning!** A secondary is overwritten. Every sync replaces its library and database with the primary's, so
> anything you change on a secondary is lost at the next sync. Use the primary for downloading, tagging and
> organizing; use the secondary for reading and watching.

## Before You Start

| Requirement | Why |
|---|---|
| Both WROLPis run the **same version** of WROLPi | The secondary takes the primary's database, which must match its own code. A sync is refused otherwise: upgrade both. |
| The secondary can reach the primary on the network | It reads the primary's web address, and copies files from port **8873** (rsync). |
| The primary's media drive is mounted | An unmounted drive looks like an empty library, so a sync from it is refused. |
| The secondary's drive is as large as the primary's library | Everything is copied, unless you exclude folders (below). |

## Make a WROLPi a Secondary

> On the WROLPi that will be the copy, click **Admin**, then **Sync**. Choose **Secondary** under "This WROLPi
> is", enter the primary's address (for example `https://192.168.0.10`), and click **Save**.

Click **Test Connection** to check that the secondary can reach the primary. Then click **Sync Now** to make the
first copy. The first sync copies the whole library, so it can take many hours; later syncs only copy what changed.

From then on, the secondary shows a "Secondary WROLPi" warning on its pages, and it never downloads anything: the
primary does that.

## When a Sync Runs

A sync runs when you click **Sync Now**, or by itself within a daily window:

> On the Sync page, set **Sync Window Start** and **Sync Window End** (for example 01:00 and 05:00) and click
> **Save**.

Within the window the secondary syncs again 15 minutes after the last sync finished. Leave both times empty to sync
only with **Sync Now**. The window is in WROLPi's timezone (set in **Admin**, **Settings**).

## During a Sync

The secondary is unavailable while it syncs: WROLPi stops its own server so that nothing changes while its library
is replaced. WROLPi shows the sync's progress over every page, with a **Stop Sync** button, and so does the
Controller's page (the secondary's address on port 80, or 8080 in Docker). When the sync finishes, WROLPi starts
again.

A sync in which nothing changed is short: under a minute on a small library, a few minutes on a very large one,
mostly spent comparing files.

A sync is stopped, and WROLPi is started again, if you click **Stop Sync** or if the primary stops answering for
five minutes. A file that was being copied is finished at the next sync.

You get a notification when a sync copied or moved files, or failed. A sync that changed nothing, or that you
stopped, is not announced.

## What Is Copied

Everything in the primary's media directory, including folders the primary
[ignores](../modules/files/index.md#files-tools), and the primary's database. These stay the secondary's own:

| Not copied | Why |
|---|---|
| `wrolpi.yaml` | This WROLPi's own settings (hotspot, timezone, WROL Mode). The settings that describe the library, such as where videos and maps are kept and which directories are ignored, are taken from the primary. |
| `sync.yaml` | This WROLPi's role, its primary, and its sync window. |
| `controller.yaml`, `fstab.yaml`, `smb.conf` | This machine's drives, shares and services. |
| `config/ssl` | This WROLPi's HTTPS certificates. |
| Cookies | Downloader logins are never copied. |
| `config/backup` | This WROLPi's own config backups. |
| `tags` and the playlists directory | Hard links that WROLPi rebuilds when it starts. |

## Files the Primary Deletes

A file the primary deletes, or the old version of a file it changes, is not deleted from the secondary at once. It
is moved to a trash folder, `.sync-trash`, in a folder for the day, and removed after **30 days**:

> On the Sync page, change **Files the primary deletes: Delete after N days**, or check **Never delete them**, and
> click **Save**.

The oldest trash is removed sooner if the secondary's drive is nearly full. To bring a file back, copy it from
`.sync-trash` to the **primary**: restored only on the secondary, it would be moved to the trash again at the next
sync.

## Excluding Folders

To keep a folder of the primary off a smaller secondary:

> On the Sync page, click **Choose Folders**, check the folders not to copy, click **Done**, then **Save**.

Files already copied into an excluded folder are kept; delete them yourself to free space. Because the secondary's
database is the primary's, the files of an excluded folder are still listed on the secondary, but they do not open.

## WROL Mode

Enabling WROL Mode on a secondary stops syncing: a WROLPi in WROL Mode is in use and must not
change under its users. The "Secondary WROLPi" warning is hidden while WROL Mode is enabled. Disable WROL Mode to
sync again.

## Docker

A WROLPi running in Docker can be a primary or a secondary. Its Controller runs the copy in a short-lived
container made from the API's container, so the media directory only needs to be set on the `api` service. The
primary serves its library from a container named `wrolpi-rsyncd-1`, on port 8873.

## Troubleshooting

| Message | What to do |
|---|---|
| "The primary's WROLPi version ... is not this WROLPi's" | Upgrade both WROLPis to the same version. |
| "The primary's database migration ... is not this WROLPi's" | The same: upgrade both. |
| "The primary's media directory is not mounted" | Mount the primary's media drive. |
| "The primary's media directory ... is not this WROLPi's" | Both must use the same media directory path, as their databases name files by their full path. |
| "The primary address is not a primary WROLPi" | The address points at another secondary, or at this WROLPi. |
| rsync failed, or the primary did not answer | Check that the secondary can reach the primary's port 8873, and that the primary is running. |
| "Not enough free space for the primary's database" | Free space on the secondary, or wait for its trash to be removed. |

A secondary can also keep a [Backup Drive](backup.md) of its own.

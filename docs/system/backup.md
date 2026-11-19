# Backup

WROLPi can keep two kinds of copies of your library:

| Copy | Where | Use it for |
|---|---|---|
| A **backup drive** | A second drive plugged into the same WROLPi | Replacing the media drive if it fails |
| A **secondary WROLPi** | Another WROLPi on your network | A second, usable library somewhere else. See [Sync](sync.md). |

They can be combined: a secondary can have a backup drive of its own.

## Backup Drive

A backup drive mirrors your media directory, so if the media drive fails, the backup drive can take its place and
WROLPi starts from it with your files, configs and database.

> Plug in and mount a second drive (see [External USB Drives](external-drives.md)). Click **Admin**, then **Sync**.
> Under **Backup Drive**, choose the drive, and click **Save**.

To back up into a folder on the drive rather than the whole drive, enter it under **Folder on the drive**. Click
**Back Up Now** to make the first copy; it copies the whole library, so it can take many hours.

Backup drives are not available when WROLPi runs in Docker, which cannot reach other drives. Use a
[secondary WROLPi](sync.md) instead.

### When a Backup Runs

A backup runs when you click **Back Up Now**, or by itself within a daily window:

> Under **Backup Drive**, set **Backup Window Start** and **Backup Window End** and click **Save**.

Within the window the backup drive is updated every hour. Leave both times empty to back up only with **Back Up
Now**. WROLPi stays usable while it backs up. **Stop Backup** stops a backup, except while the database is being
copied, which runs to the end.

A backup is only written when the drive you chose is mounted where you chose it. An unplugged drive leaves an empty
folder behind, and WROLPi never fills the system drive with it.

### What Is Copied

Everything in the media directory, except:

| Not copied | Why |
|---|---|
| `tags` and the playlists directory | Hard links that WROLPi rebuilds when it starts. |
| Folders you exclude | See below. |

The database is not copied as a file, which could be caught half-written, but as a consistent snapshot, written
only when it changed since the last backup.

### Files Deleted Here

A file you delete from WROLPi, or the old version of a file that changes, is not deleted from the backup drive at
once. It is moved to a trash folder on the backup drive, `.backup-trash`, in a folder for the day, and removed after
**30 days**:

> Under **Backup Drive**, change **Files deleted here: Delete after N days**, or check **Never delete them**, and
> click **Save**.

The oldest trash is removed sooner if the backup drive is nearly full. A file you deleted by mistake can be copied
back from `.backup-trash` within those days.

> **Warning!** The first backup after upgrading to this version moves every file the media directory no longer has
> into the trash, including any files of your own on the backup drive that are not in the media directory. Keep
> other files off the backup drive, or back up into a folder of their own.

A backup is refused when the media directory is not mounted, or holds no WROLPi library: copied with deletes, an
empty media directory would move the whole backup drive into the trash.

### Excluding Folders

> Under **Backup Drive**, click **Choose Folders**, check the folders not to back up, click **Done**, then
> **Save**.

Files already on the backup drive in an excluded folder are kept; delete them yourself to free space.

### Replacing the Media Drive

If the media drive fails, mount the backup drive at `/media/wrolpi` in its place (see
[External USB Drives](external-drives.md)) and start WROLPi. If you backed up into a folder on the drive, copy
that folder's contents to a new media drive instead. Files in `.backup-trash` are hidden from WROLPi; delete the
folder once you no longer need them.

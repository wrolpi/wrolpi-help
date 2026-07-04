# Tags

A Tag is a named, colored label that you can attach to nearly anything in your WROLPi. Tags are the primary way to
organize your library across all modules. One item can have many Tags, and one Tag can be applied to many items.

You can tag:

* **Files** — any file WROLPi tracks: videos, archives, ebooks, PDFs, images, and so on.
* **Zim entries** — individual pages inside a Zim file (for example, a particular Wikipedia article).
* **Collections** — a Channel, Domain, or Playlist can have a single Tag (see
  [Collections](collections/index.md)).

## Creating and Editing Tags

Tags are managed from the **Dashboard**. The Dashboard shows all of your Tags; click **Edit** to open the Tag editor.

The Tag editor shows every Tag with counts of how many Files, Zims, Channels, and Domains use it. From here you can:

1. **Create** a new Tag by entering a name and choosing a color (or click **Random** for a distinct color). A preview
   shows what the Tag will look like.
2. **Edit** an existing Tag's name or color.
3. **Delete** a Tag using the trash button.

You can also create Tags on the fly wherever the Tag selector appears (file previews, video player, etc.).

### Tag name rules

* Tag names must be unique, and cannot be empty.
* Tag names cannot contain a comma, or file-unsafe characters like `<`, `>`, `:`, `|`, `"`, `?`, `*`, `%`, or `!`.
  This is because Tag names are used as directory names.
* A Tag **cannot be deleted while it is in use**. Remove it from all files, Zim entries, and Collections first.
* Renaming a Tag is safe: WROLPi automatically updates any Downloads that reference the Tag, and moves any Channel
  directories named after the Tag (see [Tagged directories](#tagged-directories) below).

## Tagging Files

Wherever you view a file you can tag it:

> Open any file's preview (or the video player) and use the Tag selector to add or remove Tags.

Other ways to tag files:

* **Bulk tagging**: select many files in the Files browser, then use the bulk tag tool to add or remove Tags on all
  of them in one operation. A progress bar is shown for large batches.
* **Upload**: files can be tagged as they are uploaded.

When deleting files that have Tags, WROLPi will ask for an extra confirmation.

## Tagging Zim Entries

While reading a Zim page (a Wikipedia article, for example) you can tag that specific page using the Tag selector.

If you later replace a Zim file with a newer version (for example, this year's Wikipedia), WROLPi will automatically
migrate your tagged entries to the new Zim file.

## Tagging Collections

A Channel, Domain, or Playlist can be given **one** Tag. When tagging a Collection you can also choose to move its
files into a directory named after the Tag.

### Tagged directories

Tags control where some downloads are stored on disk:

* A tagged Channel's videos are stored in `videos/<tag>/<channel name>/` by default.
* A tagged Playlist's files are stored in `playlists/<tag>/<playlist name>/`.

When you tag (or rename the Tag of) a Channel or Playlist, WROLPi will offer to move the files to the matching
directory, and warns you if the destination conflicts with an existing Collection.

## Searching with Tags

* **Click any Tag label** anywhere in the interface to search for everything with that Tag.
* The search pages (global Search, Files, Archives) have a Tag filter. Selecting multiple Tags finds items that have
  **all** of the selected Tags.
* The **Any** button finds items that have at least one Tag (any Tag at all).
* The Tag selector suggests your **Recent Tags** and **Frequent Tags** (Tags often used together) to speed up
  tagging.

## The Tags Directory

WROLPi maintains a `tags` directory in your media directory (`/media/wrolpi/tags/`). It contains links to every
tagged file, organized into directories named after the Tags. This is the
[secondary](primary-secondary-tertiary.md) way to access your tagged files — it works even if the WROLPi app is
down, and the links survive if you browse the drive on another computer.

If a file has multiple Tags, its links are placed in a directory named with all of its Tags, sorted alphabetically
and separated by commas. For example, a video tagged with "WROL" and "Computers" is linked at
`tags/Computers, WROL/<video files>`. All files of the [FileGroup](filegroups.md) (the video, its poster, captions,
etc.) are linked together.

**Warning!** Do not store your own files in the `tags` directory — it is managed automatically by WROLPi and extra
files will be deleted.

> The Tags Directory can be turned off in the WROLPi Settings (`tags_directory`) if you do not want it.

## Where Tags are Stored

Tags are stored in the `tags.yaml` [config file](configs.md) in your config directory. It records every Tag (with
its color), every tagged file, and every tagged Zim entry. Like all WROLPi configs, this file is the source of
truth:

* Your Tags survive a database rebuild — on startup (or config import) WROLPi re-creates Tags and re-applies them to
  your files.
* You can hand-edit `tags.yaml` (for example, to add a Tag) and WROLPi will apply the change on the next startup or
  import.
* A Tag removed from the config will only be deleted if it is no longer used by anything.

Because `tags.yaml` travels with your media drive, your Tags come along when you move the drive to a new WROLPi.

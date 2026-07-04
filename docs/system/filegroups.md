# How WROLPi Stores Files

Everything in your WROLPi library is a plain file in the [media directory](special-directories.md) — videos, web
page archives, ebooks, Zims, maps. The database is only an index of those files: it can be deleted and rebuilt at
any time from the files on disk and your [configs](configs.md). There is no hidden storage format; you can browse
your entire library with any file manager, on any computer.

## FileGroups

WROLPi groups related files together into a **FileGroup**: files in the *same directory* that share the same name
(stem) are treated as one item in your library.

For example, these four files are one FileGroup, displayed as a single video:

```
videos/WROLPi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi demo.mp4        <- the video (primary file)
videos/WROLPi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi demo.info.json  <- metadata
videos/WROLPi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi demo.en.vtt     <- captions
videos/WROLPi/WROLPi_20230909_0xfMLNVFq2Y_WROLPi demo.jpg        <- poster
```

WROLPi understands multi-part suffixes like `.info.json`, `.readability.html`, `.readability.txt`, and
per-language caption suffixes like `.en.vtt` — they all group with their base file.

Typical FileGroups:

| Kind | Files |
|---|---|
| [Video](../modules/videos/files.md) | `.mp4` + `.info.json` + captions (`.vtt`/`.srt`) + poster image |
| [Archive](../modules/archives/files.md) | SingleFile `.html` + `.readability.html`/`.txt`/`.json` + screenshot |
| eBook | `.epub` or `.mobi` + a cover image |
| Document | a single `.pdf`, `.docx`, comic book, etc. |

### The primary file

Each FileGroup has a **primary file** which decides how the group appears and behaves in the interface. When a group
contains several file types, WROLPi picks the most important one: an archive page, video, or audio file beats an
ebook, an ebook beats a PDF, and images are only primary when nothing else is present. A Video, Archive, or eBook
record is then attached to the FileGroup based on the primary file's type.

Files that share a stem but live in **different directories are not grouped** — a FileGroup never spans directories.

## The File Refresh

The refresh is how WROLPi discovers your files. It scans the media directory, groups files into FileGroups, indexes
their contents for search, and creates the Video/Archive/eBook records.

> To refresh all your files, click the **Files** link in the top navigation bar, then click **Refresh** at the
> bottom of the files table. You can also select specific files or directories and refresh only those.

Things to know about the refresh:

* A brand-new WROLPi has an empty library until the first full refresh completes — the Dashboard will remind you.
* Videos and other downloads refresh their own directories automatically when they complete.
* The refresh refuses to run if the media directory looks empty — this protects your database when a drive failed to
  mount.
* A full refresh of a large library can take a long time; progress is displayed while it runs.

## Indexing and Search

During the refresh, WROLPi extracts searchable text from your files. What is extracted depends on the file type:

* **Videos**: the title, description, and the full caption/subtitle text.
* **Archives**: the page title and the readability article text.
* **eBooks / PDFs / documents**: the title, author, and the document text.
* **Everything else**: at minimum, the words of the file name.

Search offers two modes: the default **fast search** matches titles and other important fields, while **deep
search** also matches the full body text (captions, article contents, document text).

## The Database Can Be Rebuilt

Because the database is derived, deleting it is not a disaster:

* FileGroups, Videos, Archives, and eBooks are rebuilt by a file refresh.
* Everything you curated — [Tags](tags.md), Channels, Playlists, Downloads, settings — is restored from your
  [configs](configs.md).
* Only minor runtime data is lost, such as video watch history.

## Rules to Know

* All files must live inside the media directory (`/media/wrolpi/`). WROLPi cannot see files outside it.
* **Use the [Files module's tools](../modules/files/index.md) to move, rename, or delete files.** The tools keep the
  database and your Tags in sync. If you move or rename a tagged file outside of WROLPi, the Tag can be lost because
  Tags are keyed by the file's path.
* You can add files yourself (over the network, or by plugging the drive into another computer): put them anywhere
  in the media directory, keep sidecar files (posters, captions, metadata) next to their base file with the same
  stem, then run a refresh.
* Directories can be **ignored** from the Files module if you do not want their contents indexed or searchable.
* Never store your own files in the `tags` or `config` directories — see
  [Special Directories](special-directories.md).

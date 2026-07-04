# Downloads

All downloading in WROLPi goes through a single download manager. Whether it is a video, a web page archive, a Zim
file, or map data — everything is queued as a Download, runs in the background, and is visible on the **Downloads**
page.

## Starting a Download

The Download menu offers a form for each kind of download:

* **Videos** — download one or more videos (one URL per line) using yt-dlp. Options include Tags, a destination
  directory, audio-only (with audio format), preferred resolutions, and video format. See
  [Videos](../videos/index.md).
* **Channel/Playlist** — subscribe to a channel or playlist. Options include the download frequency, title
  include/exclude words, download order (newest/oldest), a video count limit, minimum/maximum duration, and a
  Channel Tag. See [Videos](../videos/index.md).
* **Archives** — create a [SingleFile archive](../archives/index.md) of each URL, with readability text and a
  screenshot. Options include Tags, compression, and skipping URLs you have already archived.
* **RSS Feed** — watch an RSS feed and automatically download new entries with either the Video or Archive
  downloader. Options include the frequency and title/URL filters.
* **Files** — download any file from a URL into a directory of your choosing.
* **Scrape** — crawl a web page (up to a chosen depth and page limit) collecting every linked file that matches your
  list of file suffixes (for example `.pdf,.mp4`), then download those files to a destination.

    **Warning!** Scraping can be exponential — each level of depth can multiply the number of pages visited.

[Zim subscriptions](../zim/index.md) and [Map subscriptions](../map/index.md) also create recurring downloads; they
are managed from their own pages but appear in the Downloads page like everything else.

## Once vs Recurring

A Download either runs **once**, or **recurs** on a frequency (hourly up to every 180 days, depending on the type).

* A **Once** download of a Channel/Playlist downloads all of its *current* videos, but will not notice videos added
  later.
* A **recurring** download keeps its schedule slot — a weekly download runs at the same time each week. If your
  WROLPi was powered off past the scheduled time, the most-overdue download runs as soon as possible and the rest
  are spread out to avoid a thundering herd.
* Completed once-downloads are automatically cleaned up after 30 days.

## The Downloads Page

The Downloads page has two tables: **Downloads** (once) and **Recurring Downloads**.

Each download has a status:

| Status | Meaning |
|---|---|
| New | Waiting to be downloaded. |
| Pending | Downloading right now. |
| Complete | Finished successfully. |
| Deferred | Failed, but will be retried automatically (with an increasing back-off). |
| Failed | Failed and will not be retried. |

Things you can do from the tables:

* **Stop** a new/pending download, **Restart** a failed/deferred one, or **Delete** it.
* **Edit** a download (its frequency, filters, destination, etc.).
* Click the red error icon to see the full error message of a failed download.
* Watch live progress (speed and time remaining) of a pending download.
* Bulk **Clear** completed downloads, or **Retry** / **Delete** the selected ones.

**Deleting a download adds its URL to a skip list** so it will not be re-downloaded by an RSS feed or Channel
subscription. You can still download it again by submitting the URL manually.

## When Downloads Run

The download manager checks for work every few seconds, but downloads only run when **all** of these are true:

1. Downloading is enabled (the toggle at the top of the Downloads page).
2. The WROLPi has internet access.
3. WROL Mode is off.
4. A drive is mounted for every download destination (so downloads cannot fill your SD card) — this can be changed
   with the *require media mounted* setting.
5. Your [encrypted cookies](../videos/cookies.md) are unlocked, if you have configured cookies.
6. The current time is inside your configured download window (if you set one).

To be polite to the websites you download from, WROLPi runs at most one download per domain at a time (a few domains
in parallel), and waits between downloads to the same domain.

## Download Settings

The Settings page has a **Download** section:

* **Download on Startup** — enable downloading automatically when WROLPi boots.
* **Wait Between Downloads** — the politeness delay between downloads to the same domain.
* **Download Timeout** — kill any download running longer than this.
* **Daily Download Limits** — cap the number of downloads per domain, and in total, per day.
* **Download Window** — only download between certain hours (overnight windows are supported).
* **Pause downloads when no drive is mounted** and **while cookies are locked** — the safety gates described above.

## Where Downloaded Files Go

Destinations are controlled by templates in the [WROLPi config](../../system/configs.md):

* Videos: `videos/<channel tag>/<channel name>/` — the Channel is created automatically if needed. Videos without a
  channel go to `videos/NO CHANNEL/`.
* Archives: `archive/<domain>/` — the Domain is created automatically.
* Zims: `zims/`, Maps: `map/`.
* Files and Scrape downloads go to the destination directory you choose.

## Failures

* Most errors are **deferred** and retried automatically with an increasing delay. Each downloader gives up for good
  after enough attempts (videos try the hardest).
* If a website blocks WROLPi as a bot (common with YouTube when cookies are missing or stale), all pending downloads
  from that domain are failed at once — see [Encrypted Cookies](../videos/cookies.md) for the fix.
* All of your downloads are stored in the `download_manager.yaml` [config](../../system/configs.md), so your
  subscriptions survive a database rebuild.

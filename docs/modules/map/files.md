# Map Files

The map is drawn from PMTiles files in the map directory of your media directory (`map/`). This page
covers getting those files, how WROLPi decides what each one is, and managing them on the Map's
**Manage** tab.

## Manage Tab

The Manage tab has two sections:

### Map Files

Lists every `.pmtiles` file in the map directory of your media directory (`map/`), including
files in sub-directories. A file in a sub-directory is shown with its directory
(e.g. `extras/infrastructure.pmtiles`). Files can be deleted from here.

| Column      | What it shows |
|-------------|---------------|
| **File**    | The file's path within the map directory, and the name the file gives itself (when it has one). |
| **Type**    | How the map draws the file: **Basemap**, **Overlay**, **Overlay (styled)**, **Terrain**, or **Unreadable**. See [Special File Names](#special-file-names) and [Overlays](overlays.md). |
| **Size**    | The size of the file. |
| **Search**  | Whether a search index exists (basemap files only). |
| **Visible** | Whether the map uses the file. |

#### Visible

Turn off a file's **Visible** toggle to make the map ignore it without deleting it. An ignored file is
not drawn, is not offered in the Layer Control, and its places are not found by search. It stays
in this list so you can turn it back on.

> Ignoring a full planet file makes the map use your regional files again, exactly as if the planet
> file were not there.

The files you ignore are saved in `maps.yaml` (see [How Configs Work](../../system/configs.md)) as their
paths within the map directory. Deleting a file also removes it from `maps.yaml`.

```yaml
ignored_files:
- extras/satellite.pmtiles
```

#### Search

The **Search** column shows whether a search index exists for each basemap file. Overlays and
terrain files have no search index:

- **Built** (green) — A search index exists. Place search is available for this file.
- **Build** (button) — No search index yet. Click to generate one using `tippecanoe-decode`.
  If WROL Mode is not active, the index will also be enriched with region names from Wikidata.

> Search indexes are small SQLite databases (typically 1-4 MB per region) stored alongside
> the PMTiles file with a `.search.db` extension. They are created automatically when you
> download a region via subscriptions, or you can build them manually with the Build button.

### Map Subscriptions

Subscribe to map regions to download them automatically from the WROLPi CDN.

- Browse the catalog of available regions (33 regions covering the entire world, plus terrain)
- Click **Subscribe** to add a region
- Click **View** to preview a region's coverage area on a mini map
- Click **View All Regions** to see all available regions on a world map
- Click **Unsubscribe** to remove a region

Subscribed regions are downloaded via aria2c and automatically renewed every 180 days
to keep your maps up to date.

## How a Subscription Downloads

When you subscribe to a region:

1. WROLPi fetches the map manifest from the CDN and verifies its GPG signature
2. A download is created for each subscribed region
3. aria2c downloads the pre-extracted PMTiles file from the CDN
4. After download, the meta4 file's GPG-signed hash is verified to ensure the file
   is authentic and untampered
5. The file is placed in your map directory with a versioned filename
   (e.g., `us-west-20260329.pmtiles`)
6. A pre-built search index (`.search.db`) is downloaded from the CDN, also with
   GPG-signed hash verification. This provides instant place search with region names.

> Downloads are integrity-verified at multiple levels: the manifest is GPG-signed,
> each file's SHA-256 hash is GPG-signed in its meta4 file, and aria2c verifies
> the hash during download.

## Special File Names

WROLPi reads each PMTiles file to decide how the map draws it. A file is a **basemap** when it
contains the Protomaps layers (`earth`, `water` and `roads`). Any other readable file is an
[overlay](overlays.md). A file which is not a PMTiles file is listed as **Unreadable** and is never drawn.

Some file names are also handled specially:

| Pattern                       | Behavior |
|-------------------------------|----------|
| `planet-*.pmtiles`            | A basemap with this name is a full planet file — used as the sole basemap. Regional extracts and the planet overview are skipped. Overlays and terrain are still drawn. |
| `YYYYMMDD.pmtiles` (8 digits) | Also treated as a full planet file. This is the naming convention used by [Protomaps builds](https://maps.protomaps.com/builds/). |
| `map-overview.pmtiles`        | Low-zoom base layer (zoom 0-6). Provides a global overview when using regional extracts. Not treated as a full planet. |
| `terrain-*.pmtiles`           | Terrain DEM data for hillshade and contour layers. Not loaded as a vector source. |
| Any other basemap             | Regional vector tiles. Multiple regional files render together on the map. |
| Any other file                | An [overlay](overlays.md). |

> Map files can be organized in sub-directories of the map directory. Hidden directories (names
> starting with `.`) are skipped; WROLPi keeps unfinished downloads in one.

## Getting Map Files

### Via Subscriptions (Recommended)

The easiest way to get map files is through **Map Subscriptions** on the Manage tab. WROLPi
hosts pre-extracted regions on a CDN that are downloaded automatically.

### Full Planet File

For complete global coverage, download the full planet file directly from
[Protomaps](https://maps.protomaps.com/builds/) and place it in your map directory.
The planet file is approximately 100-135 GB.

> WROLPi does not host the planet file due to its size. Download it directly from Protomaps.

### Custom Regions with pmtiles CLI

Use the `pmtiles` command-line tool to extract a custom region:

```shell
# Extract a single state (Oregon)
pmtiles extract https://build.protomaps.com/YYYYMMDD.pmtiles /media/wrolpi/map/oregon.pmtiles \
  --bbox="-124.8,42.0,-116.5,46.3"
```

Replace `YYYYMMDD` with the latest build date from the
[Protomaps builds page](https://maps.protomaps.com/builds/).

The `pmtiles extract` command uses HTTP Range Requests to download only the tiles for your
selected region, so you do not need to download the entire planet file.

### Multiple Regions

You can load multiple PMTiles files at once. For example, download separate files for the
contiguous US, Alaska, and Hawaii, and they will all render together on the map.

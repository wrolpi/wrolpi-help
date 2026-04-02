# Map

The Map module displays offline vector maps using MapLibre GL JS and PMTiles files. Maps are rendered
in the browser using your device's GPU, providing fast and smooth navigation with layer control.

The module is powered by [Protomaps](https://protomaps.com/) — an open-source system for
self-hosting vector maps from a single PMTiles file.

## Map Tab

The Map tab displays an interactive map with the following controls:

- **Layer Control** (top-left) — Toggle visibility of map layers: roads, water, buildings,
  land cover, boundaries, labels, hillshade, contours, and more. Your choices are saved
  between sessions.
- **GPS Location** (top-right) — Request your device's GPS position and center the map on it.
- **Zoom & Navigation** (top-right) — Zoom in/out, rotate, and tilt the map.
- **Fullscreen** (top-right) — Expand the map to fill the entire screen.
- **Scale Bar** (bottom-left) — Distance scale. Click to toggle between metric and imperial.
- **Dark/Light Mode** — The map automatically matches your WROLPi theme.

### Context Menu

Right-click (or long-press on mobile) anywhere on the map to open the context menu:

- **Copy Coordinates** — Copy the latitude and longitude to your clipboard.
- **Export PNG** — Save a screenshot of the current map view as a PNG file.
  The filename includes the GPS coordinates of the center of the map.
- **Add Pin** — Place a named pin at that location.

### Sharing Coordinates

The URL updates as you navigate the map, encoding the current position and zoom level:

```
https://your-wrolpi/map?lat=45.5231&lon=-122.6765&z=12
```

Share this URL to link someone directly to a specific location and zoom level.

## Pins Tab

Map pins let you mark and name important locations. Pins are stored in `map_pins.yaml`
in your media directory and persist across restarts.

### Adding Pins

- Right-click (or long-press on mobile) on the map and select **Add Pin**
- Enter a name and optional description

### Managing Pins

The Pins tab shows a table of all your pins with:

- **Filter** — Type to search pins by name
- **Navigate** — Click the location icon to fly the map to that pin
- **Edit** — Change the pin's name or description
- **Delete** — Remove the pin

## Manage Tab

The Manage tab has two sections:

### Map Files

Lists all `.pmtiles` files in your media directory under `/map`. Shows the file name, size,
and modification time. Files can be deleted from here.

### Map Subscriptions

Subscribe to map regions to download them automatically from the WROLPi CDN.

- Browse the catalog of available regions (33 regions covering the entire world, plus terrain)
- Click **Subscribe** to add a region
- Click **View** to preview a region's coverage area on a mini map
- Click **View All Regions** to see all available regions on a world map
- Click **Unsubscribe** to remove a region

Subscribed regions are downloaded via aria2c and automatically renewed every 180 days
to keep your maps up to date.

## Map Subscriptions

When you subscribe to a region:

1. WROLPi fetches the map manifest from the CDN and verifies its GPG signature
2. A download is created for each subscribed region
3. aria2c downloads the pre-extracted PMTiles file from the CDN
4. After download, the meta4 file's GPG-signed hash is verified to ensure the file
   is authentic and untampered
5. The file is placed in your map directory with a versioned filename
   (e.g., `us-west-20260329.pmtiles`)

> Downloads are integrity-verified at multiple levels: the manifest is GPG-signed,
> each file's SHA-256 hash is GPG-signed in its meta4 file, and aria2c verifies
> the hash during download.

## Special File Names

The map viewer detects certain file name patterns and handles them differently:

| Pattern                       | Behavior |
|-------------------------------|----------|
| `planet-*.pmtiles`            | Full planet file — used as the sole vector source. Regional extracts and the planet overview are skipped. |
| `YYYYMMDD.pmtiles` (8 digits) | Also treated as a full planet file. This is the naming convention used by [Protomaps builds](https://maps.protomaps.com/builds/). |
| `map-overview.pmtiles`        | Low-zoom base layer (zoom 0-6). Provides a global overview when using regional extracts. Not treated as a full planet. |
| `terrain-*.pmtiles`           | Terrain DEM data for hillshade and contour layers. Not loaded as a vector source. |
| Everything else               | Regional vector tiles. Multiple regional files render together on the map. |

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

## Terrain

The map supports hillshade and contour overlays when a terrain file is available.

### Downloading

You can download map terrain files from [Mapterhorn](https://mapterhorn.com/data-access/)

### Setup

Place a terrain PMTiles file (DEM data in Terrarium encoding) in your map directory.
The file name must start with `terrain-` (e.g., `terrain-z0-8.pmtiles`).

You can subscribe to the **Terrain** region on the Manage tab to download the terrain file
automatically.

### Using Terrain Layers

Once a terrain file is detected, two additional layer groups appear in the Layer Control:

- **Hillshade** — Shaded relief showing elevation changes. Hidden by default.
- **Contours** — Elevation contour lines with labels. Hidden by default. Labels show
  elevation in meters or feet depending on the scale bar setting (click the scale bar to toggle).

> Terrain layers are hidden by default to keep the map clean. Enable them in the Layer Control
> when you need elevation information.

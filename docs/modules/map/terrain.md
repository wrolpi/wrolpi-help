# Terrain

The map supports hillshade and contour overlays when a terrain file is available.

## Downloading

You can download map terrain files from [Mapterhorn](https://mapterhorn.com/data-access/)

## Setup

Place a terrain PMTiles file (DEM data in Terrarium encoding) in your map directory.
The file name must start with `terrain-` (e.g., `terrain-z0-8.pmtiles`).

You can subscribe to the **Terrain** region on the [Manage tab](files.md#map-subscriptions) to download
the terrain file automatically.

## Using Terrain Layers

Once a terrain file is detected, two additional layer groups appear in the Layer Control:

- **Hillshade** — Shaded relief showing elevation changes. Hidden by default.
- **Contours** — Elevation contour lines with labels. Hidden by default. Labels show
  elevation in meters or feet depending on the scale bar setting (click the scale bar to toggle).

> Terrain layers are hidden by default to keep the map clean. Enable them in the Layer Control
> when you need elevation information.

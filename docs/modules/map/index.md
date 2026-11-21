# Map

The Map module displays offline vector maps using MapLibre GL JS and PMTiles files. Maps are rendered
in the browser using your device's GPU, providing fast and smooth navigation with layer control.

The module is powered by [Protomaps](https://protomaps.com/) — an open-source system for
self-hosting vector maps from a single PMTiles file.

## More About the Map

| Page | What it covers |
|------|----------------|
| [Map Files](files.md) | Getting map files, subscriptions, the Manage tab, and how file names are handled. |
| [Terrain](terrain.md) | Hillshade and contour lines. |
| [Overlays](overlays.md) | Drawing your own data over the map: power lines, trails, imagery, and their styles and icons. |
| [Exporting a Map as a PDF](export.md) | Printing a 1:24,000 topographic sheet, or carrying it on a phone. |

## Map Tab

The Map tab displays an interactive map with the following controls:

- **Layer Control** (top-left) — Toggle visibility of map layers: roads, water, buildings,
  land cover, boundaries, labels, [hillshade, contours](terrain.md), and more. Your choices are saved
  between sessions. [Overlays](overlays.md) are listed here too.
- **GPS Location** (top-right) — Request your device's GPS position and center the map on it.
- **Zoom & Navigation** (top-right) — Zoom in/out, rotate, and tilt the map.
- **Fullscreen** (top-right) — Expand the map to fill the entire screen.
- **Export** (top-right, the printer) — Make a PDF of a 1:24,000 topographic sheet. See
  [Exporting a Map as a PDF](export.md).
- **Scale Bar** (bottom-left) — Distance scale. Click to toggle between metric and imperial.
- **Dark/Light Mode** — The map automatically matches your WROLPi theme.

### Context Menu

Right-click (or long-press on mobile) anywhere on the map to open the context menu:

- **Copy Coordinates** — Copy the latitude and longitude to your clipboard.
- **Export PNG** — Save a screenshot of the current map view as a PNG file.
  The filename includes the GPS coordinates of the center of the map.
- **Export a 1:24,000 map** — Start a [PDF export](export.md) with the quadrangle
  you clicked already chosen.
- **Add Pin** — Place a named pin at that location.

### Sharing Coordinates

The URL updates as you navigate the map, encoding the current position and zoom level:

```
https://your-wrolpi/map?lat=45.5231&lon=-122.6765&z=12
```

Share this URL to link someone directly to a specific location and zoom level.

### Search

Type in the search box at the top center of the map to find places by name.

- **Place search** — Type a city, town, park, or region name. Results appear in a dropdown
  showing the place name, administrative region (e.g., "Oregon"), and population.
- **Coordinate search** — Type coordinates like `45.5, -122.6` to navigate directly to
  that location.
- **Proximity bias** — Results are sorted by proximity to your current map view, so nearby
  places appear first.
- **Prefix matching** — Typing partial names works (e.g., "Port" finds "Portland").
- **Fuzzy fallback** — If no exact match is found, a broader substring search is attempted.

Click a result to fly to that location with a marker and popup. Press Escape to close the
dropdown.

> Search data is extracted from the same PMTiles map files you already have. No additional
> downloads are needed. When search indexes include Wikidata enrichment, results show
> administrative regions (state/province) to help distinguish places with the same name.

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

The Manage tab lists your map files and your map subscriptions. See [Map Files](files.md).

## Global Search

Map places also appear in WROLPi's global search. When you search from the navigation bar:

- The **Map** tab shows the number of matching map places alongside Files, Zims, and Other
- Clicking the Map tab displays results as cards with mini map previews showing each location
- Click a card to navigate to that location on the map page
- Results are paginated (12 per page) with the same region and population information

## Standalone Map Viewer

WROLPi also serves the map by itself on port `:8084` (`https://your-wrolpi:8084`), which keeps working
when the main app is unavailable. It shows the same map files, [overlays](overlays.md), styles and icons, with its own layer panel. Its
choices are remembered separately from the main map's. It can not [export a PDF](export.md).

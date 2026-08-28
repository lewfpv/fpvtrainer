# Blender tracks

The visual **Pályaválasztó** is generated from `tracks.json`. Merely copying a
GLB into this directory does not add it to the menu: create a matching metadata
entry as well.

Each track entry uses these fields:

- `trackname`: name shown below the thumbnail
- `filename`: GLB/glTF file in this directory
- `skybox_file`: relative path to a skybox, or `null`
- `desc`: short card description
- `size`: displayed download size in MB
- `scale`: uniform scale applied to the complete track (`1` = original size)

Example:

```json
{
  "trackname": "Tiny House",
  "filename": "tinyhouse.glb",
  "skybox_file": "skyboxes/skybox01.hdr",
  "desc": "Small indoor track.",
  "size": 7.51,
  "scale": 1
}
```

`scale` changes the rendered track, collision meshes, gates and `DroneSpawn`
together. For example, use `0.125` to reduce a 20-metre object to 2.5 metres.
Only positive values are accepted; an omitted or invalid value defaults to `1`.

## Tiny Drones public imports

Under local `npm run dev`, the track selector can send a
`https://tinydrones.eu/trackeditor/view/<token>` public link to the development
API. It generates a performance-merged GLB, stores it as
`TD_<TRACK_NAME>.glb`, and upserts its `tracks.json` entry. Imported metadata
also records `source_format`, `source_url`, and `imported_at`.

Public Tiny Drones responses can omit private referenced gate assemblies. Such
placements are preserved as red physical placeholder frames at the original
position and rotation, and their count is included in the card description.

The GitHub Pages UI does not expose the importer, and the standalone production
Node server rejects the write/convert endpoint. Run `npm run build:pages` after
local imports to copy the generated GLBs into the static `release` build.

Track thumbnails belong in `thumbnails`. Their base name must match the track
file, for example `tinyhouse.glb` uses `thumbnails/tinyhouse.webp`. Supported
formats: `.webp`, `.jpg`, `.jpeg`, `.png`. Missing images use a placeholder.

Skyboxes belong in `skyboxes` and are referenced explicitly by `skybox_file`.
Supported formats: `.hdr`, `.jpg`, `.jpeg`, `.png`, `.webp`.

Required Blender conventions:

- glTF Binary (`.glb`)
- Metric units, 1 Blender unit = 1 meter
- Floor top at Blender `Z = 0`
- Optional Empty named exactly `DroneSpawn`
- Apply object scale and rotation before exporting
- Keep textures embedded

Blender lights can be used instead of the simulator's built-in lighting. Enable
**Punctual Lights** during export and **Blender fényforrások** in the simulator.
glTF supports `SUN`, `POINT`, and `SPOT`; standard `AREA` lights are unsupported.

Skybox visibility and skybox reflections are separate settings. Reflections on
track materials are disabled by default.

Imported render meshes receive static Ammo triangle-mesh collision automatically.

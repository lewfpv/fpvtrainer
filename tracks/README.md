# Blender tracks

Export Blender tracks to this directory as `.glb` or `.gltf` files. They are listed automatically in the **Pályaválasztó** menu. The preferred first-start file is:

`default.glb`

Required conventions:

- glTF Binary (`.glb`)
- Metric units, 1 Blender unit = 1 meter
- Floor top at Blender `Z = 0`
- Optional Empty named exactly `DroneSpawn` for the start position and orientation
- Apply object scale and rotation before exporting
- Keep textures embedded
- Exclude Blender cameras and lights

Blender World nodes are not exported to glTF/GLB. To add an equirectangular skybox, place a separate 2:1 image next to the track using the track base name plus `_skybox`, for example:

- `default.glb`
- `default_skybox.jpg`

Supported skybox formats: `.hdr`, `.jpg`, `.jpeg`, `.png`, `.webp`. The skybox can be toggled in **Pályabeállítások**.

If no listed track can be loaded, the simulator uses its primitive fallback track.

Imported render meshes receive static Ammo triangle-mesh collision automatically.

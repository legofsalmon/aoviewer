# AO Viewer – Resolume Arena Advanced Output viewer

A single-file, dependency-free web page that visualises Resolume Arena
Advanced Output presets (`.xml`). Hosted at <https://aoviewer.letissier.ie>.

## Use

Open the page and drop a preset onto it (or use **Open XML…**). Nothing is uploaded;
the file is parsed in your browser. Presets live in
`~/Documents/Resolume Arena/Presets/Advanced Output/`; the live setup is
`~/Documents/Resolume Arena/Preferences/AdvancedOutput.xml` (also supported).

**Watch file** (Chrome / Edge, via the File System Access API) picks a file once and
re-reads it whenever it changes on disk, keeping your pan/zoom and selection. Point it at
`Preferences/AdvancedOutput.xml` to follow the setup Resolume is currently outputting; the
map refreshes a second or so after Resolume saves. Safari and Firefox don't support this
and simply don't show the button.

`index.html` also works straight from disk. `?file=name.xml` loads an XML file hosted
next to the page on start.

## What it shows

- **Input map** – every slice's input rectangle drawn on the composition.
- **One output map per screen** – slice output quads, masks, and (when a slice is
  selected) its warp mesh. Screens show their output device, resolution and state.
- **Sidebar** – screens and slices with source, size, enabled state and warnings
  (outside bounds, not 1:1 scale, edited warp). Hover for details, click to pin,
  eye icons hide items in the views.
- **Export PNG** – renders a view as a full-resolution test card (checkerboard per
  slice with name, position and size), for the input map or any screen.

Drag to pan, ⌘/Ctrl + wheel (or trackpad pinch) to zoom, or use the + / − buttons; double-click to fit. `F` fits all views, `Esc` clears the selection.

## Deploy

Static site, no build step: point Vercel (or any static host) at the repo root.

## Notes on the file format

- Only slice geometry, sources and flags are read; colour/brightness params are ignored.
- Input source codes were inferred from real presets and compositions:
  `0:1` = Composition, `1:N` = Group N, `3:N` = Layer N. Anything else is shown raw.
- Bézier point mode is rendered as cubic Bézier patches; linear mode as straight segments.

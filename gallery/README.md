# Theme gallery

The app's **Online** button (Themes tab) reads `gallery/index.json` from this repository's `main` branch
(`https://raw.githubusercontent.com/vitcox/RigCanvas/main/gallery/index.json`). Settings → Paths → "Online theme gallery"
can point it at any other `index.json` URL or a local folder.

Each theme is a `.tlcd` package (layout, pictures / videos, custom fonts) with a `.jpg` preview next to it. Previews are
rendered with sample readings; on your screen the themes show your own hardware names and values.

## Sending a theme

Open an [issue](https://github.com/vitcox/RigCanvas/issues) and attach the theme exported from the app as a `.tlcd` file
(Themes tab → Export), with a sentence about it.

## Index format

```json
{
  "version": 1,
  "themes": [
    {
      "name": "Synthwave Drive",
      "author": "RigCanvas",
      "description": "Short text shown on the card",
      "descriptionPl": "Polish card text (optional; the English one is shown when it is empty)",
      "file": "SynthwaveDrive.tlcd",
      "thumbnail": "SynthwaveDrive.jpg",
      "tags": ["animated", "retro", "gaming"]
    }
  ]
}
```

`file` and `thumbnail` are relative to `index.json` (or absolute `https://` links). Downloads must be `.tlcd` or `.lcdtheme`
over HTTPS, at most 200 MB; packages are limited to 500 entries / 512 MB unpacked and only pictures and videos are
extracted from their `assets/` folder.

Tags become filter chips in the gallery window. The app translates these: `animated`, `dashboard`, `gaming`, `clock`,
`weather`, `music`, `graphs`, `minimal`, `light`, `retro`, `neon`, `scifi`, `nature`, `elegant`, `playful`, `seasonal`,
`panel` (full-screen panels for playlists). Other tags are shown as written.

`RigCanvas.exe gallery-index <folder>` (from an administrator terminal) rebuilds `index.json` for the `.tlcd` files in a
folder. It keeps the descriptions, tags and pictures already in the index, and extracts the package's own preview for a
new theme.

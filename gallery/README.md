# Theme gallery

The app's **Online** button (gallery page) reads `gallery/index.json` from this repository's `main` branch
(`https://raw.githubusercontent.com/<owner>/<repo>/main/gallery/index.json`). Settings → Paths → "Online theme gallery"
can point it at any other `index.json` URL or a local folder.

## Adding a theme

1. In the app, export the theme as a `.tlcd` package (gallery → Export, or the editor's Export button).
2. Put the `.tlcd` into this folder.
3. Run `RigCanvas.exe gallery-index gallery` from an administrator terminal: it writes `index.json`
   and extracts each package's thumbnail next to it as `<name>.png`.
4. Optionally fill in `description` and `tags` in `index.json`, then commit.

Thumbnails are rendered from your own PC when exporting, so labels such as `{gpu.name}` show your hardware.

## Index format

```json
{
  "version": 1,
  "themes": [
    {
      "name": "Neon Pulse",
      "author": "someone",
      "description": "Short text shown on the card",
      "file": "NeonPulse.tlcd",
      "thumbnail": "NeonPulse.png",
      "tags": ["dark", "gpu"]
    }
  ]
}
```

`file` and `thumbnail` are relative to `index.json` (or absolute `https://` links). Downloads must be `.tlcd` or `.lcdtheme`
over HTTPS, at most 200 MB; packages are limited to 500 entries / 512 MB unpacked and only pictures and videos are
extracted from their `assets/` folder.

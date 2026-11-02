# Theme guide

[← Back to the README](../README.md) · [User guide](user-guide.md) · [Sensor reference](sensors.md) · [Troubleshooting](troubleshooting.md)

Everything you need to build, change and share themes for RigCanvas.

## Your first theme in five minutes

1. In the **Themes** tab, select a theme close to what you want and click **Duplicate** (or **New blank** to start empty).
2. Open the **Editor** tab. Add widgets with the buttons above the preview, or insert a ready-made block from **Templates**.
3. Drag widgets on the preview; set the sensor, colors and font in the inspector on the right.
4. **Save** (Ctrl+S). The dot on the Save button means there are unsaved changes; **Discard changes** goes back to the last save.

The preview is live: with the LCD running, the screen shows your changes as you make them.

## Canvas basics
- The canvas is **480 × 854 px**, portrait. The panel is mounted sideways; the app rotates frames for it.
- Positions are pixels from the top-left corner. Every widget has `X`, `Y`, `Width` and `Height`.
- Widgets are drawn in layer order, the top of the layer list on top. Background panels usually sit at the bottom and are **locked**, so clicks reach the widgets above them.
- Text shrinks to fit its box, so long values are never cut off. Make boxes about 1.7 × the font size tall.

## Working in the editor

| Action | How |
|---|---|
| Select several | Ctrl+click or Shift+click; Ctrl+A selects all; clicking a group in the layer list selects the whole group |
| Move by 1 px / 10 px | Arrow keys / Shift + arrow keys |
| Snap | **Guides** snap to the edges and centers of other widgets (hold Alt to move freely); **Snap to grid** snaps to a 2–20 px grid shown on the preview |
| Zoom | Ctrl + mouse wheel; drag with the right or middle mouse button to pan |
| Duplicate, delete | Ctrl+D, Delete |
| Lock / unlock | Ctrl+L |
| Group | Ctrl+G |
| Copy, cut, paste | Ctrl+C, Ctrl+X, Ctrl+V (also between themes) |
| Undo, redo | Ctrl+Z, Ctrl+Y |
| Deselect | Esc (the inspector then edits the [theme itself](#theme-options)) |

Leaving the editor with unsaved changes asks whether to save, discard or stay; so does closing the app.

## Widget types

| Type | Shows | Key properties |
|---|---|---|
| **Data text** | One sensor value | Sensor, number format, prefix / suffix, thresholds or color scale |
| **Clock / date** | Time, date or weekday | `clock.time`, `clock.time.short`, `clock.date`, `clock.day` |
| **Label** | Fixed text with optional [placeholders](#placeholders) | Text |
| **Sensor tile** | Card with a label, a big value, a status stripe and an optional mini graph | Sensor, label, sparkline, thresholds |
| **Bar** | Progress bar | Sensor, min / max, start and end color, track, vertical, LED segments |
| **Gauge** | Round gauge | Style (arc / LED segments / needle), start angle, sweep, thickness, segment count |
| **Graph** | History graph | Sensor, optional second series, time window **30 s – 24 h**, style (filled line / bars), min / max markers, auto scale |
| **Panel** | Background card | Flat or gradient fill, border, corner radius |
| **Image / GIF** | Picture, animated GIF, video or the **album cover** of what's playing | File (`media:cover` = album art), opacity |
| **Audio spectrum** | Live spectrum of the PC's sound | Style (bars / mirror / wave / circle), bands, LED segments, falling peaks |
| **Weather icon** | Drawn weather symbol | A `weather.*code` sensor; sun / cloud / rain colors |
| **Analog clock** | Dial with hands | Seconds hand, numbers |
| **Calendar** | This month, today marked | Colors, font |
| **Countdown** | Time left until a date | Target `yyyy-MM-dd [HH:mm]` or `MM-dd` (every year); style (days + hours + minutes / days / clock) |
| **Ticker** | Text that scrolls sideways when it doesn't fit | Text with placeholders, speed (px/s) |
| **Sci-fi reactor** | Animated rotating rings | Outer / inner color |

**Gauge angles** are in degrees, clockwise from 3 o'clock. Common setups: **270°** (start 135), **240° speedometer** (start 150), **180° half circle** (start 180), **360°** (start 270).

**Graph windows** up to 5 minutes use live samples. Longer windows (15 min, 1 h, 6 h, 24 h) show one average per minute, kept across restarts, so a 24 h graph is full the next day too.

## Theme options

With nothing selected (Esc), the inspector edits the theme itself:
- **Background:** a color, plus an optional picture, GIF or video (MP4, MOV, WMV, AVI, MKV). You choose the crop, rotation and frame rate once and the file is converted to the screen size, so playback stays light. Fit, opacity and dimming keep the data readable on top.
- **Smooth value changes:** bars, gauges and numbers glide to new readings (extra frames are drawn only while something moves).
- **How the theme appears on the LCD:** instantly, fading from black, or revealed from the top.
- **Grid:** a decorative grid drawn on the LCD, with its own color and spacing. This is separate from the editor's *Snap to grid*, which is never sent to the screen.

## Placeholders
Label and ticker text can contain `{sensor.key}` tokens, replaced with live values:

```
{gpu.name}            NVIDIA GeForce RTX 5070 Ti
{gpu.model|upper}     RTX 5070 TI
{cpu.model}           Ryzen 7 5800X3D
CPU {cpu.temp}°C      CPU 57°C
{media.artist} – {media.title}
```

- Modifiers: `|upper`, `|lower`.
- Any key from the [sensor reference](sensors.md) works, raw keys included: `{lhm:Nuvoton NCT6798D/Fan/Fan #3}`, `{hwi:CPU Package Power}`.
- A known sensor without a reading right now (no game running, nothing playing) shows `--`. Braces that aren't a sensor key stay as typed, so typos are easy to spot.
- In a **ticker**, separate parts with `·`. A part whose placeholders are all empty is skipped: `♪ {media.artist} – {media.title}  ·  GPU {gpu.temp}°C` shows only the GPU part while nothing plays.

> **Never type your own hardware model into a label.** Use `{cpu.model}` / `{gpu.model}` so the theme looks right on everyone's PC.

## Number formats
Data text uses .NET format strings: `{0:F0}` → `57`, `{0:F1}` → `57.3`, `{0:F2}` → `4.35`. The prefix and suffix go around the value (`°C`, ` W`, ` GB`, `%` …).

## Color thresholds
Data text, bars and gauges can change color with the value:

| Value | Color |
|---|---|
| more than 5 below *Warning from* | normal color |
| the last 5 units before *Warning from* | smooth blend into the warning color |
| from *Warning from* | warning color |
| from *Critical from* | critical color, optionally **pulsing** |

LED-segment gauges color each segment by the value it stands for, giving the classic green → amber → red speedometer. Typical limits: CPU 75 / 88 °C, GPU 72 / 84 °C.

## Color scale
Instead of thresholds, a value can follow a **color scale**: any number of stops in % of Min..Max, smooth or stepped, with presets (cool → hot, green → red, rainbow, fire, ice, neon, toxic). Bars and arcs can spread the whole scale along the track, LED gauges color each segment by its value, and graphs color the line by height. A color scale wins over thresholds.

## Templates
**Templates** (next to the widget buttons) inserts ready-made blocks: GPU card, CPU card, clock with date, now playing (cover + spectrum), network (tiles + graph), weather now. Your own: select widgets → **Save the selection as a template…**. Inserted blocks arrive as their own group.

## Groups
A **group** is a folder in the layer list. Set it with the *Group* field or Ctrl+G; a group can be selected, hidden or locked in one click. **✨ Auto** groups widgets by the first word of their name (`GPU …`, `CPU …`).

## Fonts
Any installed font works, but for themes you share, stick to fonts that ship with Windows 10 and 11: Segoe UI (Light, Semilight, Semibold, Black), Bahnschrift (Light, SemiLight, SemiBold, Condensed), Consolas, Lucida Console, Georgia, Palatino Linotype, Constantia, Candara, Corbel, Trebuchet MS, Impact, Arial Black, Courier New.

For anything else, click **+ .ttf** next to the font picker. The font (`.ttf` or `.otf`) is copied into the library and packed into `.tlcd` exports, so it shows up on other PCs too.

## Sharing: `.tlcd` packages
**Export** (in the Themes tab or the editor) saves a `.tlcd` package, a zip with:

```
theme.json        the layout; picture paths rewritten to "assets/…"
assets/…          every picture, GIF and video the theme uses
fonts/…           custom fonts the theme uses
thumbnail.png     240 × 427 preview
```

To install one, drop it onto the theme library, or open **Online** and paste its https link. Pictures, videos and fonts go into the library's `assets/` and `fonts/` folders. Choosing `.lcdtheme` when exporting saves just the layout, without pictures or fonts.

**Want your theme in the online gallery?** Open an [issue](https://github.com/vitcox/RigCanvas/issues) and attach the `.tlcd` file.

## Where themes live
`%AppData%\RigCanvas\Themes` by default (**Settings → Paths → Theme library**):

```
*.lcdtheme   your themes and the built-in ones
fonts/       custom fonts
assets/      pictures and videos
_legacy/     built-in themes replaced by a newer version (kept, not loaded)
```

Built-in themes are installed once, by the app version that adds or changes them. If you delete one, it stays deleted.

## Tips
- Use placeholders and the built-in fonts, and your theme works on any PC.
- Check a theme on the real screen: colors and thin lines look different on the LCD than on a monitor.

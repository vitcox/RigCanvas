# User guide

[← Back to the README](../README.md) · [Theme guide](themes.md) · [Sensor reference](sensors.md) · [Troubleshooting](troubleshooting.md)

How to use RigCanvas day to day, from the first start to playlists, alerts and automatic themes. To build your own themes, see the [theme guide](themes.md).

## The window

The app has three tabs:

| Tab | What it's for |
|---|---|
| **Themes** | Your theme library: pick what the LCD shows, search, sort into categories, get more themes **Online**, build a playlist |
| **Editor** | Change the selected theme on a live preview ([theme guide](themes.md)) |
| **Settings** | Screen, sensors, weather, alerts, automatic theme, startup and updates |

The **Start LCD screen** button (also in the tray menu) sends the selected theme to the screen. While it runs, the status bar shows the frame rate and the connection, e.g. `LCD FPS: 10.0 · native USB`.

## First start

A short wizard checks that the screen is connected and that [PawnIO](https://pawnio.eu/) is installed (it's needed for the CPU temperature and motherboard fans), then lets you choose the language, the [interface theme](#interface-theme-and-accent-color), a first theme, how the app starts (with Windows, in the tray) and, optionally, a place for the weather. Everything it sets can be changed later in **Settings**, and **Settings → Updates and about → Setup wizard…** runs it again.

## Interface theme and accent color

**Settings → Appearance and language** changes how the app itself looks (the LCD themes are separate):

- **Interface theme:** Dark, Light, OLED Black, Catppuccin (Mocha, Macchiato, Frappé, Latte), Nord, Dracula, Tokyo Night, Gruvbox Dark, Rosé Pine or Solarized Light. The list shows each theme's colors, and the window switches as soon as you pick one.
- **Follow Windows light / dark mode:** instead of one theme, choose one *When Windows is light* and one *When Windows is dark*, e.g. Solarized Light and Catppuccin Mocha. The app switches as soon as Windows does (Settings → Personalization → Colors in Windows).
- **Accent color:** the color of buttons, selections, sliders and switches, on top of any interface theme. *From the interface theme* keeps the theme's own accent. Accents are adjusted automatically so text stays readable on light and dark themes.

Click **Save settings** to keep your choice; **Discard changes** goes back.

## Choosing a theme

Click a theme in the **Themes** tab to show it on the LCD. The library has:

- **Search** by name, and a **category** list: Dark, Light, Panels, Single value, Mine, plus your own folders. To create a folder, type a new name in a theme's *Category* box.
- **Online**: the online gallery with over 90 more themes. Filter them by tag, then **Add to library**. **Hide the ones in the library** shows only themes you don't have yet.
- **Duplicate** before you change a built-in theme a lot, so the original stays.
- **Export** saves a theme as a `.tlcd` package to share. To install a `.tlcd` file, drop it onto the library.

## Playlists

Switch the library from **Single theme** to **Playlist** to let the LCD cycle through several themes:

1. Select a theme and click **+ Add selected** (or **+ All**). A theme can appear more than once.
2. Set how many seconds each one stays on screen (3–3600).
3. **Cross-fade** blends one theme into the next.

**Save…** / **Load…** keep playlists as `.lcdplaylist` files. A few ready-made playlists come with the app.

## Automatic theme

**Settings → Automatic theme** switches to a different theme while something is going on, then goes back to the playlist or your normal theme. Each rule has a condition and a theme:

| Condition | Example |
|---|---|
| Between times | A dim clock theme from 23:00 to 07:00 |
| Music is playing | A music theme with album art and a spectrum |
| A game is running | A game theme with FPS (needs RivaTuner Statistics Server) |
| Sensor above / below | A GPU-focused theme while `gpu.load` is above 80 % |
| An alert is active | A full-screen warning theme |

- The condition must hold for the set number of seconds (*after (s)*) before the theme switches, so a short spike doesn't flip it.
- *Go back (s) after the condition ends* sets how long the theme stays afterwards.
- The **first matching rule** in the list wins, so put the most important one at the top.
- Automatic themes win over the playlist and over the theme you picked.

## Alerts

**Settings → Alerts** warns you when a sensor crosses a limit, for example a GPU over 85 °C or a pump that stopped.

- Each alert has a sensor, *above* or *below*, a limit and a time (*for (s)*) the value has to stay past the limit. That avoids false alarms from a single reading.
- *Below* alerts (fans, pump) only arm after the sensor has been above the limit once, so a fan that isn't connected never alarms.
- **On the LCD:** a bottom banner with a flashing frame, the full screen, or just the flashing frame. *Text on the LCD* replaces the sensor name in the message.
- **Windows notification (tray)** also shows a notification on the desktop.
- **Show a test** previews the alert on the screen.

## Weather

**Settings → Weather** shows local weather in any theme with weather widgets (the built-in *Panel 09 · Weather*, or the weather themes in the online gallery).

1. Type a place and click **Search** (or press Enter).
2. If several places share the name (Southampton is in the UK and in the US), pick the right one. The list shows the region, country and population.
3. The current weather appears as a check. Click **Save**.

You can also type coordinates as `lat, lon`. Weather comes from [Open-Meteo](https://open-meteo.com/): no account or key, and only the place is sent. An empty field turns weather off. Choose °F and the refresh interval on the same page.

## Screen brightness and blanking

**Settings → LCD screen:**

- **Screen brightness** applies right away. The panel has no backlight control, so the picture is darkened before it's sent; Thermalright's own software does the same.
- **Dim at night** uses a second brightness between two times.
- **Blank the LCD when the PC is locked, asleep or the monitor is off.**
- **Max FPS** limits animations. Static themes refresh only when a value changes, so they cost almost nothing.

## Starting with Windows and the tray

**Settings → Startup and window:**

- **Start with Windows** uses a scheduled task with administrator rights, so Windows doesn't ask for permission at every logon.
- **Start minimized to the tray** starts with the tray icon only, no window.
- **Turn the LCD on automatically at startup** shows the last theme right away.
- **Minimize to the tray** and **The ✕ button hides to the tray** keep the app running in the background.

Double-click the tray icon, or start the app again, to bring the window back. Only one copy runs at a time.

## Keyboard shortcuts

**Settings → Keyboard shortcuts** (off until you turn them on) work anywhere in Windows, also in a game and while the app is in the tray:

| Action | Default |
|---|---|
| Next theme (or the next playlist item) | Ctrl+Alt+PageDown |
| Previous theme | Ctrl+Alt+PageUp |
| Turn the LCD off / on | Ctrl+Alt+End |

To change one, click its box and press the keys; Backspace clears it. With a single theme, next / previous go through the library as the category filter shows it. If another program already uses a combination, the settings page says so.

## Updates

With **Check for updates at startup** on (**Settings → Updates and about**), the app looks for a new release on GitHub and offers to install it. **Check for updates** does it on demand. The update downloads the installer from this repository's releases and restarts the app; your settings and themes stay.

## Your data and backups

Everything the app stores is in `%AppData%\RigCanvas`. **Settings → Updates and about** shows the exact folder.

| Path | Contents |
|---|---|
| `settings.json` | All settings |
| `Themes\` | Your themes and the built-in ones (`.lcdtheme`), with `fonts\` and `assets\` |
| `Playlists\` | Saved playlists |
| `history.bin` | One average per minute for the last 24 hours, for long graphs |
| `logs\app.log` | Diagnostics log (screen connection, power events) |

To back up your setup, copy the whole folder while the app is closed (tray → **Exit**). To take a theme to another PC, **Export** it as a `.tlcd` package: it carries its pictures and fonts.

When you uninstall, the uninstaller asks whether to keep this folder.

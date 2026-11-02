# Security policy

RigCanvas runs with administrator rights (hardware sensors and the USB screen need them), so security reports are taken seriously.

## Reporting a vulnerability
Please **do not open a public issue**. Use GitHub's [private vulnerability reporting](https://github.com/vitcox/RigCanvas/security/advisories/new) instead. Include the version, steps to reproduce and the impact you see. You'll get a reply as soon as possible.

## Supported versions
Only the latest release receives fixes. The app offers updates by itself (Settings → Updates and about).

## Scope notes
- Updates are downloaded only from this repository's GitHub Releases over HTTPS.
- `.tlcd` theme packages are zip files with a JSON layout, pictures, videos and fonts. On import, paths inside the archive are reduced to file names, so a package can't write outside the theme library; only pictures, videos and fonts are extracted, and oversized packages are refused.
- The app sends no telemetry. It goes online only for the update check and the online theme gallery (GitHub) and, when turned on, for weather (Open-Meteo, only the place name or coordinates) and the ping sensor (the host you set).

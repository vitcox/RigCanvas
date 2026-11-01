# Security policy

RigCanvas runs with administrator rights (needed for hardware sensors and the LCD driver), so security reports are taken seriously.

## Reporting a vulnerability
Please **do not open a public issue**. Use GitHub's [private vulnerability reporting](https://github.com/vitcox/RigCanvas/security/advisories/new) instead. Include the version, steps to reproduce and the impact you see. You'll get a reply as soon as possible.

## Supported versions
Only the latest release receives fixes. The app offers updates automatically (Settings → Updates).

## Scope notes
- Updates are downloaded only from this repository's GitHub Releases over HTTPS.
- `.tlcd` theme packages are zip files with a JSON layout, images and fonts. On import, paths inside the archive are reduced to file names, so a package can't write outside the theme library.

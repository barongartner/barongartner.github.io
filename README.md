# barongartner.github.io

Personal site. Live at **https://barongartner.github.io**

One self-contained `index.html`. No build step, no dependencies, no external
requests at runtime (the font stack is system, the favicon is an inline SVG data
URI). Edit the file, commit, push. GitHub Pages serves `main` from the root.

## Keeping it accurate

Each app card links to a specific release **tag**, not `/releases/latest`,
because Split and TrackForge ship their Windows and macOS builds under different
tags and `latest` would send half the visitors to the wrong download.

That means the version numbers and links here need bumping when you cut a
release. The pairs to update in `index.html`:

| App              | Card version | Links to                          |
| ---------------- | ------------ | --------------------------------- |
| Photon           | v1.2.0       | `Photon` tag `v1.2.0` (both OSes) |
| TrackForge       | v1.1.0       | tag `v1.1.0` mac, `v1.0.0` win    |
| Verbatim         | v2.2.0       | tag `v2.2.0` win                  |
| FreeFlow         | v2.0.0       | tag `v2.0.0` win                  |
| FreeVoice Studio | v1.0.0       | tag `v1.0.0` win                  |
| Split            | v1.1.2       | tag `v1.1.2` mac, `windows-v1.0.0` win |
| ReType           | v6.0.0       | tag `v6.0.0` win                  |

Windows-only apps are listed as Windows only on purpose. Verbatim shipped macOS
builds up to v1.1.0 and has been Windows only since v2.0.0, so the card does not
advertise a Mac download that no longer exists.

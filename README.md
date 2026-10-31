# barongartner.github.io

Personal site. Live at **https://barongartner.github.io**

One self-contained `index.html`. No build step, no dependencies, no external
requests at runtime (the font stack is system, the favicon is an inline SVG data
URI). Edit the file, commit, push. GitHub Pages serves `main` from the root.

## The chrome object

The iridescent form in the hero is generated per pixel in a 256x256 canvas, not
an image. Seven Wyvill soft-object kernels along an arc make a bounded field;
that field is compressed into a dome height, and the gradient of the *height*
gives surface normals which index a 256-entry iridescent strip. Fresnel shifts
the sample further along the spectrum at grazing angles, and a fixed key light
adds the specular glints.

Two things are load-bearing and easy to break:

- **Use a bounded kernel.** An inverse-square falloff spikes without limit at
  each centre, so the height field plateaus across the interior, the gradient
  goes to zero, and every one of those pixels samples the same spectrum entry.
  That renders as a flat peach mass rather than chrome.
- **Take the gradient of the height, not of the field.** The field gradient
  leaves a median surface normal of nz 0.99, meaning almost everything faces the
  viewer and the whole form is one colour.

Tuning constants sit together near the top of the script: `ISO_FRAC` sets how
much of the frame the form fills (~28%), `BUMP` how far normals swing toward
grazing, `EDGE` the width of the antialiased rim. Below about 0.05, `EDGE` tears
into stair-steps where two lobes meet.

The loop is capped at 30fps, pauses off-screen via `IntersectionObserver`, and
renders a single static frame under `prefers-reduced-motion`. One frame is also
painted synchronously at startup, because browsers pause rAF entirely in a
hidden or backgrounded document and the object would otherwise be missing.

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
| Verbatim         | v2.4.0       | tag `v2.4.0` (both OSes)          |
| FreeFlow         | v2.0.0       | tag `v2.0.0` win                  |
| FreeVoice Studio | v1.0.0       | tag `v1.0.0` win                  |
| Split            | v1.1.2       | tag `v1.1.2` mac, `windows-v1.0.0` win |
| ReType           | v6.0.0       | tag `v6.0.0` win                  |

Windows-only apps are listed as Windows only on purpose. Verbatim shipped macOS
builds up to v1.1.0, went Windows only from v2.0.0, and ships a Mac build again
from v2.4.0 (dmg and zip on the release), so its card links both.

## Iris card

`iris-card/` is the one-tap contact card for Iris, my iMessage assistant. It used to be
its own repo (barongartner/iris-card) and moved in here on Oct 31, 2026 because it did not
need to be separate. The URL did not change: https://barongartner.github.io/iris-card/

- `iris-card/index.html` shows her photo and an Add to Contacts button. Safari gets a plain
  link to the .vcf, which opens the iOS add-contact sheet. In-app browsers (Snapchat,
  Instagram) render a .vcf as raw text and block jumps to Safari, so the page detects them
  and shows the three taps instead.
- `iris-card/card/Iris.vcf` is the card itself. Iris owns the source copy at
  `C:\Atlas\Iris\Iris.vcf`; copy it here when she changes it.
- `404.html` at the root sends any dead `/iris-card/...` link (the old
  `/iris-card/Iris.vcf` was handed out before the file moved) to the card page.

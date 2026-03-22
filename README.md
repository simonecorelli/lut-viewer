# LUT Viewer

**LUT viewer by Simone Corelli, 22 Mar 2026**

A browser-based, zero-dependency 3D LUT visualiser. Load any Adobe `.CUBE` file and explore the colour transformation it encodes as an interactive 3D point cloud — with physically-correct perspective, CIE Lab visualisation, and live image preview.

→ **[Open the live app](https://simonecorelli.github.io/lut-viewer/)**

---

## What it does

A 3D LUT maps every RGB colour to a new RGB colour. This tool makes that mapping visible by placing N³ coloured spheres in a 3D cube — one for each sample point in the LUT — and showing the input cube alongside the transformed output cube. You can rotate both cubes in sync, zoom, pan, and click any sphere to read its exact coordinates.

## Features

- **Load any `.CUBE` file** — supports any LUT size (3³, 17³, 33³, 65³, …)
- **Physically-correct perspective** — geometry is calibrated for a 27″ monitor at 50 cm viewing distance; distance and cube size are specified in centimetres
- **Near-plane clipping** — spheres that would be in front of the screen (between the glass and your eye) are hidden, letting you slice into the cube
- **Three view spaces**
  - RGB — the standard colour cube
  - CIE Lab D65 — perceptually uniform; distances between spheres reflect perceived colour differences
  - CIE Lab D50 — same, adapted to the D50 white point used in print workflows
- **Four input colour spaces** — sRGB, Adobe RGB, Display P3, Rec. 2020
- **DIFF mode** — shows the absolute difference |output − input| on both the spheres and the background image
- **Background image** — load any photo; the top canvas shows the original, the bottom shows the LUT applied via trilinear interpolation
- **Click to inspect** — click any sphere to read R, G, B, Lab D65 and Lab D50 coordinates for both input and output
- **Drag to rotate**, sliders for X/Y/Z rotation, cube size (5–500 cm), distance (−400–1000 cm), and X/Y offset

## Usage

No installation needed. Open `index.html` (or `lut_viewer.html`) directly in any modern browser — Chrome, Firefox, Safari. No server required.

```
git clone https://github.com/your-username/lut-viewer.git
open lut-viewer/index.html
```

Or just use the [live version](https://your-username.github.io/lut-viewer/).

## Technical notes

- The `.CUBE` format is parsed according to the Adobe/Resolve specification: R varies fastest (innermost loop), B slowest
- Colour space conversions use the standard ICC primaries matrices; chromatic adaptation between D65 and D50 uses the Bradford method
- LUT application to images uses trilinear interpolation, the same method used by professional colour grading software
- The projection is a true pinhole model: `scale = eye_distance / point_distance`, where `eye_distance = 50 cm` and physical dimensions are computed from the assumed 27″ monitor width of 60 cm
- Everything runs client-side; no data is ever uploaded anywhere

## Context

This tool was developed as a companion to *Manuale TAV*, a technical audiovisual production manual (in Italian) covering colorimetry, image sensors, cameras, display technology, codecs, lighting, and optics.

## Licence

MIT — free to use, modify, and distribute with attribution.

---

*Built with plain HTML, CSS, and JavaScript. No frameworks, no build step, no dependencies.*

# inhandz

A hand-drawn sketch studio that turns any photo into ink, pencil, woodcut, screenprint or watercolour — entirely in the browser, in real time, with a WebGL shader. Nothing is uploaded, there is no account, and there is no watermark.

![inhandz](docs/preview.png)

## What it does

Drop an image in and it is redrawn as if by hand. Every part of the look is a live control, so you can dial in exactly the treatment you want and export it as a PNG or JPG.

### Stroke styles
Cross-hatch · Stipple · Engraving · Outline · Woodcut · Needle pen · Coloured pencil · Spray · Soft graphite

### Nibs
Round · Chisel · Marker · Dry brush · Crayon · Fineliner — each reshapes the cross-section of every stroke.

### Contour styles
Clean · Tapered · Broken · Double · Stippled · Bold marker.

### Colour
- Full source-colour modes: **Tint**, **Flat fill**, **Screenprint**, plus posterize and hue scatter
- Two-ink **duotone** blending
- 8 colour themes (Riso, Blueprint, Newsprint, Cyanotype, and more) and a 16-swatch ink palette

### Paper & finish
- 6 paper stocks (wove, fibrous, cold press, canvas, recycled, crumpled)
- Ruling: ruled, grid, dot grid, graph, isometric
- Sheet edges: torn, burnt, cut — with real irregular silhouettes
- Print finishes: letterpress emboss, misregister, photocopy degrade, speckle
- Media: **watercolour** washes with bloom, granulation and edge darkening; film grain; noise wash

### Workflow
- One-click **Looks** (10 presets) and **Surprise me**
- Split compare, hold **Space** to peek at the original, variations, undo/redo
- Batch queue — drop several images, tune once, export all
- Save / load your settings as a file
- Zoom, pan, pinch, focus mode, full keyboard shortcuts

## Running it

It is a single self-contained HTML file — no build step, no dependencies.

```bash
# just open it
open index.html
```

Or serve it locally:

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

### Deploy to GitHub Pages
Push this repository, then in **Settings → Pages** set the source to the `main` branch, root folder. The site will be served from `index.html`.

## Keyboard shortcuts

| Key | Action |
| --- | --- |
| `O` | Open image |
| `⌘/Ctrl Z` | Undo / redo (with Shift) |
| `C` | Split compare |
| `Space` | Peek at original (hold) |
| `L` | Cycle a look |
| `S` | Surprise me |
| `R` | New take |
| `V` | Variations |
| `⌘/Ctrl E` | Export |
| `0` | Fit to screen |
| `F` | Focus mode |
| `Esc` | Close / dismiss |

## How it works

The image is uploaded to a texture and a single fragment shader does everything per-pixel: a Sobel pass finds contours, a hatch/stipple/wash system builds the shading, and a chain of paper, edge and print-finish effects composites the final sheet. The preview is rendered at the on-screen resolution (times a supersampling factor) so it never resamples into a moiré. Everything runs on the GPU, which is why it stays real-time no matter how many controls are stacked.

## Tech

- Plain HTML/CSS/JS, one file
- WebGL 1 fragment shader (`OES_standard_derivatives`)
- No frameworks, no network calls

## License

MIT — see [LICENSE](LICENSE).

# Ellipses

**A seed-based generative system for concentric elliptical compositions.**

A catalogue of computational textile compositions for fashion, textile and surface design — algorithmically drawn, seed-documented, and ready for production.

---

## Overview

Ellipses is a generative design system rather than a single artwork. Each composition is built from two concentric rings — an outer ring of larger ellipses, and an inner ring of smaller ones. The two rings are offset by 45°, so their patterns interfere softly, producing a quiet, ornamental field.

The system is designed for:

- **Fashion houses** adapting concentric ornament for apparel and accessories
- **Textile studios** developing repeat patterns and yardage
- **Surface designers** working across print, wallpaper, and interior applications

Every composition can be licensed, adapted, or commissioned to a brief.

---

## Concept

An ellipse, when it is *repeated*, becomes a mandala — concentric, precise, quietly yours.

The concentric ring — rotated step by step around a shared centre — has always carried the mark of sacred geometry. From the rose windows of Gothic cathedrals to the mandalas of South Asian manuscript traditions, the repeated form is one of the oldest systems of ornamental computation we have. Ellipses translates that structure into code. Each composition begins with two ellipse counts and unfolds through rotation, layering, and glow, producing a soft, ornamental field.

The palette, the ellipse counts, and the size ratio between the two rings are all derived from a single numeric seed.

Like the other still volumes in this series (Girih, Arachne, Celestial Grove, ChaotiColor, Citrus Mosaic, Crazy Knight Curve, Crazy Knight Line, Crazy Letter, cyPollock, Digital Pollen, Draconic Fractals, Dreamscape Watercolors, Elliott Waves), **Ellipses is a static composition.** The plate, the framed plate, the surfaces, and the archive are all static frames. A mandala is something you read; its character is stillness, not motion.

---

## Features

- **Seed-based generation** — every composition is defined by a numeric seed and can be regenerated exactly
- **Deterministic output** — the same seed always produces the same composition
- **Two-tier rings** — an inner ring of 2–19 ellipses, surrounded by an outer ring of 2–29 ellipses
- **45° offset** — the outer ring is rotated by 45° relative to the inner ring, producing interference
- **Soft glow** — each ellipse carries a shadow blur that gives the composition its luminous quality
- **Twelve background palettes** — from pink and salmon, through lavender and green-yellow, to beige and cream
- **Twelve dark ink tones** — from dark red and indigo, through teal and forest green, to midnight blue and black
- **Twelve vibrant accent tones** — from yellow and magenta, through chartreuse and cyan, to turquoise and deep pink
- **Adaptive surfaces** — one seed applied across print, scarf, textile, and wall formats
- **Archive** — eight curated seeds available for immediate loading
- **Download** — export the composition as a high-resolution PNG
- **Keyboard shortcuts** — `R` for new seed, `S` to save

---

## Project Structure

```
.
├── index.html          # Main catalogue page
├── images/
│   ├── fav.svg         # Favicon
│   ├── tote.png        # Mockup: tote bag
│   ├── tee.png         # Mockup: t-shirt
│   └── cushion.png     # Mockup: cushion
└── README.md
```

---

## How It Works

### The Seed

A numeric seed (a large integer) initializes a deterministic pseudo-random generator. From this seed, the system derives:

- Background colour (from a palette of 12 light tones)
- Outer ring colour (from a palette of 12 dark tones)
- Inner ring colour (from a palette of 12 vibrant tones)
- Ellipse count for the outer ring (2–29)
- Ellipse count for the inner ring (2–19)
- Size ratio between the two rings

Because the generator is deterministic, the same seed always produces the same composition — on any device, at any time.

### The Rings

Each composition has two rings:

- **The inner ring** — drawn first, centred on the canvas, with a small ellipse width. Each successive ellipse is rotated by `π / smallCount`, evenly dividing the full circle.
- **The outer ring** — drawn second, also centred, but with a much larger ellipse width. This ring is rotated by 45° before starting, so its ellipses are offset from the inner ring's ellipses.

Where the two rings cross, their lines intersect and produce a quiet interference pattern — like the petals of a flower layered over one another.

### The Ellipses

Each ellipse is drawn as a stroked shape — width twice the height — rotated by an angle determined by its position in the ring. The stroke width scales with the ellipse size and the ring count, so denser rings have finer lines.

Every ellipse is drawn with a soft glow (`shadowBlur`) in its own colour. Because the glow extends past the stroke, the composition reads as luminous — an effect that becomes especially prominent in the outer ring.

### The Colours

Three palettes meet in every composition:

- **Background** — 12 light tones, from pink and salmon, through lavender and green-yellow, to beige and cream.
- **Outer ring** — 12 dark tones, from dark red and indigo, through teal and forest green, to midnight blue and black.
- **Inner ring** — 12 vibrant tones, from yellow and magenta, through chartreuse and cyan, to turquoise and deep pink.

The outer ring draws in dark tones (giving the composition weight), and the inner ring draws in bright tones (giving it focus). Where they meet, the palette reads as a coherent, ornamental family.

### The Surfaces

The same seed is rendered across four surface formats. These are static frames — they represent the print-ready composition.

| Surface  | Aspect | Material          |
|----------|--------|-------------------|
| Print    | 1 : 1  | Cotton rag        |
| Scarf    | 3 : 1  | Twill silk        |
| Textile  | 4 : 3  | Fabric yardage    |
| Wall     | 2 : 3  | Wallpaper         |

Each surface uses the same underlying seed and structural logic — only the repeat, orientation, and scale change.

### Stillness

Like the rest of the still volumes, Ellipses does not animate. The plate is a single frozen frame — the composition is complete the moment it is generated.

This is a deliberate design choice. A mandala is not a swarm. It is not a rotation. It is a concentric figure, drawn once and left. Its stillness is what makes it print-ready in the strictest sense: what you see is what you get.

---

## Usage

### In the browser

1. Open `index.html` in any modern browser.
2. Click **New Seed** to generate a new composition.
3. Click **Download** to save the composition as a PNG.
4. Scroll to the **Archive** section and click any plate to load it into Plate 001.

### Keyboard shortcuts

| Key | Action          |
|-----|-----------------|
| `R` | New seed        |
| `S` | Save as PNG     |

### Reproducing a composition

Each composition is identified by an 8-digit seed label displayed in the metadata panel. To reproduce a specific composition, note the seed and regenerate it programmatically:

```js
const rng = new RandomGenerator(seed);
const features = buildFeatures(rng);
renderComposition(canvas, features, rng);
```

Because the generator is deterministic, this will produce the identical composition on any device.

---

## Technical Notes

- **No build step.** The system is a single HTML file with inline CSS and JavaScript.
- **No dependencies.** All drawing is done with the native Canvas 2D API.
- **Deterministic.** The `RandomGenerator` class uses a xorshift-based PRNG seeded by an integer, so identical seeds produce identical outputs.
- **Static rendering.** Every canvas renders a single frame. There is no animation loop.
- **Feature isolation.** Cover, framed plate, surfaces, and archive thumbnails each derive their own feature set from their own local RNG, without disturbing the main plate's state.
- **Pre-computed size ratios.** The ellipse widths are computed inside `buildFeatures`, so the composition is stable across resizes — the same seed always produces the same ellipse sizes.
- **Clean shadow exit.** Every `renderComposition` call resets `shadowBlur` and `shadowColor` at the end, so the glow effect never bleeds into subsequent drawing operations.
- **Responsive.** The layout adapts from large desktop down to very small mobile devices (tested at 360px viewport width).
- **Accessible.** Supports `prefers-reduced-motion`. Pinch-zoom is enabled.

### Browser support

Tested in current versions of:

- Chrome / Edge
- Firefox
- Safari (desktop and iOS)

---

## Licensing

All Ellipses compositions are **seed-documented** and available for licensing across textile, surface, and print applications.

- **Standard licenses** cover single-product production runs.
- **Commercial use, custom editions, or exclusive rights** are available on request.

Each license is issued against a specific seed ID. Regeneration of the same seed produces the identical composition — ensuring reproducibility between artist, studio, and manufacturer.

For licensing enquiries: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Commission

Ellipses is a generative design system, not a fixed artwork. It can be adapted for specific briefs:

| Service     | Description                                                       |
|-------------|-------------------------------------------------------------------|
| Licensing   | Existing seeds from the archive, licensed for production use      |
| Commission  | New compositions designed to your palette, repeat, and product    |
| Systems     | A private generative tool built for your studio's ongoing use     |

To begin a conversation: [reyhanehdaneshdoost@gmail.com](mailto:reyhanehdaneshdoost@gmail.com)

---

## Series

Ellipses is part of a computational textile series. Each volume approaches ornament from a different structural angle:

| Volume                     | Structure                    | Motion                     |
|----------------------------|------------------------------|----------------------------|
| Girih 1                    | Islamic geometric            | Static                     |
| Arachne                    | Rotating rings               | Static                     |
| Baroque Me Baby            | Baroque frames               | Static                     |
| Bezier 1                   | Concentric curves            | Static                     |
| Bezier 2                   | Single rotating curve        | Animated (plate)           |
| Brownian Graphe            | Graph networks               | Animated + interactive     |
| Celestial Grove            | Recursive branch trees       | Static                     |
| ChaotiColor                | Cellular automata            | Static                     |
| Citrus Mosaic              | Arc-and-triangle tiles       | Static                     |
| Crazy Knight Curve         | Knight's-tour smooth path    | Static                     |
| Crazy Knight Line          | Knight's-tour gradient       | Static                     |
| Crazy Letter               | Framed wavy lines            | Static                     |
| cyPollock                  | Scattered branch field       | Static                     |
| Digital Pollen             | Noise-driven texture         | Static                     |
| Draconic Fractals          | Tiled dragon curve           | Static                     |
| Dreamscape Watercolors     | Layered watercolor blooms    | Static                     |
| Elliott Waves              | Financial chart              | Static                     |
| **Ellipses**               | **Concentric elliptical rings**| **Static**               |

The series is designed as a coherent whole — same page structure, same seed logic, same licensing and commission terms — so that each volume can be presented individually or as part of a larger body of work.

---

## Credits

- **Design & Generative System** — Reyhaneh Daneshdoost
- **Typefaces** — Cormorant Garamond · DM Mono
- **Platform** — Reyrove Studio
- **Edition** — Ellipses, Autumn 2026

### On AI tools

Where technical obstacles were encountered, AI tools were used for debugging and code optimization. Every structural, aesthetic, and conceptual decision remained the artist's own.

---

## Links

- Website — [reyrove.github.io](https://reyrove.github.io/)
- Instagram — [@rey._.rove](https://www.instagram.com/rey._.rove/)
- LinkedIn — [Reyhaneh Daneshdoost](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- X — [@reyrove](https://x.com/reyrove)

---

© Ellipses · All compositions reproducible by seed · Computational Textile Design
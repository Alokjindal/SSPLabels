# SSP Labels website: image prompts and placement guide

This guide goes with `index.html` in this folder. The page has **27 image slots**. Each one has a fixed file name. Create an image in Gemini, clean it up, name it after its slot and put it in an `images/` folder next to `index.html`. The page picks it up on the next load, with no code changes.

---

## 1. How the page loads images

For every slot, the page:

1. **Shows a placeholder straight away.** This is a soft grey SVG with the same proportions as the real image, a shimmer, the slot name and the expected file path. The SVG also stores the slot's details inside it (`<title>`, `<desc>` and a `<metadata>` JSON block with slot, file, width, height, kind, where it is used and alt text). Each `<img>` also gets `data-slot`, `data-src`, `data-kind`, `width`, `height` and `decoding="async"`.
2. **Looks for your file** in this order: `images/<slot>.webp`, then `images/<slot>.png`, then `images/<slot>.jpg`.
3. **Falls back to the image already built into `index.html`** if it doesn't find a file. If there is no built-in image either, the placeholder stays.

Your new images always win over the built-in ones. You can add them one at a time, and every slot you haven't replaced yet keeps working.

---

## 2. Where to put the files

```
ssplabels/                  <- the folder you deploy to Netlify
├── index.html
└── images/
    ├── cut_cosmetic.webp
    ├── cut_fmcg.webp
    ├── ...
    └── screen.webp
```

**Rules**

| Rule | Detail |
|---|---|
| Folder | `images/` (lower case), in the same folder as `index.html` |
| File name | Exactly the slot name from the table below, all lower case, e.g. `cut_cosmetic.webp` |
| Format | `.webp` preferred (smallest). `.png` also works and is needed for cut-outs if you can't export transparent WebP. `.jpg` is accepted for photos. |
| Size | Long side 1000–1800 px (see table). Aim for under 200 KB per file. |
| Transparency | **Cut-outs** (`cut_*`, and `tools`, `toys`, `tape`, `boxes`, `oil`, `electronics`) must have a **transparent background**. **Photos** are full rectangles. |

**Deploying on Netlify:** open the site in Netlify, go to **Deploys**, and drag the whole `ssplabels` folder (with `index.html` and `images/` inside) onto the drop area. If you deploy from GitHub, commit `images/` next to `index.html`.

**Checking a slot:** open the site, press F12, go to Console and type `SSP_IMG_SOURCE('cut_cosmetic')`. It shows `images/cut_cosmetic.webp` (your file is in use), `built-in` (the old image is in use) or `placeholder` (nothing has loaded yet).

---

## 3. Rules for every image (put this at the end of each prompt)

The site's constraints are: no brand names, no logos, no readable trademarks, and a light, calm, premium look. Gemini also adds a small sparkle watermark that you need to remove. Paste this block at the end of **every** prompt:

> **Style rules:** premium studio product photography, soft diffused daylight, gentle realistic shadows, light airy palette, high detail, sharp focus on the label, photorealistic. The printed label must look beautifully designed and high quality, but use only abstract patterns, colour blocks, icons and illegible micro-text. **No readable words, no brand names, no logos, no trademarks, no watermarks, no people, no hands.**

For **cut-outs**, add:

> Isolated object on a pure white seamless background (#FFFFFF), centred, whole object in frame with generous empty margin on all sides, soft contact shadow only, no props unless described.

**After generating (every image):**

1. **Remove the Gemini sparkle watermark.** Crop it away (it sits in a corner), or use the Canva / Photoshop healing or Magic Eraser tool.
2. **Cut-outs only:** remove the background (Canva *BG Remover*, Photoshop *Remove Background* or remove.bg) and export a **transparent PNG**, or WebP with transparency.
3. Crop to the ratio in the table. Cut-outs can be trimmed close to the object with about 4% margin.
4. Compress and convert at squoosh.app: WebP, quality 80–85, keeping transparency for cut-outs.
5. Rename to the slot name and drop it in `images/`.

---

## 4. Slot table

| # | Slot (file name) | Kind | Ratio (approx. px) | Where it appears |
|---|---|---|---|---|
| 1 | `cut_cosmetic` | cut-out | 2:3 (618×900) | Story slide 1, product card, industries, label strip |
| 2 | `cut_fmcg` | cut-out | 9:10 (744×831) | Story slide 2, product card, industries, label strip |
| 3 | `cut_cycle` | cut-out | 9:16 (367×653) | Story slide 3, product card, industries, label strip |
| 4 | `cut_holo` | cut-out | 4:3 (689×507) | Story slide 4, product card, industries, label strip |
| 5 | `cut_pharma` | cut-out | 9:10 (680×760) | Story slide 5, product card, industries, label strip |
| 6 | `cut_sleeve` | cut-out | 1:3 (320×900) | Story slide 6, product card, industries, label strip |
| 7 | `cut_tools` | cut-out | 1:1 (619×580) | Product card, industries, label strip |
| 8 | `cut_toys` | cut-out | 3:2 (689×474) | Product card, industries, label strip |
| 9 | `cut_tape` | cut-out | 5:3 (745×439) | Product card, industries, label strip |
| 10 | `cut_boxes` | cut-out | 6:5 (641×533) | Product card, industries, label strip |
| 11 | `cut_oil` | cut-out | 1:1 (560×591) | Product card, industries, label strip |
| 12 | `cut_electronics` | cut-out | 3:2 (681×468) | Product card, industries, label strip |
| 13 | `cosmetic` | photo | 4:5 (1000×1241) | Product detail view |
| 14 | `fmcg` | photo | 4:5 (1000×1241) | Product detail view |
| 15 | `cycle` | photo | 4:5 (1000×1241) | Product detail view |
| 16 | `holo` | photo | 4:5 (1000×1241) | Product detail view |
| 17 | `pharma` | photo | 4:5 (1000×1241) | Product detail view |
| 18 | `sleeve` | photo | 4:5 (1000×1241) | Product detail view |
| 19 | `tools` | cut-out | same as `cut_tools` | Product detail view |
| 20 | `toys` | cut-out | same as `cut_toys` | Product detail view |
| 21 | `tape` | cut-out | same as `cut_tape` | Product detail view |
| 22 | `boxes` | cut-out | same as `cut_boxes` | Product detail view |
| 23 | `oil` | cut-out | same as `cut_oil` | Product detail view |
| 24 | `electronics` | cut-out | same as `cut_electronics` | Product detail view |
| 25 | `offset` | photo | 16:9 (1700×949) | About section, Machines |
| 26 | `flexo` | photo | 16:9 (1700×949) | Machines |
| 27 | `screen` | photo | 16:9 (1700×949) | Machines |

**Slots 19–24 need no new prompt.** Copy the matching cut-out and rename it, e.g. `cut_tools.webp` → `tools.webp`. That is how the site works today.

Not covered here on purpose: the SSP and Shivay logos (use the official files), the opening and story videos, and client logos (only files SSP supplies with permission).

---

## 5. Prompts

Paste each prompt into Gemini, add the style rules from section 3 (plus the cut-out lines where it says *cut-out*), and set the aspect ratio shown.

### Cut-outs: the 6 story products (slots 1–6)

These are the hero images in the scroll story, so they matter most. Each one floats over a colour splash on a light page.

**1. `cut_cosmetic`** *(cut-out, 2:3)*
> A frosted blush-pink glass serum bottle with a rose-gold pump, standing on a small round white plinth. Wrapped in a luxury printed label: cream paper with rose-gold hot-foil line work, fine embossed border, soft-touch matte finish, abstract botanical motif, illegible micro-text only. Three-quarter front view, slightly low camera angle.

**2. `cut_fmcg`** *(cut-out, 1:1)*
> Two everyday grocery packs side by side: a glass spice jar with a black shaker cap and a slim drink can, both with bold, vibrant full-colour printed labels (illustrated chillies, garlic and herbs on the jar; citrus slices and leaves on the can). Rich saturated inks, crisp registration, glossy varnish. Front view, both labels fully visible, no readable words.

**3. `cut_cycle`** *(cut-out, 9:16)*
> A short section of a glossy bicycle frame tube, angled diagonally, carrying a vivid printed frame decal: cyan and magenta abstract swooshes with clean edges, hard-wearing UV-resistant gloss laminate, slight curvature showing the decal hugging the tube. Studio product shot, no full bicycle, no text.

**4. `cut_holo`** *(cut-out, 4:3)*
> A single hexagonal holographic security label, slightly tilted toward the camera, catching rainbow light: iridescent foil with fine concentric geometric guilloche patterns, a subtle embossed centre, crisp die-cut edge with a thin silver border. Macro product shot, no readable text or logo.

**5. `cut_pharma`** *(cut-out, 1:1)*
> An amber glass medicine bottle with a white child-resistant cap next to its small white folding carton. Clean pharmaceutical labels in white with green colour bands, tidy grid areas for batch and expiry details, a small Rx-style symbol and a barcode-like pattern, illegible micro-text only. Front three-quarter view, clinical but calm.

**6. `cut_sleeve`** *(cut-out, 1:3)*
> A tall, curvy PET juice bottle with a white cap, fully wrapped top to bottom in a printed shrink sleeve: lime-green to yellow gradient, citrus slices and leaf line art, glossy finish with a few condensation droplets, the sleeve following every curve of the bottle with no wrinkles. Straight front view, no text.

### Cut-outs: the 6 other product lines (slots 7–12)

**7. `cut_tools`** *(cut-out, 1:1)*
> A neat upright arrangement of construction hand tools: a claw hammer, a yellow spirit level and two screwdrivers with yellow-and-black handles. Each carries a tough printed label with abstract black-and-yellow graphics, scuff-resistant matte laminate. Front view, tools evenly spaced, no readable text.

**8. `cut_toys`** *(cut-out, 3:2)*
> A cheerful group of children's toys: a chunky red toy car and a small stack of colourful building blocks, each with bright, child-friendly printed labels featuring simple shapes, stars and dots, rounded die-cut corners, glossy finish. Front three-quarter view, no readable text, no recognisable toy brand.

**9. `cut_tape`** *(cut-out, 5:3)*
> A yellow measuring tape with its steel blade partly pulled out, the case carrying a durable printed label with abstract colour blocks and a small ruler pattern, metallic silver accents, scratch-resistant gloss. Side three-quarter view, no readable numbers or text.

**10. `cut_boxes`** *(cut-out, 6:5)*
> A tidy stack of eight small printed retail cartons in different sizes, each printed with bold geometric patterns in purple, magenta, teal, orange and yellow, crisp folded edges, satin varnish. Three-quarter view from slightly above, no readable text or logos.

**11. `cut_oil`** *(cut-out, 1:1)*
> Three clear PET edible-oil bottles of different sizes filled with golden cooking oil, each wearing a clear, appetising printed label with colourful geometric bands and a white panel, glossy and oil-resistant. Front view, bottles grouped tightly, no readable text.

**12. `cut_electronics`** *(cut-out, 3:2)*
> A white wall-mounted split air-conditioner indoor unit with a neat printed energy-rating style label on its side: a colour-coded bar scale from green to red and small warning pictograms, plus a slim silver rating plate, matte durable finish. Front three-quarter view, no readable text, no brand.

### Photos: product detail scenes (slots 13–18)

These fill the large panel when a visitor opens a product. They are full rectangles with a soft scene. **4:5 portrait.**

**13. `cosmetic`**
> The same luxury serum bottle with its rose-gold foil label on a round white plinth, in a soft pastel pink-to-lilac studio scene with a sprig of eucalyptus and dried flowers in the background, out of focus. Gentle morning light, lots of calm negative space at the top.

**14. `fmcg`**
> The vibrant spice jar and drink can on a light warm stone surface, scattered with a few whole spices and a citrus slice, peach-coloured backdrop softly blurred. Bright, fresh, appetising light, labels facing camera.

**15. `cycle`**
> Close-up of a glossy bicycle frame section with its vivid cyan-and-magenta decal, set in a soft light-blue studio with gentle reflections on the paint and a blurred hint of a wheel spoke in the background. Calm and clean.

**16. `holo`**
> A few hexagonal and round holographic labels laid on a pale lavender surface, catching rainbow light at different angles, one in sharp focus, the others softly blurred, gentle prism light streaks.

**17. `pharma`**
> The amber medicine bottle and its green-banded white carton on a clean white counter in a bright, minimal, softly blurred pharmacy-style background. Clinical, trustworthy, calm.

**18. `sleeve`**
> Two or three shrink-sleeved juice bottles in different colourways (lime, orange, berry) on a light pale-yellow surface, a few condensation droplets, soft daylight, blurred fresh backdrop.

### Photos: machines (slots 25–27)

**16:9 landscape.** These represent the three press types. They show generic machines, not a specific brand.

**25. `offset`**
> Wide shot of a modern four-colour sheet-fed offset printing press in a bright, spotless, daylight-filled print shop, a neat stack of freshly printed colourful label sheets at the delivery end. Light grey epoxy floor, large windows, calm and orderly, no people, no brand name on the machine.

**26. `flexo`**
> A modern narrow-web flexographic label press running a roll of colourful printed labels through its print stations and UV dryers, the web of labels clearly visible, bright clean industrial interior, soft daylight. No people, no brand name.

**27. `screen`**
> A semi-automatic flatbed screen printing machine with its screen frame lifted, a squeegee resting on the frame, sheets of brightly printed labels stacked beside it, bright clean workshop, soft daylight. No people, no brand name.

---

## 6. Quick checklist before you deploy

- [ ] Gemini sparkle watermark removed from every file
- [ ] No readable words, brand names or logos anywhere in the images
- [ ] Cut-outs have transparent backgrounds; photos are full rectangles
- [ ] File names match the slot names exactly (lower case)
- [ ] `tools`, `toys`, `tape`, `boxes`, `oil` and `electronics` are copies of their `cut_` files
- [ ] Files are in `images/`, next to `index.html`
- [ ] Each file is under about 200 KB
- [ ] Spot-check with `SSP_IMG_SOURCE('<slot>')` in the browser console

Once all 27 files are in place, the built-in copies inside `index.html` are no longer needed. They can be stripped out, which takes the page from about 5.7 MB to under 3 MB.

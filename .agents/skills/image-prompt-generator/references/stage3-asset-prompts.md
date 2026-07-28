# Stage 3 Asset Prompts

Use this file for Stage 3 only. Generate one already-stitched multi-view asset image from the approved Stage 2 image. Run one Image Workbench Nano Banana Pro generation per asset sheet. Do not create separate views or assemble them outside the generated image.

Use the approved Stage 2 image as the first reference. When an approved face reference is supplied for a character, attach it as the second reference.

In every final prompt, refer to an input only as `the reference image`, `the first reference`, or `the second reference`. Do not write approval status, workflow stages, concept terminology, or model names.

## Measurement Resolution

Every single-character sheet must include a height caption. Every prop sheet must include a real-world size caption. Environment sheets carry no measurement caption. Use an explicit measurement from the user or story reference when available. Otherwise infer one specific, plausible metric measurement from the approved design and story context.

For characters, infer height from stated age, build, role, relative stature, and intended physical read. For prop assets, state the production-useful dimension: length for long objects and vessels, height for upright objects, diameter for circular devices, or width and height for flat objects. Infer the measurement from human use, carrying capacity, internal space, mechanical function, and the approved design's scale.

Crowds have no Stage 3 sheet and therefore no height caption.

## Asset-Sheet Routing

Classify each non-character asset by physical scale and spatial role before selecting a template. Use `Human-Scale Props` for discrete objects at or below human scale. Use `Large Props` for any discrete asset larger than a person or requiring boarding, access, cargo capacity, or large-scale structural support. Use `Environments` for a navigable space, fixed architecture, or an asset whose identity depends on its surroundings. This routing is based on scale and spatial role, not object type.

## Characters

Create three panels stitched left to right. Keep the same person, face, hair, outfit, colors, proportions, and photographic style as the approved Stage 2 image.

Use this prompt, replacing `<HEIGHT>` with an explicit measurement from the brief or story reference, or with a plausible metric height inferred from the approved design and story context.

```text
Using the same person in the first reference image, generate one photorealistic live-action cinematic image composed of three panels stitched side by side, left to right, in a simple dark interior space with a black wall and black floor. Keep the same face, hair, outfit, colors, proportions, skin texture, fabric texture, material response, and photographic style.

Use consistent cinematic available-light photography across all panels: even soft interior illumination, soft frontal ambient key, gentle overhead room fill, balanced exposure, open readable shadows, and grounded contact shadows. Use subtle fine cinematic film grain. Keep the result sharp, clean, richly colored, and professionally photographed. Use no rim light, backlight, edge light, spotlight, flood fill, harsh beauty key, white bounce, halo separation, scratches, dust, stains, faded vintage damage, film burn, border artifacts, sepia tint, washed-out contrast, or aged-photo deterioration.

Left panel: front-facing head-and-shoulders portrait with facial features clearly visible.
Middle panel: front-facing full-body view, head removed above the neck, showing the body from the neck down.
Right panel: back-facing full-body view, entire body visible.

Use even spacing and consistent scale across all panels. In the bottom-right corner, render a small clearly legible caption on a subtle semi-transparent dark label reading exactly: "Height: <HEIGHT>". Include no other text. Maintain exact continuity with the first reference image.
```

### Face-Locked Character Variant

Use this branch only when an approved face reference is supplied. Attach the approved Stage 2 character image first and the face reference second.

```text
You are given two reference images. The first reference defines the body, build, outfit, garment colors, hairstyle, pose, and current facial condition. The second reference defines the facial identity.

Create the same three-panel photorealistic live-action character image described in the Characters section. The face in the left panel must match the second reference exactly in bone structure, eye shape, nose, mouth, jawline, and proportions, while retaining any current facial condition shown in the first reference. Maintain exact continuity with both references.
```

## Prop Sheets

Use the approved Stage 2 image as the sole reference. Select replacements by scale:

- **Human-Scale Props:** replace `<ITEM>` with `item`, `<VIEWS>` with `front, side, and top views`, and `<STAGE>` with `a simple dark studio with a black wall and black floor`.
- **Large Props:** replace `<ITEM>` with `large asset`, `<VIEWS>` with `front three-quarter, side-profile, and rear three-quarter views`, and `<STAGE>` with `a large-scale black seamless stage with a black backdrop and black floor plane`. Do not use top-down or underside views.

Replace every placeholder before returning the final prompt.

```text
Based on this reference image, generate one 16:9 landscape multi-view sheet of the same <ITEM>, preserving identical silhouette, structural form, materials, colors, finish, wear, and proportions. Show <VIEWS> combined into one single image.

Render every view as a photorealistic live-action cinematic reference still of the same real three-dimensional asset, with the same material response, surface finish, reflections, perspective, depth, and shading character as the reference. Place all three views in <STAGE>. Use consistent cinematic available-light photography across the sheet: even soft illumination, soft frontal ambient key, gentle overhead fill, balanced exposure, open readable shadows, and grounded contact shadows. Use no rim light, backlight, edge light, spotlight, flood fill, harsh beauty key, white bounce, or halo separation. Use subtle fine cinematic film grain. Keep the result sharp, clean, richly colored, and professionally photographed, with consistent scale and exact photographic continuity with the reference.

In the bottom-right corner, render a small clearly legible caption on a subtle light label reading exactly: "Size: <MEASUREMENT>". Include no other text.
```

Use an explicit measurement from the brief or story reference when available. Otherwise infer `<MEASUREMENT>` from the approved design and story context; do not omit the `Size` line.

## Special Elements

Special elements are effects rather than solid objects. Create a multi-angle sheet only when the user explicitly requests it and multiple views are useful. Use a plain dark, composite-ready background and lock the approved reference colors exactly.

### Body-Anchored Effect

```text
Based on this reference image, generate a turnaround sheet of the same special effect on the same caster figure in the same motivating pose. Preserve identical effect form, particle layers, color, and intensity. Create three panels stitched side by side on a plain dark composite-ready background: front, side profile, and back. Keep the effect semi-transparent and luminous where it emits, with consistent particle detail across all panels. Include no text. Maintain exact continuity with the reference.
```

### World-Space Effect

```text
Based on this reference image, generate a multi-angle sheet of the same special effect on a plain dark composite-ready background. Preserve identical form, particle layers, color, and intensity. Create three panels stitched side by side: front-on, three-quarter oblique, and overhead views. Keep the effect semi-transparent and luminous where it emits, with consistent particle detail across all panels. Include no text. Maintain exact continuity with the reference.
```

## Environments

Create one 16:9 landscape image laid out as an even 2x2 grid of the same location from four camera positions. Use the approved Stage 2 environment image as the sole reference. This is a location turnaround, not a body or object sheet.

```text
Based on this reference image, generate one 16:9 landscape image laid out as an even 2x2 grid of four panels, two on top and two on the bottom, not a single horizontal strip. Each panel shows the same location from a different camera angle, with identical architecture, materials, dressing, palette, period, ornament, scale, and lighting mood.

Top-left panel: front view of the location.
Top-right panel: camera turned 90 degrees left from the front-view position, facing the left side of the space.
Bottom-left panel: camera turned 90 degrees right from the front-view position, facing the right side of the space.
Bottom-right panel: 180-degree reverse view from the front-view position, facing the opposite direction and showing the unseen back of the space. Invent the unseen half freely while keeping it fully consistent with the established location.

Render every panel as a photorealistic live-action film still in exactly the same photographic style, materials, and lighting as the reference image. Keep all four panels unmistakably the same place seen from four positions. The front panel preserves exact continuity with the reference. The left, right, and reverse panels reveal off-frame space while remaining fully consistent with the established location. Include no characters and no text.
```

### Environment Variant Grid

Use this branch for a time, condition, or dressing variant of an existing approved four-panel environment sheet. Use the approved base grid as the sole reference.

```text
Based on this 2x2 grid of the same location, keep all four camera angles, framing, grid layout, architecture, furniture, materials, and composition exactly the same. Change only the time, lighting, condition, and dressing to: <VARIANT_APPEARANCE>. Apply that state consistently across all four panels. Include no characters and no text.
```

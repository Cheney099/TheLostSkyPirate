# Stage 3 Asset Prompts

Use this file for Stage 3 only. For characters, props, and special elements, generate one already-stitched multi-view asset image and create one Nano Banana Pro node per sheet. For environments, generate three standalone images from three prompts and create one node per prompt. Do not assemble environment views into a grid or sheet.

Use the approved Stage 2 image as the first reference. When an approved face reference is supplied for a character, attach it as the second reference.

In every final prompt, refer to an input only as `the reference image`, `the first reference`, or `the second reference`. Do not write approval status, workflow stages, concept terminology, or model names.

## Measurement Resolution

Every single-character sheet must include a height caption. Every prop sheet must include a real-world size caption. Environment images carry no measurement caption. Use an explicit measurement from the user or story reference when available. Otherwise infer one specific, plausible metric measurement from the approved design and story context.

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

Use the approved Stage 2 environment image as the sole reference. Return three complete prompts, each creating one standalone 16:9 landscape, 4K image of the same location from a different camera position. Create and run three separate Nano Banana Pro nodes, attaching the same reference image to each node. Do not create a grid, split screen, collage, contact sheet, or multi-panel image.

Keep the location's architecture, layout, scale, materials, dressing, palette, period, ornament, condition, and lighting continuity identical across all three views. Preserve all identity-defining landmarks and established spatial relationships. Reveal only plausible off-frame portions of the same location; do not add, remove, replace, or relocate major structures or defining elements. Adapt camera height and distance to the location and story evidence rather than forcing a ground-level view when an elevated, aerial, or distant view is required.

Write each prompt by replacing `<VIEW_INSTRUCTION>` below with the matching view instruction. Return the three completed prompts in the listed order, without placeholder text.

```text
Based on this reference image, generate one standalone photorealistic live-action cinematic environment still of the same location. Preserve identical architecture, layout, scale, materials, dressing, palette, period, ornament, condition, and lighting continuity. <VIEW_INSTRUCTION> Keep the primary landmark recognizable and preserve the established relationship between all visible structures. Reveal only spatially plausible portions of the same location without introducing, removing, replacing, or relocating identity-defining elements. Match the reference's photographic treatment, material response, atmospheric depth, and lighting mood. 16:9 landscape, 4K. Include no characters, text, labels, borders, panels, or grid.
```

Use these view instructions:

1. **Establishing oblique view:** `Move to a new camera position and show a wide three-quarter establishing view that clearly presents the primary landmark, the main usable space, and their depth relationship; do not duplicate the reference composition.`
2. **Cross-axis view:** `Move laterally to the opposite side of the main viewing axis and look diagonally across the location, keeping the primary landmark visible while revealing the side-to-side arrangement, access, and circulation.`
3. **Reverse spatial view:** `Relocate beyond or beside the primary focal area and look back through the location from the opposing direction, preserving the primary landmark and established structures while revealing their reverse spatial relationship.`

### Environment View Variants

Use this branch for a time, condition, or dressing variant of an approved three-view environment set. Process each approved view separately. Attach one base view to each node and return three prompts and three standalone images in the same view order.

```text
Based on this reference image, generate one standalone photorealistic live-action cinematic environment still. Keep its camera position, framing, architecture, layout, furniture, materials, and composition unchanged. Change only the time, lighting, condition, and dressing to: <VARIANT_APPEARANCE>. Apply the specified state consistently throughout the image. 16:9 landscape, 4K. Include no characters, text, labels, borders, panels, or grid.
```

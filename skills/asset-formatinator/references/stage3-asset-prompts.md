# Stage 3 Asset Prompts

Use this file for Stage 3 only. For characters, props, and special elements, return one prompt for an already-stitched multi-view asset image. For environments, return three prompts for three standalone images. Do not run the prompts or assemble environment views into a grid or sheet.

Require a non-null `stage1_prompt` in the matching registry variant. Read it directly and extract the stable visible design decisions appropriate to the asset type. Discard its model syntax, rendering method, background, camera, framing, aspect ratio, and other source-presentation instructions. Every normal Stage 3 final prompt tells the image model to use the attached approved cinematic image as its visual reference. For a Combined environment this is the direct MidJourney image; otherwise it is the Stage 2 image. The user supplies that image externally; the skill never inspects, verifies, requests, or internally requires it and must not block prompt writing when it is unavailable to the local agent.

Write the extracted design facts directly into every final prompt and refer to the external visual source only as `the attached image` or `the reference image`. Do not mention approval status, workflow stages, prior prompts, source documents, concept terminology, model names, or whether the local agent can access the image.

Replace every angle-bracket placeholder with concise concrete wording before returning a final prompt.

## Measurement Resolution

Every single-character sheet must include a height caption. Every prop sheet must include a real-world size caption. Environment images carry no measurement caption. Use an explicit measurement from the user or story reference when available. Otherwise infer one specific, plausible metric measurement from the logged design and story context.

For characters, infer height from stated age, build, role, relative stature, and intended physical read. For prop assets, state the production-useful dimension: length for long objects and vessels, height for upright objects, diameter for circular devices, or width and height for flat objects. Infer the measurement from human use, carrying capacity, internal space, mechanical function, and the logged design's scale.

Crowds have no Stage 3 sheet and therefore no height caption.

## Asset-Sheet Routing

Classify each non-character asset by physical scale and spatial role before selecting a template. Use `Human-Scale Props` for discrete objects at or below human scale. Use `Large Props` for any discrete asset larger than a person or requiring boarding, access, cargo capacity, or large-scale structural support. Use `Environments` for a navigable space, fixed architecture, or an asset whose identity depends on its surroundings. This routing is based on scale and spatial role, not object type.

## Characters

Extract the character's body design, apparent age, face, hair, outfit, colors, proportions, permanent accessories, and prosthetics from `stage1_prompt`. Apply the photographic material, lighting, and finish rules from `character-generator.md` directly to that design. The externally attached Stage 2 image supplies visual continuity. Create three panels stitched left to right and preserve both the stated design and attached appearance exactly across them.

Use this prompt, replacing `<CHARACTER_DESIGN>` with the concise concrete extracted design and `<HEIGHT>` with an explicit measurement from the brief or story reference, or with a plausible metric height inferred from the logged design and story context.

```text
Using the person in the attached image as the visual reference, generate one photorealistic live-action cinematic image composed of three panels stitched side by side, left to right, in a simple dark interior space with a black wall and black floor. The fixed character design is: <CHARACTER_DESIGN>. Keep the same person, face, hair, outfit, colors, proportions, skin texture, fabric texture, and material response as the attached image across all panels.

Use consistent cinematic available-light photography across all panels: even soft interior illumination, soft frontal ambient key, gentle overhead room fill, balanced exposure, open readable shadows, and grounded contact shadows. Use subtle fine cinematic film grain. Keep the result sharp, clean, richly colored, and professionally photographed. Use no rim light, backlight, edge light, spotlight, flood fill, harsh beauty key, white bounce, halo separation, scratches, dust, stains, faded vintage damage, film burn, border artifacts, sepia tint, washed-out contrast, or aged-photo deterioration.

Left panel: front-facing head-and-shoulders portrait with facial features clearly visible.
Middle panel: front-facing full-body view, head removed above the neck, showing the body from the neck down.
Right panel: back-facing full-body view, entire body visible.

Use even spacing and consistent scale across all panels. In the bottom-right corner, render a small clearly legible caption on a subtle semi-transparent dark label reading exactly: "Height: <HEIGHT>". Include no other text. Maintain exact continuity with the attached image and stated character design.
```

### Face-Locked Character Variant

Use this optional branch only when the user explicitly supplies a separate face reference. The externally attached Stage 2 character image is the first reference and the face image is the second reference. Continue to derive the written body, build, outfit, garment colors, hairstyle, proportions, and current condition from `stage1_prompt`; the second reference controls facial identity only. Do not inspect or verify either image.

Use the complete Characters prompt template above, changing `the attached image` to `the first reference image`. After its fixed character design sentence, add: `Use the second reference image only for facial bone structure, eye shape, nose, mouth, jawline, and facial proportions; the first reference image and stated design control the body, build, outfit, garment colors, hairstyle, proportions, and current condition.` Keep every panel, lighting, finish, measurement, and exclusion instruction from the base template so the returned prompt remains standalone.

## Prop Sheets

Extract the asset's identity, silhouette, structural form, proportions, construction, operating parts, moving parts, and functional logic from `stage1_prompt`. Use the externally attached Stage 2 image for visual continuity. Resolve any written material, color, finish, wear, and craftsmanship instructions using `prop-generator.md`, then state those concrete decisions in the final prompt. Select replacements by scale:

- **Human-Scale Props:** replace `<ITEM>` with `item`, `<VIEWS>` with `front, side, and top views`, and `<STAGE>` with `a simple dark studio with a black wall and black floor`.
- **Large Props:** replace `<ITEM>` with `large asset`, `<VIEWS>` with `front three-quarter, side-profile, and rear three-quarter views`, and `<STAGE>` with `a large-scale black seamless stage with a black backdrop and black floor plane`. Do not use top-down or underside views.

Replace `<ASSET_DESIGN>` and every routing placeholder before returning the final prompt.

```text
Using the attached image as the visual reference, generate one 16:9 landscape multi-view sheet of this <ITEM>: <ASSET_DESIGN>. Preserve the attached asset's silhouette, structural form, materials, colors, finish, wear, proportions, operating parts, and functional logic across all views. Show <VIEWS> combined into one single image.

Render every view as a photorealistic live-action cinematic reference still of the same real three-dimensional asset, with the attached image's material response, surface finish, reflections, perspective, depth, and shading character. Place all three views in <STAGE>. Use consistent cinematic available-light photography across the sheet: even soft illumination, soft frontal ambient key, gentle overhead fill, balanced exposure, open readable shadows, and grounded contact shadows. Use no rim light, backlight, edge light, spotlight, flood fill, harsh beauty key, white bounce, or halo separation. Use subtle fine cinematic film grain. Keep the result sharp, clean, richly colored, and professionally photographed, with consistent scale and exact visual continuity with the attached image across every view.

In the bottom-right corner, render a small clearly legible caption on a subtle light label reading exactly: "Size: <MEASUREMENT>". Include no other text.
```

Use an explicit measurement from the brief or story reference when available. Otherwise infer `<MEASUREMENT>` from the logged design and story context; do not omit the `Size` line.

## Special Elements

Special elements are effects rather than solid objects. Create a multi-angle sheet only when the user explicitly requests it and multiple views are useful. Extract the effect's form, particle layers, colors, intensity, attachment, and motivating pose from `stage1_prompt`; use the externally attached Stage 2 image for visual continuity. Use a plain dark, composite-ready background and preserve both sources within their assigned roles.

### Body-Anchored Effect

```text
Using the attached image as the visual reference, generate a turnaround sheet of this body-anchored special effect: <EFFECT_DESIGN>. Preserve the attached caster design, motivating pose, effect form, particle layers, color, and intensity. Create three panels stitched side by side on a plain dark composite-ready background: front, side profile, and back. Keep the effect semi-transparent and luminous where it emits, with consistent particle detail across all panels. Include no text.
```

### World-Space Effect

```text
Using the attached image as the visual reference, generate a multi-angle sheet of this world-space special effect: <EFFECT_DESIGN>. Preserve the attached effect's form, particle layers, color, and intensity. Create three panels stitched side by side on a plain dark composite-ready background: front-on, three-quarter oblique, and overhead views. Keep the effect semi-transparent and luminous where it emits, with consistent particle detail across all panels. Include no text.
```

## Environments

Use the matching scene variant's `stage1_prompt` as the textual architectural and spatial anchor. Every final prompt tells the image model to use the externally attached approved cinematic environment image as its visual reference, but the skill does not inspect or verify it. Return three complete standalone prompts, each creating one 16:9 landscape, 4K image of that location from a different camera position. Do not create a grid, split screen, collage, contact sheet, or multi-panel image.

Read `stage1_prompt` before writing any view. Extract only explicitly established architecture, layout, circulation, scale, fixed mechanisms, landmarks, usable spaces, spatial relationships, materials, colors, time, weather, lighting, and atmosphere. Do not infer additional structures, visual treatment, or off-frame features from it.

Keep the architecture and spatial relationships identical across all three views. Reveal an off-frame area only when its existence and relationship are explicit in `stage1_prompt`. Do not add, remove, replace, or relocate fixed structures or defining elements. Adapt camera height and distance to the established location rather than forcing a ground-level view.

Repeat location-specific materials, colors, time, weather, lighting, or atmosphere only when they are explicitly stated in `stage1_prompt` or requested by the user. Otherwise apply the same generic treatment in all three prompts: neutral cinematic available-light photography, balanced exposure, open readable shadows, physically plausible material response, atmospheric depth, and subtle fine film grain. Do not infer unrecorded visual treatment from the inaccessible attached image.

Before returning the prompts, replace every placeholder with concise concrete wording from `stage1_prompt`. Generic labels such as `primary landmark`, `key feature`, `main usable space`, and `identity-defining elements` are planning terms only and must not appear in a completed prompt. If the stored prompt does not establish a required relationship, choose a different camera instruction supported by the available information instead of inventing one.

Write each prompt by replacing `<CONCRETE_ARCHITECTURE_AND_RELATIONSHIPS>` and `<VIEW_INSTRUCTION>` below. Return the three completed prompts in the listed order, without placeholder text.

```text
Using the attached image as the visual reference, generate one standalone photorealistic live-action cinematic environment still of the same location. The fixed location design is: <CONCRETE_ARCHITECTURE_AND_RELATIONSHIPS>. <VIEW_INSTRUCTION> Preserve the attached location's architecture, layout, scale, construction, dressing, condition, and stated spatial relationships; do not introduce, remove, replace, or relocate any established structure or fixed feature. Use neutral cinematic available-light photography, balanced exposure, open readable shadows, physically plausible material response, atmospheric depth, and subtle fine film grain. 16:9 landscape, 4K. Include no characters, text, labels, borders, panels, or grid.
```

Use these view instructions:

1. **Establishing oblique view:** Resolve a wide three-quarter view around a named fixed structure and a named usable or circulation space explicitly established by `stage1_prompt`; state their concrete foreground, middle-ground, or background relationship and choose a materially different framing from the one recorded in `stage1_prompt`.
2. **Cross-axis view:** Move laterally across an explicit viewing or circulation axis and look diagonally across the location; name the fixed structures and access route whose side-to-side arrangement becomes visible.
3. **Reverse spatial view:** Relocate beyond or beside an explicitly established focal structure or usable area and look back from the opposing direction; name the fixed structures whose reverse relationship becomes visible.

### Environment View Variants

Use this branch for a time, condition, or dressing variant of a three-view environment set. Derive the same written fixed design from `stage1_prompt` and use the externally attached approved cinematic environment image as the visual reference. Preserve the three resolved camera instructions from the original Stage 3 prompts when available; otherwise resolve them again using the three standard view instructions above. Return three standalone prompts in the same view order without asking the local agent to inspect or verify an image.

```text
Using the attached image as the visual reference, generate one standalone photorealistic live-action cinematic environment still of the same location. The fixed location design is: <CONCRETE_ARCHITECTURE_AND_RELATIONSHIPS>. Use this camera plan: <VIEW_INSTRUCTION>. Preserve the attached location's architecture, layout, scale, construction, and stated spatial relationships. Change only the time, lighting, condition, and dressing to: <VARIANT_APPEARANCE>. Apply the specified state consistently throughout the image. 16:9 landscape, 4K. Include no characters, text, labels, borders, panels, or grid.
```

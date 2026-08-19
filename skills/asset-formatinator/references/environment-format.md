# Environment Format

## Stage Routing

- **Stage 1: MidJourney Concept:** Create a complete monochrome line-art environment sketch using `environment-style-guide.md`.
- **Stage 2: Nano Banana Pro Film Still:** Read the matching scene variant's `stage1_prompt` as the textual architectural and spatial source, read `environment-style-guide.md` internally to resolve visible color and material treatment, and create a live-action cinematic still using this format. The final prompt tells the image model to use the attached Stage 1 environment image, which the user supplies externally. Do not inspect, verify, or request that image.

## Shared Prompt Rules

Resolve the brief in this order: intended location, function, story state, and approved continuity; project-appropriate equivalents for conflicting literal terms; ownership, scale, activity, time, weather, and condition; circulation, work areas, access routes, fixed structures, and a focal point; then clear near, middle, and far spatial relationships. Do not normalize a brief when the user explicitly requests strict literal use.

Write a coherent visible description, not disconnected keywords. Apply the universal final-prompt rules in `SKILL.md`. Translate internal location, ownership, and story facts into visible architecture, materials, equipment, activity, and atmosphere. Do not put instructions such as "derive" or "apply the style guidance" in the final prompt.

## Stage 1: MidJourney Concept Guidance

The final MidJourney prompt must be strictly under 150 words. Count all descriptive text and parameters; the maximum is 149 words.

Describe location identity and function; one dominant architectural, terrain, or vessel silhouette; clustered secondary masses; selective tertiary detail; spatial layout and circulation; materials, construction, and equipment; project motifs and ownership cues; camera position, framing, and focal point; time, weather, atmosphere, and requested activity; then output and continuity requirements. Include specific near, middle, and far relationships, mechanism and load logic, large negative spaces, scale comparisons, and a deliberate frame boundary. Expand thin briefs with physical evidence, not generic adjectives.

The completed Stage 1 prompt becomes the environment's architectural and spatial anchor. Explicitly name the fixed structures, usable or circulation spaces, and relationships that later camera views must preserve. Do not substitute labels such as `primary landmark`, `key feature`, `main usable space`, or `identity-defining elements` for the actual visible design.

Render monochrome linework with a white paper or neutral light ground, clear line hierarchy, crisp varied-width ink lines, clear graphic shape design, minimal texture, and a clean presentation. Use line weight, contour density, overlap, and open space to separate dominant, secondary, and tertiary forms. Use no color, lighting, shading, gradients, or painterly rendering. Use one prominent pattern or repetition system and, when useful, one quieter supporting system; vary repeated elements by function, construction, perspective, and use.

Choose a motivated camera position with readable depth, a scene-appropriate focal point, and deliberate framing. Honor a camera height or viewpoint that the user brief, story continuity, or required scene function explicitly states or clearly implies. Use elevated, overhead, or aerial framing when the scene is an overall city, island, fleet, skyline, or spatial-layout reveal; do not replace that implied overview with a street-level view. For monumental locations, allow a wide establishing view, centered ceremonial axis, or close foreground mass partially occluding the frame when it strengthens scale. Use receding structures, routes, terrain, ship elements, cloud layers, minor vessels, or repeated architectural units to establish depth and size. Keep people, animals, text, signage, props, and plot events out unless the brief or continuity requires them.

For an established location design, preserve its architecture, layout, object count, scale, and spatial relationships unless the request changes them. For a variant, state what remains unchanged and describe only the visible delta.

## Stage 2: Nano Banana Pro Film Still Format

### Transformation and Recomposition

Require a non-null `stage1_prompt` in the matching scene variant. Extract its concrete location identity, architecture, scale, layout, mechanisms, landmarks, circulation, usable spaces, and spatial relationships. Keep those facts unchanged while translating the logged line-art design into real construction edges, joints, seams, materials, and volumetric space. Discard the Stage 1 rendering method, line-art treatment, background, camera, framing, aspect ratio, and other concept-presentation instructions. Tell the image model to use the attached image as the visual source for that same design without claiming to have inspected it.

Open every final prompt with: `Using the attached image as the visual reference, create a fully photorealistic live-action cinematic environment of the same location.` Follow it with a concise concrete description of the extracted fixed design. Select a camera plan materially different from the framing recorded in `stage1_prompt`; state the resulting camera position directly without mentioning comparison, prior imagery, or workflow. Do not write stage labels, approval status, concept terminology, production-design terminology, or internal source-handling instructions into the final prompt.

Select a shot purpose, such as arrival, scale, an existing circulation route, an operational area, or observed activity. Use an on-location standing-height camera only when the brief, story continuity, logged design, and scene function do not explicitly state or clearly imply an elevated, overhead, distant, or aerial view. For a city, island, fleet, skyline, or spatial-layout reveal, retain an appropriately elevated viewpoint while selecting a genuinely new angle. Change at least three of distance, angle, focal length, foreground relationship, depth order, and focal point from the Stage 1 framing.

Preserve the set itself: do not add, remove, replace, or relocate structures, vehicles, mechanisms, routes, or props established in `stage1_prompt`. Name the actual landmark and fixed spatial anchors in the final prompt rather than using generic labels. Allow only the cropping and occlusion that naturally result from the selected camera position; do not choose an angle that hides the defining landmark or changes the location's identity.

Render a fully photographed environment with physical material texture, construction depth, natural light behavior, reflections, contact shadows, and atmospheric perspective. Do not retain line art, drawn outlines, sketch marks, hatching, paper texture, cel contouring, flat graphic fills, simplified illustrated perspective, comic treatment, painted concept-art marks, or any hand-drawn appearance.

### Stage 2 Prompt Emphasis and Compression

Treat `stage1_prompt` and the externally attached image as the detailed continuity sources. Do not rewrite the complete Stage 1 inventory. Compress physical continuity into one opening paragraph of no more than two sentences; the required opening sentence counts toward this limit. State only the dominant silhouette, essential spatial arrangement, focal structure, defining condition, and continuity-critical mechanisms or features. Do not enumerate tertiary architecture, individual fittings, repeated equipment, every vessel or building component, comprehensive material variants, or decorative inventories already established by the source design.

Follow the continuity paragraph with one concise sentence specifying camera position, viewing direction, lens feel, framing, focal point, and depth order. Do not repeat physical details from the continuity paragraph unless their placement is necessary to define the shot.

Make the lighting, color behavior, atmosphere, and cinematic depth paragraph the largest part of the prompt. State the motivating source and direction; foreground, middle-distance, and distant exposure and contrast; depth-dependent saturation and color temperature; the density and distribution of cloud, mist, condensed steam, and suspended water vapor; volumetric scattering, rays, and veiling glare; and the placement and strength of halation and bloom. Describe how light organizes the established materials rather than repeating a list of material colors.

Close with one compact sentence containing photographic finish, aspect ratio, resolution, and only exclusions that prevent a demonstrated or continuity-critical failure. Combine related exclusions instead of writing a long negative inventory. Do not repeat the same requirement across sections.

### Presentation, Camera, and Activity

Produce one photorealistic live-action cinematic environment still, 16:9 landscape, 4K, with plausible perspective, scale, construction, material response, reflections, contact shadows, and lighting appropriate to the requested time, weather, and location.

Place the camera within an unfolding scene rather than treating the location as a neutral record. Favor an oblique or three-quarter view when useful, but use a centered axial composition for ceremonial gateways, civic monuments, or symmetrical engineered spaces. Use a wide 24-40mm full-frame lens feel for monumental architecture, fleets, floating structures, and large spatial reveals; use a natural 35-55mm feel for human-scale locations. Allow a close dark foreground structure, vessel edge, bridge, or architectural mass to partially occlude the frame when it strengthens depth and scale. Stage a readable middle-distance focal area and receding structures, routes, vessels, or landmarks. Include observable use, activity, or recent evidence of activity when appropriate.

Use one coherent lighting situation. State its source, direction, color temperature, shadow and reflection behavior, practical sources, and distance falloff. Let daylight, moonlight, and practical illumination enter through plausible openings or fixtures; derive mist, condensed steam, cloud, ambient fill, reflections, and visibility from that same condition. In aerial, maritime, elevated, cloudbound, or steam-powered environments, make dense suspended water vapor a primary depth medium: banks of luminous moisture occupy the gaps between structures, curl around hulls and platforms, soften cloud boundaries, and progressively veil distant forms. Build layered volumetric separation through strong foreground silhouettes, readable middle-distance architecture, and distant forms partially absorbed into water-laden atmosphere.

When a bright source enters or sits behind the composition, push optical diffusion strongly: extreme localized halation, heavy broad bloom, luminous veiling glare, and visible volumetric scattering through suspended water droplets. Allow the brightest sky openings, engine emissions, reflections, and practical sources to clip and bleed deeply into adjacent vapor. Keep this diffusion source-driven rather than uniformly fogging the image; preserve dark foreground silhouettes, readable middle-distance edges, and material detail outside the bloom field.

Use moderate depth of field, localized sharpness, subtle lens softness, fine irregular film grain, and a photochemical motion-picture response with smooth exposure transitions. Keep water vapor clean, luminous, and moisture-heavy rather than dusty, sooty, dirty, or distressed.

### Color and Physical Scene Logic

Read `environment-style-guide.md` and the brief internally to resolve palette, material color, lighting, and atmospheric color. In the final prompt, state the resulting visible materials, surface colors, lighting source, direction, and atmospheric conditions directly without naming their story or style-guide source. Carry color through physical surfaces such as paint, brick, sailcloth, glass, metal, timber, textiles, enamel, and planted elements. Use a dominant material-color family, a supporting family, and a restrained contrast or metallic system.

Preserve rich, theatrical material color and clean luminous pale surfaces in the near and middle distance. Allow atmospheric distance, cloud, sky, and backlit haze to compress toward cool silver, blue-gray, or teal when compatible with the location and lighting, while retaining selective warm metal, enamel, sailcloth, or practical-light accents. In low light, preserve the strongest color on directly lit, reflective, or nearby surfaces while distant forms and deep shadow become restrained. Build darkness through natural low light, value contrast, reflection, surface finish, glaze, and depth rather than uniform desaturation or a global color wash.

Describe materials by type, color, finish, and condition. Arrange furniture, machinery, cargo, storage, tools, and equipment according to use, access, circulation, handling, and maintenance. Concentrate fine detail at entrances, inhabited platforms, mechanical junctions, load-bearing connections, and focal structures while preserving quieter structural planes and open voids. Use environmental details as evidence of construction, history, ownership, repeated activity, and function; preserve natural variation in repeated objects and surfaces.

### Prompt Construction and Continuity

Write one concise standalone prompt for the location defined by `stage1_prompt` and represented by the externally attached image. Follow the required order and limits from `Stage 2 Prompt Emphasis and Compression`: two-sentence continuity paragraph, one camera sentence, a larger lighting-color-atmosphere-depth paragraph, then one compact finish-and-exclusions sentence. State only the dominant silhouette, essential fixed architecture, scale cues, and spatial relationships needed to preserve identity. Resolve visible materials through their response to light, color, dense water vapor, atmospheric depth, extreme source-driven halation, and heavy bloom rather than through exhaustive inventory. Refer to the external source only as `the attached image` or `the reference image`; do not claim to have inspected it or include story summary, workflow, or internal source-handling language.

For shot sequences, treat `stage1_prompt` as the master geometry record. Repeat the same resolved materials, placement, background detail, lighting direction, weather, and color relationships across every standalone prompt unless the user requests a change. For a requested camera move, specify path, distance, height, rotation, lens, and final framing; change only what would naturally change.

### Stage 2 Environment Image Edits

Use this optional branch only when the user explicitly requests an edit to an existing live-action environment image. It is independent of the default staged branches and never supplies Stage 3 design evidence. Do not apply it to Stage 1 prompt construction or to existing Stage 3 environment views.

Interpret a user's plain-language request to alter the current environment as an image edit; do not depend on fixed trigger words. Read `environment-style-guide.md` and `scripts/STORY-REFERENCE.md` when the requested change depends on story continuity. Treat the existing live-action environment as the base-scene reference and preserve its camera, composition, architecture, layout, lighting, palette, scale, and all unaffected elements.

When the user attaches another image, determine from the request whether it is the base scene to edit or an asset to add, replace, or alter. Attach the base scene first and an added-asset image second. Use an added-asset image only to preserve the asset's visible identity: silhouette, proportions, materials, colors, distinctive construction, and applicable condition. Do not treat edit attachments as style references. If their roles cannot be determined from the request, ask one concise question.

Write the final edit prompt as a direct instruction to edit the attached base scene, preserve its unaffected visual facts, and use an attached asset reference for the same visible asset in its requested role. Resolve placement, scale, contact, occlusion, damage, and environmental interaction through the user request and story continuity. Return the edit prompt only; image execution is outside this skill.

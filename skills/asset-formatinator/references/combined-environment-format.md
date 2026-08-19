# Combined Environment Format

## Purpose

Use this workflow only when the user selects `Combined`. It replaces the default environment Stage 1 concept and Stage 2 conversion with one MidJourney prompt that directly creates the cinematic environment image. Read `environment-style-guide.md` for project-specific architecture, materials, palette, ornament, technology, and ownership cues.

The user's MidJourney moodboard controls cinematic style, photographic character, color grading, texture, and general visual atmosphere. Do not spend prompt space reconstructing those qualities. Keep material colors, time of day, weather, visibility, and lighting conditions when they are required by the user, story state, registry, or location design.

## Prompt Resolution

Resolve the environment in this order:

1. Location identity, function, scale, and requested story state.
2. Dominant architecture, terrain, vessel structure, or fixed landmark.
3. Concrete layout, circulation, access, and near-, middle-, and far-distance relationships.
4. Construction materials, project motifs, ornament, machinery, and ownership cues from `environment-style-guide.md`.
5. Functional set dressing, activity, and evidence of use required by the brief or continuity.
6. A motivated camera position, framing, focal point, depth order, and deliberate frame boundary.
7. Required time, weather, visibility, and environmental condition.

Name actual visible structures and relationships. Do not substitute planning labels such as `primary landmark`, `key feature`, `main usable space`, or `identity-defining elements`. Translate story-specific proper names into concrete visible descriptions.

Honor a viewpoint explicitly stated or clearly implied by the brief or story. Use an elevated, overhead, distant, or aerial view for a city, island, fleet, skyline, or spatial-layout reveal when appropriate. Otherwise choose a natural on-location viewpoint with readable foreground, middle ground, and background depth.

## MidJourney Prompt Construction

Write one coherent prompt targeting approximately 150 words. Aim for 140-150 words of descriptive prose and never pad the prompt to reach the target. Keep the complete submission concise when MidJourney parameters are included.

Describe the finished image directly as a live-action cinematic environment still. Prioritize concrete architecture, layout, spatial relationships, materials, function, and camera composition. Include only story-required lighting or atmospheric facts. Leave generic cinematography, lens character, film texture, color grading, and stylistic mood to the selected moodboard.

Preserve any user-supplied MidJourney moodboard or personalization parameter exactly and place it after the descriptive prompt. Do not invent a moodboard code, describe the moodboard inside the prompt, or add a second competing style system. Use `--ar 16:9` unless the user explicitly requests another aspect ratio.

The final prompt must describe one complete cinematic environment image. Do not include line-art, concept-sheet, transformation, conversion, reference-image, workflow-stage, approval, model, source-document, or internal reasoning language.

## Registry and Approval

Immediately replace the matching scene variant's `stage1_prompt` with the complete combined MidJourney prompt. This field remains the textual design anchor used by Stage 3. Preserve every other registry field.

Return the grounded brief and combined prompt, then stop for approval. After the user approves the resulting MidJourney image and requests continuation, proceed directly to Stage 3. Do not create a separate environment Stage 2 prompt.

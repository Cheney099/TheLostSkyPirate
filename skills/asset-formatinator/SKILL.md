---
name: asset-formatinator
description: "Create story-reference- and asset-registry-grounded prompts through staged image workflows, including default concept-to-live-action generation and a combined MidJourney environment route, followed by multi-view asset output. Target Seedream for character concepts, MidJourney for environment, prop, and vehicle prompts, and Nano Banana Pro for later stages. Use for characters, crowds, scenes, props, skyships, vehicles, architecture, creatures, and visual effects when project style and story continuity must shape the result."
---

# Image Prompt Generator

Create the prompt required for the current workflow stage. Image execution is outside this skill. Return only the current stage's required prompt artifacts and wait for explicit approval before advancing.

## References

Before generating any prompt, read `scripts/STORY-REFERENCE.md` and the relevant asset-registry records according to `Project Source Loading` below.

Read `references/general-aesthetics.md` for the project's shared visual language. Read the matching asset reference:

- **Characters and crowds:** `references/character-generator.md`
- **Environments:** `references/environment-style-guide.md` for project-specific design, `references/environment-format.md` for the Default workflow, and `references/combined-environment-format.md` for the Combined workflow
- **Props, vehicles, machinery, and automatons:** `references/prop-generator.md`
- **Stage 3 asset views and sheets:** `references/stage3-asset-prompts.md`

Read `scripts/STORY-REFERENCE.md` for established characters, factions, locations, objects, relationships, events, timeline forms, and episode-specific visual states.

`scripts/STORY-REFERENCE.md` supplies prompt-time narrative and visual continuity. The registry supplies canonical reusable asset records. `general-aesthetics.md` supplies shared visual language, and the asset generators define reusable construction and formatting rules.

## Environment Workflow Selection

At the beginning of every new environment-prompt request, determine whether the user explicitly selected `Combined` or `Default`. If neither is stated, return only this question and stop before reading project sources, writing a brief or prompt, or changing the registry:

`Which environment workflow should I use: Combined or Default?`

- **Combined:** use `combined-environment-format.md` to create one direct MidJourney cinematic environment prompt, bypassing the default environment Stage 1 and Stage 2 split.
- **Default:** use `environment-format.md` for the existing MidJourney concept prompt, approval gate, and Nano Banana Pro live-action conversion.

Do not infer the workflow from the requested model, an attachment, prior defaults, or wording such as `environment prompt`. An explicit selection in the current request satisfies the gate. Keep that selection for follow-up stages and revisions of the same environment asset unless the user changes it. A prompt-only request does not bypass this gate.

## Project Source Loading

Resolve these paths from the repository root:

- `scripts/STORY-REFERENCE.md`: canonical prompt-time story and visual-continuity source
- `scripts/*.pdf`: source screenplays used only when the user explicitly asks to refresh `STORY-REFERENCE.md`; do not read them during ordinary asset prompting
- `asset_registry/characters/`: characters, crowds, and age or wardrobe forms
- `asset_registry/props/`: props, weapons, vehicles, machinery, and automatons
- `asset_registry/scenes/`: locations and persistent spaces

Before writing any Combined environment, Stage 1, Stage 2, Stage 3, revision, direct-generation, or prompt-only prompt:

1. Read the complete `scripts/STORY-REFERENCE.md`. Do not open or reread any screenplay PDF during this workflow.
2. Identify the requested asset, applicable age or wardrobe form, location, relevant scene, and any related reusable assets.
3. Read the complete matching registry JSON for each relevant character, crowd, prop, vehicle, machine, or scene. Search IDs, names, and screenplay aliases when the match is not immediately clear.
4. Use registry `description`, `attributes`, the applicable base or requested variant `appearance`, and any real non-null `image` metadata to identify and ground the correct asset before Stage 1. For Stage 2 and Stage 3, require and read the selected variant's non-null `stage1_prompt`; it is the sole source for established Stage 1 design decisions. Do not derive downstream design facts from registry image metadata.
5. Use `scripts/STORY-REFERENCE.md` for narrative identity, relationships, timeline form, scene-specific action, and temporary visible conditions. Include a temporary condition only when the requested image represents that episode or story state.

Use the registry as the canonical reusable asset record and `scripts/STORY-REFERENCE.md` as the canonical prompt-time narrative source. Select the registry form that matches the requested episode or story state; never blend separate age, life-stage, or wardrobe records into one design. If the sources materially conflict and the correct form cannot be established, ask one concise question rather than silently choosing.

Do not invent a registry match for an unregistered generic asset. In that case, use the user brief, `scripts/STORY-REFERENCE.md` when relevant, and the project style references. Source loading supplies facts only and never overrides the selected stage's content and formatting limits.

## Brief Resolution

Identify the asset type, requested subject, intended use, required visible facts, current workflow stage, and supplied images.

For a sparse brief, use `scripts/STORY-REFERENCE.md`, matching registry records, and project references to resolve missing design facts conservatively. For a detailed brief, preserve its stated identity, costume, materials, composition, camera, lighting, and required details. Correct literal terms that conflict with the project's period, technology, faction logic, or worldbuilding by selecting the closest visible project-appropriate equivalent that preserves the user's intent.

Do not normalize or correct the brief when the user explicitly requests strict literal use. Mandatory stage formatting still applies.

For either environment workflow and for the default staged workflow used by other asset types, write one concise grounded design brief containing only visible design decisions needed by the image model. Keep internal research, selection rationale, plot summary, and story-specific proper names out of it.

## Combined Environment Workflow

Use this route only after the user selects `Combined`. Read `environment-style-guide.md` and `combined-environment-format.md`, then write one MidJourney prompt that directly creates the cinematic environment image. The moodboard controls cinematic style; the prompt supplies the concrete location, architecture, layout, materials, function, story state, and composition required for continuity.

Return the grounded brief and final combined prompt, immediately replace the matching scene variant's `stage1_prompt` with that complete prompt, and stop for approval. After the user approves the resulting MidJourney image and asks to continue, proceed directly to Stage 3. Do not write an environment Stage 2 prompt for this route.

## Default Three-Stage Workflow

This is the Default workflow. Stage 1 is the canonical textual design anchor for both downstream stages. The skill itself reads only text and never inspects, verifies, generates, or internally requires an image. Stage 2 prompt wording assumes the user will attach the Stage 1 image externally. Stage 3 prompt wording assumes the user will attach the approved cinematic source image externally. Write either prompt without checking whether that external attachment currently exists.

### Stage 1: Concept Design

Write the concept prompt using the matching generator:

- **Single character or crowd:** use Seedream with `character-generator.md`.
- **Environment:** after the user selects `Default`, use MidJourney with `environment-style-guide.md` and `environment-format.md`.
- **Prop, vehicle, machinery, or automaton:** use MidJourney with `prop-generator.md`.

The matching generator owns the concept style, composition, aspect ratio, content order, and word limit. Do not add a generic concept treatment from this file.

Return the grounded brief and final prompt, then stop. Do not write Stage 2 or Stage 3 until the user approves the Stage 1 prompt and asks to continue with the selected branch.

Whenever a final Stage 1 prompt is produced, immediately replace the matching registry variant's current `stage1_prompt` with that complete prompt. Replacement is scoped to that one variant: preserve every other field and every other asset's log. Do not append prompt history or retain the superseded prompt. Characters and crowds write under `asset_registry/characters/`; props, vehicles, machinery, and automatons write under `asset_registry/props/`; environments write under `asset_registry/scenes/`. Stage 1 prompt-only work follows the same replacement rule. Do not write Stage 1 without a resolved registry variant; establish the record through the project's registry workflow first.

### Stage 2: Live-Action Image

Require the matching variant's non-null `stage1_prompt`. Read it directly, extract the stable design decisions appropriate to the asset type, discard its Stage 1 presentation instructions, and apply the selected Stage 2 visual layer. The final prompt must tell the image model to use the attached image as its visual source; this means the Stage 1 image that the user attaches externally. Do not inspect, verify, request, or internally require that image before writing the prompt.

- **Single character or crowd:** `Nano Banana Pro Photo Format` in `character-generator.md`
- **Environment:** for the `Default` workflow only, use `Stage 2: Nano Banana Pro Film Still Format` in `environment-format.md`, with `environment-style-guide.md` read internally
- **Prop, vehicle, machinery, or automaton:** `Nano Banana Pro Prop Format` in `prop-generator.md`

Return the Stage 2 prompt, then stop. Do not automatically continue to Stage 3.

For an explicit edit to an existing live-action environment image, use only the optional `Stage 2 Environment Image Edits` branch in `environment-format.md`. This edit branch may use user-supplied image references, but it does not become a Stage 3 dependency.

### Stage 3: Multi-View Asset

Require the matching variant's non-null `stage1_prompt`, then read `references/stage3-asset-prompts.md` and select the route for the asset. Every final Stage 3 prompt must tell the image model to use the attached approved cinematic image. For the Default workflow this is the Stage 2 image; for a Combined environment this is the direct MidJourney image. The skill does not inspect, verify, request, or internally require that image. Classify non-character assets by physical scale and spatial role as `Human-Scale Props`, `Large Floor-Supported Props`, `Large Flight-Capable Props`, or `Environments`.

For a character, human-scale prop, or special element, derive the written fixed design directly from `stage1_prompt` and return one Nano Banana Pro prompt for an already-stitched asset sheet. Apply the Stage 3 photographic, material, lighting, view, and measurement rules. Refer to the externally attached Stage 2 image as the visual continuity source. An explicitly supplied face reference may be used only by the optional face-lock branch. The prompt must not request external assembly.

For a large floor-supported or flight-capable prop, require an explicit Stage 3 view selection before loading project sources or writing prompts. If the user has not selected `Low Front Three-Quarter`, `Low Side Profile`, `Low Rear Three-Quarter`, `High Oblique Aerial`, or `All Four`, ask exactly: `Which Stage 3 view would you like: Low Front Three-Quarter, Low Side Profile, Low Rear Three-Quarter, High Oblique Aerial, or All Four?` Then stop. The user may select one view or a named subset. Generate all four only when the user explicitly requests all four.

For each selected large-prop view, return one complete Nano Banana Pro prompt of no more than 150 words, excluding its external chat label. Derive from `stage1_prompt` a short generic asset category and a factual design lock of three to five noun-led items totaling no more than 35 words. Include only the dominant structural form, primary movement or propulsion, and the few largest identity-critical features; never copy or closely paraphrase the complete Stage 1 prompt or list minor mechanisms. Choose one aspect ratio from the asset's silhouette and use it consistently across every selected prompt. Repeat the same compact design lock, full-scale dark-showroom presentation, neutral illumination, support treatment, and identical size caption in every returned prompt. Label each returned view separately in the chat immediately before its prompt block; keep those labels outside the prompt text. Never combine these views into one image.

For an environment, use `stage1_prompt` for concrete architecture, layout, circulation, scale, fixed mechanisms, landmarks, usable spaces, and explicit spatial relationships, then return three complete Nano Banana Pro prompts. Each prompt refers to the externally attached approved cinematic environment image. Each prompt creates one standalone 16:9 view from the camera position assigned in `stage3-asset-prompts.md`; never combine the views into one image. If `stage1_prompt` is absent, stop rather than reconstructing the approved design from generic registry text or an image.

Crowds stop after Stage 2. They have no Stage 3 sheet or measurement caption.

## Revisions

For a targeted revision, read the matching asset generator and the project references needed to resolve continuity. Preserve every approved and unspecified visual fact and change only the requested delta.

When revising or regenerating a Stage 1 asset or Combined environment prompt, build one complete standalone prompt that includes the preserved design and requested change, then immediately replace that variant's `stage1_prompt` with the complete prompt. Never store a delta-only edit instruction as the Stage 1 log. Stage 2 and Stage 3 revisions do not change `stage1_prompt`.

Return the revision prompt only. Image execution is outside this skill.

## Exceptions

- **Different model requested:** use the named model for that stage while preserving the workflow and approval gates.
- **Prompt or prompt-only requested:** return only the requested final prompt or prompts. Do not return a grounded brief, planning notes, preservation list, or workflow explanation. A Stage 1 prompt still replaces the matching `stage1_prompt`.
- **Existing Stage 1 prompt supplied:** store it in the matching variant, replacing the prior `stage1_prompt`, then begin Stage 2 or Stage 3 as requested.
- **External image attachments:** never inspect, verify, or require them locally. Still include the required attached-image wording: Stage 2 addresses the externally attached Stage 1 image, and Stage 3 addresses the externally attached approved cinematic image.
- **Direct Nano Banana Pro prompt requested:** write a grounded brief and one Nano Banana Pro prompt without Stage 1. Do not run it.
- **Crowd requested:** write prompts through Stage 2 only.
- **Material ambiguity:** ask one concise question only when the missing fact would materially change identity, continuity, or composition. Otherwise infer conservatively.

The prompt-only exception takes precedence over every output format in this skill.

## Universal Final-Prompt Rules

- Describe the finished visible image directly and coherently.
- Keep story-specific proper names internal at every stage. This includes names and aliases for characters, factions, organizations, families, locations, vessels, objects, episodes, and events. Translate them into concrete visible design evidence.
- Use story references as internal evidence only. Do not include plot, chronology, causality, narrative summary, or nonvisual character interpretation.
- Do not mention workflow stages, approval status, source documents, style guides, model names, production instructions, or internal reference-handling logic.
- Include attached-image language in every Stage 2 and Stage 3 prompt. This language addresses the external image model and does not mean the skill has inspected or verified an image.
- Ground people, text, logos, magic, weapons, and decorative elements in the brief, `scripts/STORY-REFERENCE.md`, matching registry records, logged Stage 1 prompt, or project references.
- Preserve the role assigned to each external reference: Stage 1 image for Default Stage 2 visual conversion; the Default Stage 2 image or Combined MidJourney image for Stage 3 visual continuity; and any optional face or edit reference only within its explicitly assigned scope.
- Follow the selected generator for all asset-specific prompt content and formatting.

## Output Contract

Return only the artifacts required by the active branch:

- **Default workflow stage:** grounded design brief, final prompt or prompts, and approval checkpoint
- **Combined environment workflow:** grounded design brief, final combined prompt, and approval checkpoint
- **Prompt-only request:** final prompt or prompts alone
- **Revision prompt request:** revision prompt alone

Never advance through an approval checkpoint in the same response unless the user explicitly supplied approval and requested the next stage.

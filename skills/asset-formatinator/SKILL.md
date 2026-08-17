---
name: asset-formatinator
description: "Create and execute a screenplay- and asset-registry-grounded LibTV Agent image workflow: generate a concept design, wait for approval, create a Nano Banana Pro live-action image, then create a Nano Banana Pro multi-view asset output after final approval. Use Seedream for character concepts and MidJourney for environment, prop, and vehicle concepts. Use for characters, crowds, scenes, props, skyships, vehicles, architecture, creatures, and visual effects when project style and story continuity must shape the result."
---

# Image Prompt Generator

Create the prompt and LibTV Agent image node required for the current workflow stage. Prompts are required artifacts at every stage. Run only the current stage, retain its result on the canvas, report the generated image, and wait for explicit approval before advancing.

## References

Before generating any prompt, read the current screenplay and the relevant asset-registry records according to `Project Source Loading` below.

Read `references/general-aesthetics.md` for the project's shared visual language. Read the matching asset reference:

- **Characters and crowds:** `references/character-generator.md`
- **Environments:** `references/environment-style-guide.md` for project-specific design and `references/environment-format.md` for Stage 1 and Stage 2 construction
- **Props, vehicles, machinery, and automatons:** `references/prop-generator.md`
- **Stage 3 sheets:** `references/stage3-asset-prompts.md`

Read `references/STORY-REFERENCE.md` as a secondary continuity summary when the request depends on an established character, faction, location, object, relationship, event, or timeline form. It does not override the screenplay or registry.

The project screenplay and registry supply narrative and asset continuity. `general-aesthetics.md` supplies shared visual language, and the asset generators define reusable construction and formatting rules.

## Project Source Loading

Resolve these paths from the repository root:

- `scripts/`: canonical screenplay files
- `asset_registry/characters/`: characters, crowds, and age or wardrobe forms
- `asset_registry/props/`: props, weapons, vehicles, machinery, and automatons
- `asset_registry/scenes/`: locations and persistent spaces

Before writing any Stage 1, Stage 2, Stage 3, revision, direct-generation, or prompt-only prompt:

1. Read the complete current screenplay from `scripts/`. When several scripts exist, select the one named by the user or the one containing the requested asset and scene context.
2. Identify the requested asset, applicable age or wardrobe form, location, relevant scene, and any related reusable assets.
3. Read the complete matching registry JSON for each relevant character, crowd, prop, vehicle, machine, or scene. Search IDs, names, and screenplay aliases when the match is not immediately clear.
4. Use registry `description`, `attributes`, the applicable base or requested variant `appearance`, and any real non-null `image` metadata as stable continuity evidence.
5. Use the screenplay for narrative identity, relationships, timeline form, scene-specific action, and temporary visible conditions. Include a temporary condition only when the requested image represents that scene or state.

Use the registry as the canonical reusable asset record and the screenplay as the canonical narrative source. Select the registry form that matches the screenplay scene; never blend separate age, life-stage, or wardrobe records into one design. If the sources materially conflict and the correct form cannot be established, ask one concise question rather than silently choosing.

Do not invent a registry match for an unregistered generic asset. In that case, use the user brief, screenplay evidence when present, and the project style references. Source loading supplies facts only and never overrides the selected stage's content and formatting limits.

## Brief Resolution

Identify the asset type, requested subject, intended use, required visible facts, current workflow stage, and supplied images.

For a sparse brief, use the screenplay, matching registry records, and project references to resolve missing design facts conservatively. For a detailed brief, preserve its stated identity, costume, materials, composition, camera, lighting, and required details. Correct literal terms that conflict with the project's period, technology, faction logic, or worldbuilding by selecting the closest visible project-appropriate equivalent that preserves the user's intent.

Do not normalize or correct the brief when the user explicitly requests strict literal use. Mandatory stage formatting still applies.

For the default generation workflow, write one concise grounded design brief containing only visible design decisions needed by the image model. Keep internal research, selection rationale, plot summary, and story-specific proper names out of it.

## Three-Stage Workflow

Each later stage uses the selected, user-approved result from the preceding stage.

### Stage 1: Concept Design

Write the concept prompt using the matching generator:

- **Single character or crowd:** use Seedream with `character-generator.md`.
- **Environment:** use MidJourney with `environment-style-guide.md` and `environment-format.md`.
- **Prop, vehicle, machinery, or automaton:** use MidJourney with `prop-generator.md`.

The matching generator owns the concept style, composition, aspect ratio, content order, and word limit. Do not add a generic concept treatment from this file.

Create and run one LibTV Agent canvas image node using the routed model. Put the prompt in its prompt field and retain the result. Return the grounded brief, prompt, node, and generated image, then stop. Do not create Stage 2 until the user explicitly approves a selected concept and asks to continue.

### Stage 2: Live-Action Image

Attach the approved Stage 1 image as Nano Banana Pro's primary design reference and use the matching Stage 2 section:

- **Single character or crowd:** `Nano Banana Pro Photo Format` in `character-generator.md`
- **Environment:** `Stage 2: Nano Banana Pro Film Still Format` in `environment-format.md`, with `environment-style-guide.md` read internally
- **Prop, vehicle, machinery, or automaton:** `Nano Banana Pro Prop Format` in `prop-generator.md`

Create and run one new Nano Banana Pro canvas image node, retain the result, and return the prompt, node, and generated image. Stop until the user explicitly approves the result and asks to continue.

For an edit to an existing live-action environment, use only the `Stage 2 Environment Image Edits` branch in `environment-format.md`. Complete and approve the edit before Stage 3.

### Stage 3: Multi-View Asset

Read `references/stage3-asset-prompts.md` and select the route for the approved Stage 2 image. Classify non-character assets by physical scale and spatial role as `Human-Scale Props`, `Large Props`, or `Environments`.

For a character, prop, or special element, create and run one Nano Banana Pro canvas image node that generates one already-stitched asset sheet. Attach the approved Stage 2 image first. For a face-locked character sheet, attach the approved face reference second. Do not generate separate views or assemble them outside the image node.

For an environment, return three complete prompts and create three separate Nano Banana Pro canvas image nodes. Attach the same approved Stage 2 environment image to every node. Each node generates one standalone 16:9 view from the camera position assigned in `stage3-asset-prompts.md`; never combine the views into one image.

Crowds stop after Stage 2. They have no Stage 3 sheet or measurement caption.

## Revisions

For a targeted revision, read the matching asset generator and the project references needed to resolve continuity. Preserve every approved and unspecified visual fact and change only the requested delta.

Create and run a new Nano Banana Pro revision node only when the user requests image generation. Otherwise return the revision prompt alone.

## Exceptions

- **Different model requested:** use the named model for that stage while preserving the workflow and approval gates.
- **Prompt or prompt-only requested:** return only the requested final prompt or prompts. Do not return a grounded brief, planning notes, preservation list, workflow explanation, or node.
- **Approved concept supplied:** begin at Stage 2 when the user asks to continue.
- **Approved live-action image supplied:** begin at revision or Stage 3 according to the request.
- **Direct Nano Banana Pro generation requested:** write a grounded brief and one Nano Banana Pro prompt, then create and run one node without Stage 1.
- **Crowd requested:** generate through Stage 2 only.
- **Material ambiguity:** ask one concise question only when the missing fact would materially change identity, continuity, or composition. Otherwise infer conservatively.

The prompt-only exception takes precedence over every output format in this skill.

## Universal Final-Prompt Rules

- Describe the finished visible image directly and coherently.
- Keep story-specific proper names internal at every stage. This includes names and aliases for characters, factions, organizations, families, locations, vessels, objects, episodes, and events. Translate them into concrete visible design evidence.
- Use story references as internal evidence only. Do not include plot, chronology, causality, narrative summary, or nonvisual character interpretation.
- Do not mention workflow stages, approval status, source documents, style guides, model names, production instructions, or internal reference-handling logic.
- Include image-reference language only when the image model needs it to identify an attached visual source.
- Ground people, text, logos, magic, weapons, and decorative elements in the brief, approved image, screenplay, matching registry records, or project references.
- Preserve an approved image over a general style rule when they conflict.
- Follow the selected generator for all asset-specific prompt content and formatting.

## Output Contract

Return only the artifacts required by the active branch:

- **Default generation stage:** grounded design brief, final prompt or prompts, created node or nodes, generated image or images, and approval checkpoint
- **Prompt-only request:** final prompt or prompts alone
- **Revision prompt request:** revision prompt alone
- **Generated revision:** revision prompt, created node, and generated image

Never advance through an approval checkpoint in the same response unless the user explicitly supplied approval and requested the next stage.

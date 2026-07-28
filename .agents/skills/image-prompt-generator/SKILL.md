---
name: image-prompt-generator
description: "Create and execute a project-grounded hybrid image workflow: generate character concepts with Dreamina Seedream 5.0 Pro through Image Workbench, generate environment, prop, and vehicle concepts with MidJourney through LibTV CLI model 悠船 V8.1, then generate Nano Banana Pro live-action images and multi-view asset sheets through Image Workbench after approval. Use for characters, crowds, scenes, props, skyships, vehicles, architecture, creatures, and visual effects when project style and story continuity must shape the result."
---

# Image Prompt Generator

Create the prompt and generated image required for the current workflow stage. Prompts are required artifacts at every stage. Run only the current stage, report every generated result and local file path, and wait for explicit approval before advancing.

## Tool Contracts

Before generation, read and follow:

- `C:\Users\Zhiyuan Chen\.codex\skills\image-workbench\SKILL.md`
- `C:\Users\Zhiyuan Chen\.codex\skills\libtv-cli\SKILL.md`

Use Image Workbench through `scripts/workbench.py`; do not reimplement its HTTP calls, provider calls, or polling. Use LibTV only through the `libtv` CLI; do not invent direct LibTV HTTP requests.

Default routing:

- Character or crowd concept: Image Workbench `--model dreamina --resolution 2K`
- Environment, prop, vehicle, machinery, or automaton concept: LibTV CLI image node with support-model display name `悠船 V8.1`, resolving to `mj-v8.1 / Midjourney V8.1`
- Live-action conversion, revision, and Stage 3 sheet: Image Workbench `--model nano --resolution 4K --count 1`
- Output root: `<project-root>\DesignSheet\generated\<asset-slug>\<stage-folder>`

Before every paid Image Workbench generation, run `python $runner status`. Pass references by repeating `--reference "<absolute-path>"`. Report every successful `file`, exact `error`, and `submitId`. If a job remains querying or times out, continue from the existing job state and do not resubmit it. Never silently switch providers after failure and do not stop the workbench unless the user asks.

Before every paid LibTV generation, verify login, canvas binding, and the live schema with `libtv model search --type image "8.1"` and `libtv model "悠船 V8.1"`. Bind the intended canvas with `libtv project use <canvas-uuid>`. Use the exact support-model display name `悠船 V8.1` in `-s model=...`. Create and synchronously run a uniquely named image node:

```powershell
libtv node create "<asset-slug>-concept-<unique-suffix>" -t image `
  --prompt "<prompt>" `
  -s "model=悠船 V8.1" `
  -s "ratio=<supported-ratio>" `
  -s "quality=auto" `
  -s "stylize=100" `
  -s "weird=50" `
  -s "chaos=5" `
  -s "count=4" `
  --run
```

Treat the final stdout JSON as the source of truth. `--run` already waits and polls; do not background it or add another polling loop. Retain all four concept results for selection. After approval, save the selected result locally before passing it to Image Workbench as Stage 2's first reference.

When the user requests several Image Workbench generations in parallel, run one independent generation per source image concurrently after a status check for every submission. Keep each task's stdout and stderr separate, monitor existing jobs without duplicate submission, and verify every downloaded image. If the user requests one delivery folder, copy the verified outputs into that folder with asset-specific filenames while preserving the original per-asset outputs.

## References

Read `references/general-aesthetics.md` for the project's shared visual language. Read the matching asset reference:

- **Characters and crowds:** `references/character-generator.md`
- **Environments:** `references/environment-style-guide.md` for project-specific design and `references/environment-format.md` for Stage 1 and Stage 2 construction
- **Props, vehicles, machinery, and automatons:** `references/prop-generator.md`
- **Stage 3 sheets:** `references/stage3-asset-prompts.md`

Read `references/STORY-REFERENCE.md` when the request depends on an established character, faction, location, object, relationship, event, or timeline form.

Project-specific information belongs in `general-aesthetics.md` and `STORY-REFERENCE.md`. The asset generators define reusable construction and formatting rules.

## Brief Resolution

Identify the asset type, requested subject, intended use, required visible facts, current workflow stage, and supplied images.

For a sparse brief, use the project references to resolve missing design facts conservatively. For a detailed brief, preserve its stated identity, costume, materials, composition, camera, lighting, and required details. Correct literal terms that conflict with the project's period, technology, faction logic, or worldbuilding by selecting the closest visible project-appropriate equivalent that preserves the user's intent.

Do not normalize or correct the brief when the user explicitly requests strict literal use. Mandatory stage formatting still applies.

For the default generation workflow, write one concise grounded design brief containing only visible design decisions needed by the image model. Keep internal research, selection rationale, plot summary, and story-specific proper names out of it.

## Three-Stage Workflow

Each later stage uses the selected, user-approved result from the preceding stage.

### Stage 1: Concept Design

Write the concept prompt using the matching generator:

- **Single character or crowd:** use Dreamina Seedream 5.0 Pro through Image Workbench with `character-generator.md`.
- **Environment:** use MidJourney through LibTV CLI model `悠船 V8.1` with `environment-style-guide.md` and `environment-format.md`.
- **Prop, vehicle, machinery, or automaton:** use MidJourney through LibTV CLI model `悠船 V8.1` with `prop-generator.md`.

The matching generator owns the concept style, composition, aspect ratio, content order, and word limit. Do not add a generic concept treatment from this file.

For a character or crowd, run one Image Workbench Dreamina generation and save it under `step-01-concept`. For an environment, prop, vehicle, machinery, or automaton, create and run one LibTV CLI 悠船 V8.1 image node, retain all four results on the canvas, and wait for the user to select one. Return the grounded brief, prompt, generation result, and image or image paths, then stop. Do not create Stage 2 until the user explicitly approves a selected concept and asks to continue.

### Stage 2: Live-Action Image

Attach the approved Stage 1 image as Nano Banana Pro's primary design reference and use the matching Stage 2 section:

- **Single character or crowd:** `Nano Banana Pro Photo Format` in `character-generator.md`
- **Environment:** `Stage 2: Nano Banana Pro Film Still Format` in `environment-format.md`, with `environment-style-guide.md` read internally
- **Prop, vehicle, machinery, or automaton:** `Nano Banana Pro Prop Format` in `prop-generator.md`

Run one Image Workbench Nano Banana Pro generation with `--model nano --resolution 4K --count 1`, the approved Stage 1 image as the first `--reference`, and a supported ratio. Save it under `step-02-live-action`, then return the prompt, `submitId`, and local generated image path. Stop until the user explicitly approves the result and asks to continue.

For an edit to an existing live-action environment, use only the `Stage 2 Environment Image Edits` branch in `environment-format.md`. Complete and approve the edit before Stage 3.

### Stage 3: Multi-View Asset

Read `references/stage3-asset-prompts.md` and select exactly one template for the approved Stage 2 image. Classify non-character assets by physical scale and spatial role as `Human-Scale Props`, `Large Props`, or `Environments`.

Run one Image Workbench Nano Banana Pro generation with `--model nano --resolution 4K --count 1` that generates one already-stitched asset sheet. Attach the approved Stage 2 image first. For a face-locked character sheet, attach the approved face reference second. Save it under `step-03-multiview`. Do not generate separate views or assemble them outside the generated image.

Crowds stop after Stage 2. They have no Stage 3 sheet or measurement caption.

## Revisions

For a targeted revision, read the matching asset generator and the project references needed to resolve continuity. Preserve every approved and unspecified visual fact and change only the requested delta.

Run a new Image Workbench Nano Banana Pro revision only when the user requests image generation. Save it under `step-02-revision`. Otherwise return the revision prompt alone.

## Exceptions

- **Different model requested:** use the named model only when the active Image Workbench or LibTV CLI supports it; otherwise report the unsupported model without silently substituting another provider.
- **Prompt or prompt-only requested:** return only the requested final prompt or prompts. Do not return a grounded brief, planning notes, preservation list, workflow explanation, or generation command.
- **Approved concept supplied:** begin at Stage 2 when the user asks to continue.
- **Approved live-action image supplied:** begin at revision or Stage 3 according to the request.
- **Direct Nano Banana Pro generation requested:** write a grounded brief and one Nano Banana Pro prompt, then run one Image Workbench Nano Banana Pro generation without Stage 1.
- **Crowd requested:** generate through Stage 2 only.
- **Material ambiguity:** ask one concise question only when the missing fact would materially change identity, continuity, or composition. Otherwise infer conservatively.

The prompt-only exception takes precedence over every output format in this skill.

## Universal Final-Prompt Rules

- Describe the finished visible image directly and coherently.
- Keep story-specific proper names internal at every stage. This includes names and aliases for characters, factions, organizations, families, locations, vessels, objects, episodes, and events. Translate them into concrete visible design evidence.
- Use story references as internal evidence only. Do not include plot, chronology, causality, narrative summary, or nonvisual character interpretation.
- Do not mention workflow stages, approval status, source documents, style guides, model names, production instructions, or internal reference-handling logic.
- Include image-reference language only when the image model needs it to identify an attached visual source.
- Ground people, text, logos, magic, weapons, and decorative elements in the brief, approved image, or project references.
- Preserve an approved image over a general style rule when they conflict.
- Follow the selected generator for all asset-specific prompt content and formatting.

## Output Contract

Return only the artifacts required by the active branch:

- **Default generation stage:** grounded design brief, final prompt, generation result, generated image path, and approval checkpoint
- **Prompt-only request:** final prompt alone
- **Revision prompt request:** revision prompt alone
- **Generated revision:** revision prompt, generation result, and generated image path

Never advance through an approval checkpoint in the same response unless the user explicitly supplied approval and requested the next stage.

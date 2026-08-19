# Registry Format

## Asset Test

Register something only when it has an independent identity that must remain consistent across segments or episodes.

Register:

- Every named character and every recurring human group whose appearance needs continuity.
- Plot-significant or recurring physical objects.
- Vehicles, robots, automatons, weapons, tools, and machinery as props.
- Distinct locations and persistent interior or exterior spaces as scenes.

Do not register:

- Incidental generic objects that require no continuity.
- Actions, emotions, poses, injuries, dirt, wetness, damage, activation state, or other temporary conditions.
- Light beams, flames, smoke, dust, sparks, debris, cracks, reflections, energy, weather responses, or similar
  dependent visual phenomena.

Assign dependent phenomena to the character, prop, machine, vehicle, or scene that carries them when writing a segment prompt.
Do not store those temporary conditions in registry JSON.

A permanent scar, birthmark, tattoo, integrated lamp, sensor, or other stable physical feature belongs inside the owning
character or prop's universal appearance. Whether clothing, pose, activation, or framing reveals that feature in a particular
segment belongs in the segment brief and `【视频内容】`.

## Deduplication

- Resolve aliases and repeated mentions before creating IDs.
- Keep one asset when the script clearly refers to the same identity or object in the same age/life-stage and wardrobe form.
- Create a separate character asset JSON for each distinct age/life-stage or outfit form established by the screenplay. Give
  every form its own top-level ID, filename, name, appearance, and base variant; do not place these forms together as variants
  inside one character record.
- When age/life-stage and outfit both differ, register only the combinations that actually occur in the screenplay. Do not
  generate a theoretical set of combinations.
- Share confirmed universal identity facts, such as voice or movement behavior, across related form records when those facts
  remain true. Keep form-specific appearance in each form's own base variant.
- Do not split an asset for a passing accessory, removed outer layer, partial disguise, or other minor presentation change
  unless the screenplay establishes it as a distinct reusable wardrobe form.
- Variants may still represent legitimate reusable forms of non-character assets when separate top-level identities are not
  warranted.
- Do not create variants for one-scene damage, attached fire, dirt, injuries, active lights, temporary props, or pose changes.
- When identity is genuinely ambiguous, do not guess. Record the ambiguity in the delivery report and leave the existing files
  unchanged.

## File Schema

Use one JSON file per asset. The filename must equal the top-level `id` plus `.json`.

```json
{
  "id": "Char-Example",
  "type": "character",
  "name": "Example",
  "description": "Adult; low-pitched, rough masculine voice with a regional accent; 175 cm tall.",
  "attributes": {
    "height": "175 cm",
    "voice": {
      "gender": "masculine",
      "pitch": "low",
      "timbre": "rough",
      "accent": "regional"
    }
  },
  "variants": [
    {
      "id": "Char-Example-Base",
      "status": "Base",
      "is_base": true,
      "appearance": "Reusable canonical appearance with no segment-specific condition.",
      "stage1_prompt": null,
      "image": null
    }
  ]
}
```

Allowed top-level `type` values:

- `character`
- `prop`
- `scene`

Allowed ID prefixes:

- `Char-`
- `Prop-`
- `Scene-`

Every file must contain exactly one base variant. Variant IDs remain stable after creation.

Every variant also contains `"stage1_prompt": null` until the matching concept workflow writes its exact Stage 1 prompt.

## Universal Attributes

Use `attributes` only for facts that should remain consistent whenever the asset appears. Character age/life stage, height,
and voice are required and follow the controlled inference rules below. Omit other unsupported fields instead of guessing.

Character fields may include:

```json
{
  "height": "string",
  "voice": {
    "gender": "string",
    "pitch": "string",
    "timbre": "string",
    "accent": "string"
  },
  "movement": "string",
  "sound": "string"
}
```

For characters, `attributes.voice` and `attributes.height` are the canonical structured values. Character movement or sound
may remain in `attributes` only when it is a universal identity trait.

## Character Inference

Infer character age/life stage, approximate height, and voice from the complete screenplay alone. Do not read or use a
storyboard, reference image, generated prompt, segment mapping, or existing visual design as evidence for these fields.

Use evidence in this order:

1. Direct screenplay statements, including stated ages, measurements, casting notes, and voice or delivery descriptions.
2. Strong screenplay context, including time jumps, family relationships, occupation, physical interactions, relative scale,
   dialogue register, and speaking style.
3. A single plausible production interpretation consistent with the character's established life stage and dramatic function.

Requirements:

- Use a specific age when the screenplay supplies one; otherwise use a stable life stage or approximate range.
- Store height as one approximate metric measurement. Use relative screenplay evidence when available; otherwise choose a
  plausible value and keep it consistent.
- Populate `attributes.voice.gender`, `pitch`, `timbre`, and `accent` for every individual character. Infer vocal qualities from
  dialogue, delivery notes, setting, and characterization without copying dialogue or catchphrases.
- Do not infer nationality, ethnicity, or a specific regional accent without screenplay support. When no specific accent is
  supported, use a neutral accent appropriate to the screenplay's dialogue language.
- Related outfit assets at the same age/life stage must share height and voice unless the screenplay establishes a lasting
  difference. Different age/life-stage assets may change both.
- Keep the result internally consistent across the full screenplay. Do not offer multiple alternatives inside JSON.
- If direct screenplay evidence conflicts irreconcilably, preserve the stronger explicit fact and report the conflict outside
  the JSON. Do not add confidence, evidence, rationale, or provenance fields.

For props, vehicles, robots, and machines, place all reusable structure, scale, movement, operation, and characteristic sound
information together in `description`, written as concise natural language. Interpret the asset's general physical function
instead of copying its role in the screenplay. Exclude owners, users, targets, relationships, locations, plot events, and the
reason the asset appears. Keep specific identity in `id` and `name`, and visual design in `appearance`. Do not create or retain
separate `dimensions`, `movement`, `operation`, or `sound` fields for these assets. Keep the required `attributes` object empty
unless the established schema already contains unrelated metadata that must be preserved.

Scene fields may include:

```json
{
  "layout": "string",
  "scale": "string",
  "persistent_lighting": "string",
  "ambient_sound": "string"
}
```

For universal character movement and scene layout, describe actual behavior or structure rather than broad labels. For props,
apply the same specificity inside the single natural-language `description`.

## Appearance And Image

- A character `description` contains only its age/life stage, voice, and height. Do not put facial features, body shape, hair,
  clothing, accessories, pose, action, emotion, or temporary condition there. Keep voice and height consistent with the
  canonical structured values in `attributes`.
- A prop, vehicle, robot, or machine `description` is a generic reusable brief, naturally combining physical function, stable
  structure, scale, movement, operation, and characteristic sound without labels or subsections. It must remain valid outside
  the screenplay scene and must not narrate who owns, uses, deploys, encounters, or is affected by the asset.
- A scene `description` identifies the location and its universal function.
- `stage1_prompt` stores the matching generator's exact final Stage 1 prompt. For every asset type, it is the local agent's sole textual source for established design decisions in both Stage 2 and Stage 3. Stage 2 prompt wording assumes the user externally attaches the Stage 1 image, and Stage 3 prompt wording assumes the user externally attaches the Stage 2 image; those images are never inspected or verified by the local agent. The screenplay-only registry workflow initializes `stage1_prompt` as `null`, never infers it, and preserves any non-null value exactly. Producing a new complete Stage 1 prompt for that same variant replaces it immediately; replacement never affects another variant and never stores prompt history.
- `variants[].appearance` contains the stable reusable visual form. For a character, it describes only the age/life-stage and
  wardrobe form named by that top-level asset; alternate ages or outfits belong in separate character JSON files.
- Do not include camera direction, aspect ratio, delivery resolution, temporary condition, current pose, current emotion, or
  current action in `appearance`.
- Preserve an existing non-null `image` object exactly unless the user explicitly replaces the reference image.
- When no real image exists, write `"image": null`; never fabricate keys, hashes, byte counts, timestamps, or history.
- A non-null image object follows this shape:

```json
{
  "key": "path/to/image.png",
  "etag": "real-etag",
  "bytes": 123,
  "updated_at": "real timestamp",
  "updated_by": null,
  "history": []
}
```

## Updating Existing Files

- Read the existing record and all variants before editing.
- Preserve stable IDs, approved appearance text, image metadata, and non-null `stage1_prompt` values.
- When an existing character record combines distinct age/life-stage or outfit forms as variants, split those forms into
  separate top-level assets without inventing unsupported appearance details. Preserve each real image object with the form it
  depicts, and report any uncertain mapping instead of guessing.
- Add newly established universal facts without replacing stronger manually authored detail with weaker inference.
- When updating a prop, vehicle, robot, or machine, merge existing `dimensions`, `movement`, `operation`, and `sound` values
  into one concise natural-language `description`, remove story-specific context, then remove those duplicate fields from
  `attributes`.
- When updating a character, remove visual appearance and narrative-role wording from `description`; preserve those stable
  visual facts in the appropriate base `appearance`, and preserve voice and height in `attributes`.
- Never write temporary segment conditions into `description`, `attributes`, or variants.
- Do not silently resolve a source conflict. Preserve the existing record and report the conflict.

## Validation

Before delivery, verify:

- Every reusable screenplay asset appears exactly once in the appropriate folder.
- Every screenplay-established character age/life-stage or outfit form has its own record, and no such forms remain grouped as
  variants of one character record.
- Every filename equals its top-level ID plus `.json`.
- IDs are unique across all three folders.
- Types, prefixes, and folders agree.
- Every record has `id`, `type`, `name`, `description`, `attributes`, and non-empty `variants`.
- Every record has exactly one `is_base: true` variant.
- Every variant has `id`, `status`, `is_base`, `appearance`, and `image`.
- Every variant also has `stage1_prompt`; its value is either `null` or a non-empty string written by the matching Stage 1 prompt workflow.
- JSON parses successfully as UTF-8.
- Universal voice, movement, operation, sound, scale, and layout facts are retained.
- Every individual character has a screenplay-derived age/life stage, metric height, and complete four-field voice object.
- Character descriptions contain exactly the corresponding age/life stage, voice, and height information and nothing else.
- Prop, vehicle, robot, and machine descriptions contain their complete reusable briefs, with no duplicate `dimensions`,
  `movement`, `operation`, or `sound` fields in `attributes`.
- Prop descriptions contain no owner, user, target, relationship, location, plot event, or scene-specific purpose.
- No temporary appearance condition or dependent visual phenomenon has become a registry asset or variant.

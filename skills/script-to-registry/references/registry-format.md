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
- Keep one asset when the script clearly refers to the same identity or object.
- Use variants only for reusable forms that may have separate reference images across multiple segments or episodes, such as a
  time-separated identity form, a recurring uniform, or a persistent alternate construction.
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
  "description": "Universal identity and narrative function.",
  "attributes": {},
  "variants": [
    {
      "id": "Char-Example-Base",
      "status": "Base",
      "is_base": true,
      "appearance": "Reusable canonical appearance with no segment-specific condition.",
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

## Universal Attributes

Use `attributes` only for facts that should remain consistent whenever the asset appears. Omit unsupported fields instead of
guessing.

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

Prop, vehicle, robot, or machine fields may include:

```json
{
  "dimensions": "string",
  "movement": "string",
  "operation": "string",
  "sound": "string"
}
```

Scene fields may include:

```json
{
  "layout": "string",
  "scale": "string",
  "persistent_lighting": "string",
  "ambient_sound": "string"
}
```

Movement, operation, voice, sound, dimensions, and layout belong here when they are universal. Describe actual mechanics rather
than broad labels: identify which parts move, their order, pauses, weight transfer, repeated rhythm, or stable operating behavior.

## Appearance And Image

- `description` identifies the asset and its universal function.
- `variants[].appearance` contains the stable reusable visual form, including age or life-stage information when relevant.
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
- Preserve stable IDs, approved appearance text, and image metadata.
- Add newly established universal facts without replacing stronger manually authored detail with weaker inference.
- Never write temporary segment conditions into `description`, `attributes`, or variants.
- Do not silently resolve a source conflict. Preserve the existing record and report the conflict.

## Validation

Before delivery, verify:

- Every reusable screenplay asset appears exactly once in the appropriate folder.
- Every filename equals its top-level ID plus `.json`.
- IDs are unique across all three folders.
- Types, prefixes, and folders agree.
- Every record has `id`, `type`, `name`, `description`, `attributes`, and non-empty `variants`.
- Every record has exactly one `is_base: true` variant.
- Every variant has `id`, `status`, `is_base`, `appearance`, and `image`.
- JSON parses successfully as UTF-8.
- Universal voice, movement, operation, sound, scale, and layout facts are retained.
- No temporary appearance condition or dependent visual phenomenon has become a registry asset or variant.

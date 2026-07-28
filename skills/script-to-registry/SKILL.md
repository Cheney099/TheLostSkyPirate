---
name: script-to-registry
description: >-
  Read a complete screenplay, identify its reusable characters, groups, props, vehicles, robots, machinery, and scenes, and
  create or update one schema-consistent JSON registry file per asset under asset_registry/. Use when starting an episode,
  auditing missing prompt assets, rebuilding an asset inventory, or preparing universal asset briefs before segment mapping
  and Seedance prompt generation.
---

# Script To Registry

## Route

1. Read the complete user-specified screenplay from the project `scripts/` folder before identifying assets.
2. Do not read or use storyboard files. The registry must be derived exclusively from the complete screenplay.
3. Read [references/registry-format.md](references/registry-format.md) completely.
4. Inventory the complete episode before writing any JSON. Resolve repeated names, aliases, identity-level age or wardrobe
   forms, and recurring objects into stable assets. Create separate character assets for distinct age/life-stage or outfit forms.
5. For every character asset form, infer a stable age/life stage, approximate height, and voice from the complete screenplay
   using [references/registry-format.md](references/registry-format.md). Do not use storyboard evidence.
6. Read every existing JSON under `asset_registry/characters/`, `asset_registry/props/`, and `asset_registry/scenes/` before
   creating or updating files.
7. Create or update one JSON per reusable asset form. Preserve stronger manually authored data and real image metadata.
8. Validate the complete registry against the screenplay and report created, updated, unchanged, ambiguous, and unresolved assets.

## Authority

- The screenplay determines which assets exist and their narrative identity.
- Storyboard files are outside this skill's authority and must not supply, alter, or enrich registry information.
- Registry JSON stores only reusable facts. Temporary damage, dirt, blood, active illumination, attached fire, smoke, weather,
  debris, and other segment conditions belong in the later prompt under that prompt skill's placement rules.
- Never create a standalone registry asset for a visual condition, emission, material response, or environmental consequence.
  A permanent body feature belongs to its character's canonical appearance; its temporary visibility belongs in video content.
- Character age/life stage, height, and voice are required registry facts. Infer them from the screenplay when they are not
  stated directly; do not leave them empty merely because the screenplay provides only contextual evidence.

## Output

- Characters and reusable human groups: `asset_registry/characters/<Char-id>.json`
- Physical props, vehicles, robots, and machinery: `asset_registry/props/<Prop-id>.json`
- Locations and persistent spaces: `asset_registry/scenes/<Scene-id>.json`

Write valid UTF-8 JSON with two-space indentation. Do not create auxiliary inventories, README files, or effect folders.

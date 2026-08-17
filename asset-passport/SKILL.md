---
name: asset-passport
description: |
  Build exhaustive, locked-ready passports for characters, locations, and props.
  A passport = exhaustive text descriptor + grey-background reference sheet
  (front, three-quarter, profile, back, close portrait). State variants (wet,
  blood, night) become separate tagged assets.
  Use when: "create passport", "lock this character", "build character sheet",
  "location passport", after reference boards. Required before stress-test and
  any generation.
---

# Asset Passport

Consistency is manufactured here.

A video model has no memory. If a character’s appearance is not described **exhaustively and identically** in every prompt, neighbouring shots hand him a different face, jacket, or age. Across a film this is fatal.

The passport is the memory the model does not have.

## What a passport contains

For every character, location, and key prop:

1. **Tag** — stable identifier, e.g. `@cal`, `@cal_wet`, `@kitchen_day`
2. **Exhaustive text descriptor** — never shortened later
3. **Reference sheet** — images generated (or selected) on neutral grey background:
   - Front
   - Three-quarter
   - Profile
   - Back
   - Close portrait / hero detail
4. **Version** and status in the registry

### Critical variant rule

Wet clothes are a **different passport**.  
Blood is a **different passport**.  
Night lighting on a location is often a **different passport**.

`@cal`, `@cal_wet`, and `@cal_blood` are three separate assets with three separate tags. A variant described only inline will be forgotten by the model.

## Process (one asset at a time)

### 1. Interview until the descriptor has no gaps

Ask focused questions. Do not accept vague answers.

For a **character**:
- Age range, ethnicity cues, face shape, distinctive marks
- Hair (exact style, colour, length, condition)
- Eyes, expression baseline
- Body type, posture habits
- Wardrobe: every visible garment, colour, condition, fit, specific details
- Accessories
- What must stay identical across every appearance

For a **location**:
- Architecture / geography
- Key objects and their relative positions (distances in metres when possible)
- Palette and light character (this travels into every shot in that location)
- Time-of-day variants if needed

For a **prop**:
- Exact appearance, scale, material, condition, any text or markings

Write the descriptor as a dense, ordered block that can be pasted verbatim.

### 2. Generate or collect the grey-background reference sheet

Prefer generating the sheet with a strong identity-capable image model on pure neutral grey.  
Front / 3/4 / profile / back / close.  

Once the sheet is approved, **never regenerate it**. If later motion looks wrong, fix the motion prompt, not the identity images.

### 3. File the passport

```
assets/characters/<tag>/
├── descriptor.md
├── sheet/
│   ├── front.png
│   ├── three-quarter.png
│   ├── profile.png
│   ├── back.png
│   └── close.png
└── meta.md
```

### 4. Register

Add or update the row in `docs/registry.md`. Status starts as `draft`. Only `stress-test` may move it to `locked`.

## Descriptor rules

- Never shorten later "for brevity". That is exactly where consistency dies.
- Location passports carry the scene’s palette and light character so every shot arrives pre-graded.
- The descriptor is copied **word-for-word** into every generation prompt that uses the asset.

## After all draft passports for a production block exist

Hand off to `/stress-test`. No generation is allowed while any required asset remains `draft`.

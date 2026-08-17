---
name: stress-test
description: |
  Combat-test every draft passport under real scene conditions before it is
  allowed to lock. Tests different angles, shot sizes, actual scene lighting,
  and two-shots with co-stars. Only a full pass moves status from draft to locked.
  Use when: "stress test this character", "lock the passports", "test consistency",
  after asset-passport and before any film generation.
---

# Stress Test

A passport that looks perfect alone often breaks the moment it shares a frame or meets real scene light.

This stage is cheap insurance. Tests are static images (or very short clips) run **before** any expensive video generation for the film.

## Goal

Every asset that will appear in the current production block must reach **10/10 repeatability** under combat conditions. Anything below stays `draft`. The scenes that depend on it remain closed.

## Combat matrix (minimum)

For each character passport under test:

1. **Angles & sizes** — Front, three-quarter, profile, back, low angle, high angle, wide, medium, close.
2. **Real scene lighting** — Use the lighting description from the actual locations the character will inhabit.
3. **Two-shots / group** — Standing next to every other character they share a frame with.
4. **Wardrobe & state** — If variants exist (`@cal_wet`), test those under the same matrix.

For locations: multiple camera positions, different times of day if claimed, with and without key characters.

For props: in hand, on surface, different distances, different lighting.

## Process

1. Read the registry and the breakdown for the current production block.
2. Build the test matrix for every `draft` asset that the block touches.
3. Write explicit test prompts (image model first — cheaper and faster).
4. Generate the test set.
5. Score with the user against a clear checklist (identity holds? wardrobe identical? no age/face drift?).
6. Only on a **full pass** flip the registry row to `locked`.
7. If it fails, return to `asset-passport` or move the scene to a later production block.

## Lock criteria (strict)

- 10/10 identity and wardrobe consistency across the matrix
- No contradictory details between descriptor and generated tests
- Two-shot partners also hold
- User (or director role) explicitly accepts the lock

There is no "almost locked".

## After the block is fully locked

```
All assets for scenes X–Y are locked.
Generation is now permitted for those scenes only.
Next: /shot-prompt for the first locked scene.
```

## Rules

- Never mark locked without the combat matrix.
- Never allow generation for a scene that still has draft assets.
- Keep test generations in a clearly separated folder so they are never confused with film selects.

## References

- `references/combat-matrix.md` — full recommended test grid
- `references/scoring-checklist.md`

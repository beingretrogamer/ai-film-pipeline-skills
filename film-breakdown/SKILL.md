---
name: film-breakdown
description: |
  Convert a script, treatment, or short idea into structured scene tables and
  22-field shot cards. Extracts in-frame text into a separate task list.
  Use when: "breakdown this script", "make shot cards", "turn this idea into shots",
  "scene by scene breakdown", after studio-init. Produces the cards that later
  feed shot-prompt.
---

# Film Breakdown

Before anyone writes a prompt, the script becomes shot cards.

A perfect card still describes a man that no two models will draw the same way — that problem belongs to the passport stages. This stage only creates the structured brief.

## Input

Accept any of:
- Full script
- Treatment
- One-paragraph idea
- Existing scene list

Work scene by scene. One question at a time when information is missing.

## Output artefacts

For each scene:
1. Scene table entry (in `docs/breakdown/scenes.md`)
2. One shot-card file per shot (`prompts/cards/<scene>-<shot>.md`)
3. In-frame text task list (signs, phone screens, titles) pulled out of generation

## The 22 fields (three lanes)

Every shot card must contain all 22 fields. Leave none blank; mark "n/a" only when truly inapplicable and explain why.

### Lane A — Identity (what exists)

1. **scene_id** / **shot_id**
2. **location** (tag that will match a passport)
3. **time_of_day**
4. **characters** (list with asset tags + state variants, e.g. `@cal`, `@cal_wet`)
5. **props** (tagged)
6. **description** (one clear paragraph of what is on screen)
7. **dialogue** (verbatim, or "none")
8. **running_time** (target seconds)
9. **complexity** (simple / medium / hard — affects iteration budget)

### Lane B — Direction (what it must achieve)

10. **goal** (what this shot must accomplish for the story)
11. **task** (single verb: reveal, confront, escape, land, etc.)
12. **dramaturgy** (beat function: setup / build / turn / resolve)
13. **blocking** (where bodies are in space)
14. **acting** (intention, emotion, physical behaviour)
15. **style_device** (if any: slow push, smash cut energy, etc.)

### Lane C — Camera & Edit

16. **shot_size** (EWS / WS / MWS / MS / MCU / CU / ECU)
17. **movement** (static, pan, tilt, dolly, tracking, handheld, crane…)
18. **lens** (approximate mm or FOV description — one lens only)
19. **angle** (eye, low, high, dutch, overhead…)
20. **cut_type** (how it joins previous/next)
21. **pace** (lingering / normal / urgent)
22. **transition** (cut, dissolve, match, wipe, hard cut to black…)

## Critical rules

- **One action per clip.** Never a sequence of actions inside one generation. Split if needed.
- **Any text that must appear inside the frame** (sign, phone UI, title card, newspaper) is removed from the generation brief and added to a separate task list. Video models still write text poorly; titles belong to the edit or specialized image models.
- Work interactively. Fill fields the user can answer quickly; propose sensible defaults for the rest and confirm.
- After a scene is complete, write the files immediately. Do not hold everything in chat.

## Process

1. Read or receive the source material.
2. Split into scenes. Create the scene index.
3. For each scene, list candidate shots (start coarse).
4. Expand each shot into the full 22-field card.
5. Extract every piece of in-frame text into `docs/breakdown/text-tasks.md`.
6. Confirm with user before marking the breakdown "complete".

## Shot card template

Save exactly in this form (so later skills can parse it):

```markdown
# Shot Card — <scene_id>-<shot_id>

## Identity
- scene_id:
- shot_id:
- location:
- time_of_day:
- characters:
- props:
- description:
- dialogue:
- running_time:
- complexity:

## Direction
- goal:
- task:
- dramaturgy:
- blocking:
- acting:
- style_device:

## Camera & Edit
- shot_size:
- movement:
- lens:
- angle:
- cut_type:
- pace:
- transition:
```

## After completion

Update the project status and hand off:

```
Breakdown complete.
N scenes, M shot cards written to prompts/cards/
In-frame text tasks: docs/breakdown/text-tasks.md
Next: /reference-board for style + character/location references, then /asset-passport.
```

## References

- `references/22-fields-explained.md` — deeper rationale and examples for each field
- `references/example-cards.md` — sample filled cards

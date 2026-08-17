---
name: shot-prompt
description: |
  Write generation-ready prompts using the fixed 15-block structure. Pulls locked
  passports verbatim, enforces one-line-change iteration, maintains the generation
  log, and refuses to write a prompt while any asset is still draft.
  Use when: "write the prompt for this shot", "generate this card", "iterate on
  shot X", after stress-test locks are in place. Core of the generation stage.
---

# Shot Prompt

Once the blocks are locked, the render itself becomes mechanical.

Every shot prompt uses the **same 15 blocks in the same fixed order**. No negative prompts — every prohibition is rewritten as what **is** in the frame.

## Hard gate

Before writing any generation-ready prompt:

1. Read the shot card.
2. Collect every character, location, prop, and variant tag it references.
3. Check `docs/registry.md`.
4. **If any of those assets is not `locked`, refuse.** Tell the user exactly which tags are still draft and send them back to stress-test / asset-passport.

No exceptions.

## The 15 blocks (fixed order)

1. **Character count lock** — `EXACT N CHARACTERS — NO DUPLICATES.`
2. **Character passports** — Paste every required character descriptor **verbatim**.
3. **Location passport + spatial map** — Full location descriptor + distances; 180° line.
4. **Props** — Verbatim prop passports or short locked descriptions.
5. **Time of day & light** — Shaped from the location’s own sources; carry pre-baked palette.
6. **Camera** — One lens only. Shot size, angle, movement.
7. **Action & timed beats** — Beats of 0.3–0.8s. For 30s one-shots: 0–6 / 6–14 / 14–24 / 24–30.
8. **Dialogue & performance** — Verbatim dialogue + lip-sync / acting notes.
9. **Physics & continuity** — Damage never heals mid-scene; debris stays.
10. **Style & grade** — 60:30:10 colour line + locked style paragraph from bible.
11. **Motion grammar** — Camera move paired with an event; forbid frozen figures.
12. **Reference roles** — What each attached media controls and must NOT touch.
13. **Sound / ambience notes** (if model supports native audio).
14. **Technical / duration** — Length, aspect, resolution, model flags.
15. **Positive frame statement** — What is and is not present. No negative prompt language.

## Iteration protocol

- Every new attempt changes **exactly one line** (or one clearly scoped block).
- Everything else stays word-for-word identical.
- Log the attempt in `docs/generation-log.md` before the next generation starts.
- At attempt **15**, stop. Simplify the shot (split, drop an action, change angle).

## Acceptance into selects

A finished take is accepted only by checklist: matches locked references, no major artifacts, camera as ordered, lip-sync holds, cuts cleanly with neighbours, logged.

Only accepted takes go into `selects/`. The editor never touches raw generations.

## Process for one shot

1. Load the shot card from `prompts/cards/`.
2. Verify all assets locked.
3. Assemble the 15 blocks, pasting passports verbatim.
4. Write the full prompt into `prompts/versions/<shot-id>-v01.md`.
5. Hand off to `film-generate` (or the generation backend).
6. Review → accept to selects + log, or iterate (one change) → new version + log.

## Rules

- Never shorten a passport.
- Never skip the log.
- Never generate while any asset is draft.
- Prefer one primary video model for the whole film.
- Keep the 15-block order sacred so surgical edits remain possible.

## References

- `references/15-blocks-detailed.md`
- `references/iteration-examples.md`
- `references/acceptance-checklist.md`

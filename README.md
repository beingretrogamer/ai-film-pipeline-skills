# AI Film Pipeline Skills

**Production-grade Agent Skills for consistent, long-form AI video and film generation.**

Built for Claude Code, Cursor, Codex, and any agent that supports the [Agent Skills](https://agentskills.io) open standard.

These skills implement a complete studio pipeline designed around one core truth:

> **Video models have no memory between generations.**  
> The pipeline *is* the memory.

They turn the chaotic "prompt → generate → hope" loop into a disciplined, gated production system for coherent multi-shot work on Higgsfield, fal.ai, Kling, Veo, and others.

## Why this exists

Most AI video dies on continuity. A character's face, jacket, age, or the distance between a door and a window drifts from shot to shot. Across 30–90 seconds this kills immersion faster than any other flaw.

This suite solves that by forcing:

- Locked visual bibles and written decisions
- One asset → one exhaustive passport (never shortened)
- Stress-testing before any expensive generation
- Fixed 15-block prompt structure with surgical iteration
- Hard gates: nothing generates until every asset in the scene is locked
- Full versioning and generation logs

## Skills

| Skill | Invoke | Purpose |
|-------|--------|--------|
| **ai-film-pipeline** | `/ai-film-pipeline` | Master orchestrator. Runs the full 11-stage process and enforces gates. |
| **film-setup** | `/film-setup` | Model stack, auth, project config (Higgsfield / fal / Replicate / manual). |
| **studio-init** | `/studio-init` | Scaffold production directory tree + registry templates. |
| **film-breakdown** | `/film-breakdown` | Script/treatment → scene tables + 22-field shot cards. |
| **reference-board** | `/reference-board` | Collect, caption, ban-list, and lock visual references. |
| **asset-passport** | `/asset-passport` | Build exhaustive character / location / prop passports. |
| **stress-test** | `/stress-test` | Combat-test passports under real scene conditions before locking. |
| **shot-prompt** | `/shot-prompt` | Write generation-ready 15-block prompts + manage iteration log. |
| **film-generate** | `/film-generate` | Submit to configured backend, log, move accepted takes to selects/. |

## Recommended order

```
film-setup → studio-init → film-breakdown → reference-board
→ asset-passport → stress-test → shot-prompt → film-generate
```

## Backend-agnostic by design

Pre-production never depends on a vendor. Only `film-generate` talks to a provider:

- **Higgsfield** (CLI + official skills)
- **fal.ai** (Seedance, Kling, Veo, Sora, Grok Imagine Video, …)
- **Replicate** (and similar)
- **manual** — skills write the perfect prompt + reference list; you generate in any UI

## Core production laws (never break these)

1. Generate **nothing** for the film until every required asset is locked.
2. One asset = one approved passport. Copy it **verbatim** into every prompt that uses it.
3. Edits are surgical: change **one line**, keep everything else word-for-word.
4. Everything is versioned and logged. An unlogged good shot is a shot you cannot reproduce.
5. At attempt 15, stop blaming the prompt — simplify the shot.

## Samples

Real examples that show the full pipeline applied to concrete projects.

| Sample | Type | Demonstrates |
|--------|------|--------------|
| [**Alphabet Zoo**](./samples/alphabet-zoo/) | Kids educational shorts series | Locked recurring host, letter-animal passports, 22-field shot cards, 15-block sing-along prompts, series scaling templates |

The Alphabet Zoo sample is complete enough to generate Episode A immediately and then expand to the full alphabet using the included templates.

## Install

```bash
npx skills add beingretrogamer/ai-film-pipeline-skills
```

## License

MIT

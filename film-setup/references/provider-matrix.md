# Provider & Model Matrix (2026)

Pre-production is always backend-agnostic. Only `film-generate` talks to a vendor.

## Recommended primary video models

| Model | Best backends | Max practical duration | Native audio | Notes |
|-------|---------------|------------------------|--------------|-------|
| Seedance 2.5 | Higgsfield, fal | ~30 s | Yes | High reference budget, strong one-shot. |
| Seedance 2.0 | Higgsfield, fal | ~15 s | Yes | Excellent motion + audio. |
| Kling 3 / O3 | fal, others | ~15 s | Yes (toggle) | Strong multi-shot / storyboard control. |
| Veo 3.1 | fal, Google | shorter | Yes | Highest fidelity; watch duration limits. |
| Sora 2 / Pro | fal, OpenAI | up to ~20 s | Yes | Strong narrative coherence. |
| Grok Imagine Video | fal, xAI | ~15 s | Yes | Fast, cost-effective option. |

**Rule of thumb:** Pick **one** primary video model for the entire film.

## Music / song models (fal)

Use these when you need a stronger melody or a locked song asset for a series.

| Model | Best for | Notes |
|-------|----------|-------|
| **MiniMax Music 2.6 / Music 3** | Short vocal kids songs, chants, lyric-driven tracks | Recommended default upgrade path. Style + lyrics input. |
| ElevenLabs Music | Higher polish, section control | More expensive per minute |
| Lyria 2 / 3 | Structured full songs | Strong overall quality |
| Seed Audio 1.0 | Scene + dialogue + light music | More cinematic than pure song |
| Sonilo | Licensed / commercial-safe music | Good when rights clarity matters |

### Seedance audio cost note

On Seedance 2.5, `generate_audio: true|false` does **not** change price.  
Token cost is driven only by resolution × duration × frame rate.  
Leave native audio **on** by default. Turn it off only when you already have an external track you want to force.

### Recommended music strategy for series work

1. Iterate with Seedance native audio (free, joint generation).
2. When a chant/song needs to be locked, generate it with MiniMax on fal.
3. Feed the MiniMax track as an audio reference into Seedance reference-to-video for final lip-sync and timing.

## Image models for passports / grey sheets

Need strong identity hold and clean neutral-grey background sheets.

Good options: Nano Banana family, Flux variants, GPT Image class, Seedream, Soul models.

## Switching backends later

Passports, shot cards, registry, and the 15-block prompts stay identical.  
Only `config/project.json` and the `film-generate` adapter change.

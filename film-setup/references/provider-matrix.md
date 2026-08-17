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

## Image models for passports / grey sheets

Need strong identity hold and clean neutral-grey background sheets.

Good options: Nano Banana family, Flux variants, GPT Image class, Seedream, Soul models.

## Switching backends later

Passports, shot cards, registry, and the 15-block prompts stay identical.  
Only `config/project.json` and the `film-generate` adapter change.

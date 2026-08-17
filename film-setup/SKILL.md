---
name: film-setup
description: |
  Configure generation backends, model preferences, and shared project config for the
  AI film pipeline. Supports multiple providers (Higgsfield, fal.ai, Replicate, manual).
  Establishes which video model and image models will drive production while keeping
  pre-production fully backend-agnostic.
  Use when: starting a new film project, "set up models", "configure fal", "switch to
  Kling", "which backend for consistency", or before any studio-init / breakdown work.
  Chain with: studio-init next. NOT for actual generation or asset creation.
---

# Film Setup

Establish the technical foundation so every later skill speaks the same language.
Pre-production (breakdown, passports, stress-test, prompt writing) never depends on a specific vendor.

## Goal

Produce a single `config/project.json` that every other skill can read. Generation adapters later consume this config.

## Supported backends

| Backend | Notes | Primary video models (2026) |
|---------|-------|-----------------------------|
| `higgsfield` | Official CLI + agent skills, strong agentic surface | Seedance 2.5 / 2.0, Cinema Studio, etc. |
| `fal` | Clean serverless API, excellent model catalog | Seedance 2.5, Kling 3 / O3, Veo 3.1, Sora 2, Grok Imagine Video |
| `replicate` | Simple API, many community models | Varies |
| `manual` | Skills only write prompt files; user generates in any UI | Any |

You can change backend later without touching passports or shot cards.

## Workflow

### 1. Detect existing setup

Check for:
- Existing `config/project.json`
- `higgsfield` CLI authenticated
- `FAL_KEY` (or `FAL_API_KEY`) in environment
- Previous project tree

### 2. Interview (one question at a time)

Ask only what is missing:

1. **Primary backend**  
   Recommended defaults:
   - Strong agentic / CLI workflow → `higgsfield`
   - Maximum model choice + simple API → `fal`
   - Just want the discipline + write prompts → `manual`

2. **Primary video model** for the film  
   Prefer **one model for the whole film** (one prompt grammar, one consistency behaviour).  
   Strong 2026 options:
   - Seedance 2.5 (30 s one-shot, high reference budget, native audio) — available on both Higgsfield and fal
   - Kling 3 / O3 (multi-shot storyboarding, native audio, strong motion)
   - Veo 3.1 (high fidelity + audio)
   Record the exact model / endpoint ID the chosen backend expects.

3. **Image models for reference sheets & passports**  
   Need strong identity + neutral grey background control.  
   Good options: Nano Banana family, Flux variants, GPT Image / equivalent, Seedream, Soul models.

4. **Resolution, aspect, max duration targets**

5. **Auth status**  
   - Higgsfield: `higgsfield auth login`
   - fal: `export FAL_KEY=...` (or fal client login)

### 3. Write config

Create or update:

```
config/
├── project.json          # machine-readable
├── models.md             # human notes + quirks
└── laws.md               # the five non-negotiable production laws
```

`project.json` schema (extensible):

```json
{
  "project_name": null,
  "backend": "fal",
  "video": {
    "provider": "fal",
    "model": "bytedance/seedance-2.5/text-to-video",
    "fallback_models": [],
    "default_resolution": "720p",
    "default_aspect": "16:9",
    "max_clip_seconds": 30,
    "native_audio": true
  },
  "image": {
    "character_sheet": "fal-ai/flux/dev",
    "location": null,
    "general": null
  },
  "iteration_limit": 15,
  "cli_ready": false,
  "notes": ""
}
```

For Higgsfield the `model` field should be the CLI job-set type / display name the official skills expect.

### 4. Bootstrap if needed

**Higgsfield**
```bash
curl -fsSL https://raw.githubusercontent.com/higgsfield-ai/cli/main/install.sh | sh
# or npm install -g @higgsfield/cli
higgsfield auth login
npx skills add higgsfield-ai/skills
```

**fal.ai**
```bash
pip install fal-client   # or npm equivalent
export FAL_KEY="your-key"
# Verify with a tiny test call later via film-generate
```

### 5. Confirm readiness

```
✓ Backend: fal
✓ Video model: bytedance/seedance-2.5/text-to-video (30s, native audio)
✓ Image models for passports: ...
✓ Auth: FAL_KEY present
✓ Config written to config/project.json

Next: run /studio-init with the project name.
```

## Rules

- Never assume a model ID. Prefer live discovery when possible.
- Prefer one primary video model for the entire film.
- Image models exist only to build the reference sheets that feed the video model.
- Record known quirks of the chosen video model in `models.md`.
- Changing backend later must not require rewriting passports or shot cards.

## References

- `references/provider-matrix.md` — recommended model pairings
- `references/config-schema.md` — full schema documentation

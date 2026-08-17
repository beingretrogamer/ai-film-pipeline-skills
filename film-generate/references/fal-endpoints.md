# fal.ai Endpoint Notes (Seedance-focused)

Always verify live schema with the fal playground or client before production calls.

## Common Seedance patterns

### Text-to-video
```
bytedance/seedance-2.5/text-to-video
```

Typical arguments: `prompt` (required), duration / resolution flags, optional audio toggles.

### Image-to-video / Reference-to-video
Endpoints differ in how they accept references (single `image_url` / `start_image_url` vs arrays).

**Critical for our pipeline:** When attaching passport reference sheets, state in the prompt (block 12) exactly what each reference controls and what it must **not** influence.

## Practical workflow

1. `shot-prompt` writes `prompts/versions/<shot>-vNN.md`
2. `film-generate` reads config → chooses fal endpoint
3. Collects passport sheet paths, uploads or passes URLs
4. Submits, waits or polls
5. Downloads into `generations/<shot>/<attempt>/`
6. Logs request id + params
7. User reviews → accept into `selects/` or iterate

## Auth

```bash
export FAL_KEY="..."
```

Never commit keys.

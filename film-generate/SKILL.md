---
name: film-generate
description: |
  Execute generation for a locked shot using the configured backend (Higgsfield,
  fal.ai, or manual). Reads the 15-block prompt version, attaches reference media
  according to passport rules, submits the job, logs the attempt, and places
  accepted outputs into selects/.
  Use when: "generate this shot", "run the prompt", "submit to fal", "call Seedance",
  after shot-prompt has written a version and all assets are locked.
  NOT for writing prompts or building passports.
---

# Film Generate

This is the only skill that talks to a generation provider.
Everything upstream is backend-agnostic.

## Hard gate (inherited)

Before any call:

1. Load the shot card and the chosen prompt version.
2. Verify every asset tag referenced in the prompt is `locked` in the registry.
3. If any asset is still draft → refuse and send user back to stress-test / asset-passport.

## Read config

```bash
# Expect config/project.json
backend = project.backend          # higgsfield | fal | replicate | manual
video_model = project.video.model
```

## Adapter behaviour

### Backend = `manual`

- Write or confirm the final prompt file.
- List the exact reference images that should be attached and what each controls.
- Tell the user the exact settings (duration, aspect, resolution).
- Wait for the user to drop the resulting video into `generations/`.
- Then run the normal logging + acceptance flow.

### Backend = `fal`

Typical pattern (Python / fal-client):

```python
import fal_client

handler = fal_client.submit(
    "bytedance/seedance-2.5/text-to-video",   # or image-to-video / reference-to-video
    arguments={
        "prompt": open("prompts/versions/S01-01-v03.md").read(),
        # attach image / video / audio references according to passport sheet paths
    },
)
result = handler.get()
video_url = result["video"]["url"]
```

- Download the result into `generations/<shot-id>/<attempt>/`.
- Record request id, model, and parameters in the generation log.
- Different fal endpoints have different reference parameter names. Read the live model schema or `references/fal-endpoints.md` before calling.

### Backend = `higgsfield`

Prefer the official Higgsfield skills / CLI:

```bash
higgsfield generate create <model> --prompt "..." --image ... --wait
```

Or invoke the installed `higgsfield-generate` skill with the prepared prompt and reference paths.
Follow the same logging rules.

### Backend = `replicate` (or others)

Map the configured model ID to the provider’s API and follow the same download + log + accept pattern.

## After generation

1. Log the attempt (shot, attempt #, what changed, model, path, verdict).
2. Review with user.
3. On accept → copy/move to `selects/` with a clean final name.
4. On reject → prepare one-line change for next version via shot-prompt.

## Rules

- Never generate while any referenced asset is draft.
- Always log before the next attempt.
- selects/ is the only folder the edit is allowed to see.

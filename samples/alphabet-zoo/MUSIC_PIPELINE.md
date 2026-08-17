# Music Pipeline — Alphabet Zoo

## Core rule

**Native Seedance audio stays on by default.**  
It costs the same as silent video and is often good enough while you lock characters and framing.

## Decision tree

```
Are you still iterating visuals / passports?
  └─ Yes → generate_audio: true (native)
  └─ No, this letter song must be locked for the series
        └─ Generate with MiniMax Music on fal
        └─ Then run Seedance reference-to-video with that audio as reference
```

## Why this order

| Stage | Audio source | Reason |
|-------|--------------|--------|
| Exploration | Seedance native | Zero extra cost, joint lip-sync, fast |
| Locked letter song | MiniMax → Seedance audio ref | Better melody + consistent chant across the series |
| Final polish | Same MiniMax track | One canonical song per letter |

## MiniMax quick payload shape (fal)

```json
{
  "prompt": "Bright children’s nursery rhyme, major key, simple catchy melody, clear kids choir, soft clapping, playful educational, 115 BPM",
  "lyrics_prompt": "[Chorus]\nA is for Avery!\nAvery the Alligator!\nA-A-Avery, come and play!\nA is for Avery today!"
}
```

(Exact field names may vary slightly by MiniMax version — check the current fal model card.)

## What never to do

- Turn `generate_audio` off hoping to save money (it does not).
- Mix different songs for the same letter across episodes.
- Regenerate the song every time you tweak a visual — lock the audio asset once.

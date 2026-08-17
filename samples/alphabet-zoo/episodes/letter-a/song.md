# Song — Letter A

## Short chant (recommended for 20–28s shorts)

**Structure:**
```
A is for Avery!
Avery the Alligator!
A-A-Avery, come and play!
A is for Avery today!
```

**Musical direction:**
- Major key, bright and simple
- 110–120 BPM
- Kids-choir or clear child-like lead vocal
- Light claps or soft percussion on the beat
- Very short — designed to loop cleanly inside one generation

---

## Music strategy (recommended order)

### 1. Default — Seedance 2.5 native audio (always on)

Leave `generate_audio: true`.

Why:
- Costs the same as silent video
- Joint generation often produces surprisingly good lip-sync + simple chant
- Zero extra steps while iterating visuals

Only turn it off when you already have a locked external track you want to force.

### 2. Upgrade path — MiniMax Music on fal (when you want better melody)

When the native chant is not catchy enough, generate a proper short song on fal and feed it back as an audio reference.

**Recommended model:** `fal-ai/minimax-music/v2.6` (or `minimax/music-3` when available)

**Style prompt example:**
```
Bright children’s nursery rhyme, major key, simple catchy melody, clear kids choir, soft clapping rhythm, playful and educational, 110-120 BPM, short 20-25 second loopable chant
```

**Lyrics prompt example:**
```
[Chorus]
A is for Avery!
Avery the Alligator!
A-A-Avery, come and play!
A is for Avery today!
```

### 3. Hybrid (production quality)

1. Generate the MiniMax track
2. Run Seedance 2.5 **reference-to-video**
3. Pass the MiniMax audio URL as an audio reference
4. Keep character passports locked
5. Seedance matches timing and lip-sync to the external track

This is the highest-quality path for a published series.

---

## Fallback / alternative music models on fal

| Model | When to use |
|-------|-------------|
| MiniMax Music 2.6 / 3 | Default upgrade for short vocal kids songs |
| ElevenLabs Music | Higher polish, more expensive |
| Lyria | Strong structured songs |
| Seed Audio 1.0 | Scene + dialogue + light music in one pass |

---

## Rule for this series

- **Iterate visuals** → keep native Seedance audio on
- **Lock a letter song** → generate with MiniMax, then use as audio reference
- Never pay extra hoping silent video is cheaper — it is not

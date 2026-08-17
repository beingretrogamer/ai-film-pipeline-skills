# Sample: Alphabet Zoo

A complete, production-ready example of a kids educational shorts series built with the AI Film Pipeline skills.

**One host. Twenty-six letters. Infinite replay value.**

This sample shows how the discipline layer turns a simple idea ("cute animals teach the alphabet") into a consistent, scalable series that video models can actually deliver without identity drift.

## Why this sample exists

Kids content lives or dies on recognition. The same character must look identical across dozens of episodes. The same world, the same lighting language, the same chant structure.

Most AI kids videos fail because every generation is treated as a one-off prompt. This sample treats it as a **studio**.

## What is locked in this sample

- Host character: **Zippi the Zookeeper** (full passport)
- First letter animal: **Avery the Alligator** (full passport)
- World rules + ban list
- Complete 22-field shot cards for Episode A
- Ready-to-run 15-block prompt for Seedance 2.5
- Song direction for the letter chant
- Template system so Letters B–Z become mechanical

## How to use this sample

1. Copy the entire `alphabet-zoo` folder into your own project workspace (or start a new studio with `/studio-init` and mirror this structure).
2. Run `/stress-test` on the two existing passports if you want to verify them on your model stack.
3. Generate Episode A with the provided 15-block prompt.
4. Use the templates in `templates/` to create the next letter animals one by one.
5. Once a letter animal is locked, generating its episode is mostly a search-and-replace on the 15-block skeleton.

## Recommended model stack for this sample

- **Video**: Seedance 2.5 (text-to-video or reference-to-video) — strong native audio + 30s capability
- **Image (passports)**: Any strong identity model that can hold soft rounded characters on grey (Flux variants, Seedream, GPT Image, etc.)
- **Music**: Suno (or equivalent) for the short letter chants

See `config/project.json` for the exact settings used in this example.

## Folder map

```
alphabet-zoo/
├── README.md
├── SERIES_BIBLE.md
├── config/
│   └── project.json
├── assets/
│   ├── passports/
│   │   ├── zippi-the-zookeeper.md
│   │   └── avery-the-alligator.md
│   └── reference-board/
│       ├── style-lock.md
│       └── ban-list.md
├── episodes/
│   └── letter-a/
│       ├── shot-cards.md
│       ├── 15-block-prompt.md
│       └── song.md
└── templates/
    ├── new-letter-passport.md
    ├── new-letter-shot-cards.md
    └── new-letter-15-block.md
```

## Core lesson

The expensive part is not the generation.
The expensive part is the **unlocked character** that forces five regenerations.

Lock once. Generate many times.

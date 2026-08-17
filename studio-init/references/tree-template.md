# Full Annotated Tree

```
<project-name>/
├── assets/
│   ├── characters/
│   │   └── <tag>/
│   │       ├── descriptor.md
│   │       ├── sheet/
│   │       ├── stress-tests/
│   │       └── meta.md
│   ├── locations/
│   ├── props/
│   └── variants/
├── prompts/
│   ├── cards/
│   └── versions/
├── generations/
├── selects/
├── edit/
├── color/
├── sound/
├── master/
├── docs/
│   ├── breakdown/
│   ├── bible/
│   ├── registry.md
│   ├── generation-log.md
│   └── FOLDER_LAWS.md
└── config/
    ├── project.json
    ├── models.md
    └── laws.md
```

## Folder laws (recap)

1. Never rename a reference or passport file. New version = new file.
2. `generations/` is private.
3. `selects/` is the only folder the edit is allowed to see.
4. Every generation is logged before the next attempt.
5. Locked passports are copied verbatim.

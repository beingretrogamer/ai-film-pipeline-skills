---
name: studio-init
description: |
  Scaffold the complete production directory tree, living registry, generation log,
  and folder laws for an AI film project. Creates the file system that is the
  studio itself.
  Use when: "start a new film project", "initialize studio", "create project folders",
  after film-setup, or when the user gives a project name and wants the pipeline structure.
  Chain after film-setup. Before film-breakdown.
---

# Studio Init

There is no production office. There is a directory.

This skill creates the entire working tree and seeds the documents every later skill depends on.

## Required input

- Project name (one short slug or title). Ask if missing.

## Workflow

### 1. Create the tree

```bash
PROJECT="<project-name>"
mkdir -p "$PROJECT"/{assets/{characters,locations,props,variants},prompts/{cards,versions},generations,selects,edit,color,sound,master,docs/{breakdown,bible,logs},config}
```

Exact layout:

```
<project>/
├── assets/
│   ├── characters/          # one folder per character passport
│   ├── locations/
│   ├── props/
│   └── variants/            # wet, blood, night, aged, etc. treated as separate assets
├── prompts/
│   ├── cards/               # the 22-field shot cards (source of truth)
│   └── versions/            # every prompt attempt, never overwrite
├── generations/             # raw model outputs (prompt engineer only)
├── selects/                 # ONLY accepted takes. Edit sees nothing else.
├── edit/
├── color/
├── sound/
├── master/
├── docs/
│   ├── breakdown/           # scene tables + shot card index
│   ├── bible/               # visual bible, style decisions, ban lists
│   ├── registry.md          # living asset registry (status, version, scenes)
│   └── generation-log.md    # every attempt, what changed, verdict
└── config/                  # from film-setup (copy or symlink)
```

### 2. Seed the registry

Create `docs/registry.md` with this header and empty table:

```markdown
# Asset Registry — <project>

Status values: draft | testing | locked | deprecated

| Tag | Type | Version | Descriptor file | Ref sheet | Scenes | Status | Notes |
|-----|------|---------|-----------------|-----------|--------|--------|-------|
|     |      |         |                 |           |        |        |       |
```

### 3. Seed generation log

```markdown
# Generation Log — <project>

Format per entry:
- Shot ID
- Attempt #
- Timestamp
- What changed (exactly one line or “initial”)
- Model + seed/params if available
- Verdict: keep / reject / simplify
- Path to output
- Notes

---
```

### 4. Write the three folder laws

Create `docs/FOLDER_LAWS.md`:

```markdown
# Folder Laws (inherited by every agent)

1. A reference or passport file is **never renamed**. A new version is a new file.
2. `generations/` is private to the prompt engineer. The editor never looks here.
3. `selects/` contains only accepted takes. The edit is allowed to see nothing else.
4. Every generation must be logged before the next attempt begins.
5. Locked passports are copied **verbatim**. Shortening is forbidden.
```

### 5. Copy or link config

If `config/` already exists from `film-setup`, ensure it is inside the project or clearly referenced.

### 6. Confirm

Print the tree and the next required action:

```
Studio ready: <project>
Registry: docs/registry.md (empty)
Next: /film-breakdown with the script, treatment, or one-paragraph idea.
```

## Rules

- Never start generation or asset work before this tree exists.
- Project name becomes the root folder. Keep it filesystem-safe.
- All later skills assume this exact structure. Do not invent alternate layouts without updating every skill.

## References

- `references/tree-template.md` — full annotated tree
- `references/registry-schema.md` — recommended registry fields and status machine

---
name: reference-board
description: |
  Collect, caption, and lock visual references for characters, locations, props,
  lighting, color, optics, camera movement, texture, and cutting tempo. Builds
  the written visual bible and ban list.
  Use when: "gather references", "build the visual bible", "reference board",
  "lock style", after breakdown and before or alongside asset-passport.
---

# Reference Board

A reference is a **specification**, not inspiration.

"A tired father in a worn jacket" produces a different man in every model and every head. An actual image of him settles the question.

Rule direction is one-way only: **find the existing image first, then describe it**. Never invent a description and then hunt for proof.

## Working counts (from real productions)

| Element | Target images |
|---------|---------------|
| Lead character | 10–20 |
| Supporting character | 6–12 |
| Key location | 8–15 |
| Prop | 3–5 |
| Light / color / optics / texture / tempo boards | 5–12 each |

These are working minimums, not aspirations.

## Boards to create

1. **Character boards** (one per major character)
2. **Location boards**
3. **Prop boards**
4. **Style boards**: light, color palette, optics/lens character, camera movement language, texture/grain, cutting tempo, sound palette (optional)
5. **Ban list** ("like this — not allowed")

## Process (one board at a time)

1. **Collect**  
   User supplies images or points to sources. Prefer real cinema stills, photographic references, or previously approved generations. Extract from films that already carry the desired feeling when possible.

2. **Caption every image**  
   Force a caption that names **exactly what is taken from it**:
   - "Front three-quarter, soft key from camera left, tired eyes, navy work jacket with frayed cuff"
   - Not "cool shot" or "I like this".

3. **Ban list**  
   Any image the user marks "never this" goes into the ban list with a short reason. Ban lists save more generations than positive references.

4. **Written decision**  
   Close every board with one of:
   - **Approved**
   - **Revise** (list exact changes)
   - **Rejected**

   A style that was only approved verbally means the director and the prompt engineer are holding two different films. They discover it a month in.

5. **Lock record**  
   Write the decision onto the board file itself and into `docs/bible/`.

## Style extraction shortcut

For light, color, optics, grain, and tempo:
- Feed stills from reference films to a vision model.
- Ask it to name lens character, light direction, palette, grain structure.
- Lock the output as one tight paragraph that will be pasted into every relevant prompt.

## Output location

```
docs/bible/
├── characters/<name>-board.md
├── locations/<name>-board.md
├── props/
├── style/
│   ├── light.md
│   ├── color.md
│   ├── optics.md
│   ├── movement.md
│   ├── texture.md
│   └── tempo.md
└── ban-list.md
```

Each board file must end with:

```markdown
## Decision
Status: Approved | Revise | Rejected
Date:
Notes:
```

## Rules

- No image without a caption is allowed to stay on a board.
- Verbal approval is not a lock. Written decision only.
- Ban list is first-class, not an afterthought.
- When extracting from cinema, prefer stills that already solve the lighting and wardrobe problems you face.

## After boards are locked

Proceed to `/asset-passport` for every character, location, and prop that appears in the current production block. The passports will reference these boards.

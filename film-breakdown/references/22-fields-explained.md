# Why 22 fields?

The columns map almost one-to-one onto the later 15-block prompt structure. Filling them forces decisions that would otherwise be improvised (and therefore inconsistent) at generation time.

## Identity lane
Locks *what* exists so the passport stage knows exactly which assets to build and the prompt stage knows exactly what to paste.

## Direction lane
Locks *why* the shot exists. Prevents beautiful but useless generations.

## Camera & Edit lane
Locks the optical and editorial intention so the model is not guessing lens or movement.

## One action rule
A single generation that tries to perform a sequence of actions almost always fails or drifts. Split the sequence into multiple shot cards.

## In-frame text extraction
Current video models still handle readable text poorly. Titles, UI, signage, and newspapers are better handled in edit or with specialized image models.

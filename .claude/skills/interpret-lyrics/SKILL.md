---
name: interpret-lyrics
description: Interpret the meaning of a poem or song lyrics, covering themes, imagery, literary devices, form, and context. Use when the user shares lyrical or poetic text, or names a poem or song, and asks what it means or wants an analysis.
argument-hint: <the poem/lyrics text, or a title and author>
---

# Interpret Lyrics

Material: $ARGUMENTS

<!-- TODO: Edit this whole file to shape how interpretations are done. -->

## 1. Get the text

- If the user pasted the text, work from that.
- If they only named a work, work from what you know about it and quote at most a few short lines. Ask them to paste the full text if a close reading needs it.

## 2. Identify the style

Decide the form or style (e.g. haiku, ballad, sea shanty, a particular artist's style).
If a matching style skill exists in `.claude/skills/style-*/`, read it for the conventions that shape the meaning.

## 3. Analyze

<!-- TODO: Add, remove, or reorder lenses. -->
- **Literal content:** what happens and who is speaking
- **Themes:** the main ideas and emotional core
- **Imagery and devices:** metaphor, symbolism, repetition, sound, and what each one does
- **Form:** how structure, meter, rhyme, or refrain support the meaning
- **Context:** the author or artist, the era, the genre, and its traditions, where relevant
- **Ambiguity:** where several readings are valid, give them instead of forcing one

## 4. Present

Output format:
<!-- TODO: Adjust the output format and depth to taste. -->
```
## Interpretation: <Title>

**In short:** <a 2–3 sentence summary of the meaning>

### Themes
### Imagery & Devices
### Form & Style
### Other Readings
```

## 5. Offer to save

After presenting, offer to save the interpretation. Save it if the user says yes, or if they asked for it to be saved in the original request.

**Location:** `interpretations/<YYYY-MM-DD>-<slug>.md`, relative to the project root, where `<slug>` is the work's title in kebab-case (e.g. `the-world-is-too-much-with-us`). Never overwrite an existing file. Add `-v2`, `-v3`, and so on if the name is taken.

Put this frontmatter above the interpretation:
```
---
title: <Title of the work>
author: <author or artist, if known>
style: <form or style identified in step 2>
date: <YYYY-MM-DD>
---
```

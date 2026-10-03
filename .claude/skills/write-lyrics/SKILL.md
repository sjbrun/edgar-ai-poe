---
name: write-lyrics
description: Write original song lyrics or poetry in a requested style or form (e.g. haiku, sea shanty, sonnet, "in the style of Tom Petty"). Use when the user asks to write, compose, or draft a poem, song, verse, or lyrics.
argument-hint: <style> <topic or brief>
---

# Write Lyrics

Request: $ARGUMENTS

<!-- TODO: Edit this whole file to shape how lyrics get written. -->

## 1. Pin down the request

Identify, asking the user only if something essential is missing:
- **Style or form:** e.g. haiku, sea shanty, limerick, or an artist's style
- **Topic or story:** what the piece is about
- **Length and structure:** number of verses, whether there's a chorus or bridge
- **Tone:** e.g. playful, melancholy, defiant

<!-- TODO: Decide on defaults when the user doesn't specify (length, tone, etc.). -->

## 2. Load style knowledge

Look for a matching style skill in `.claude/skills/style-*/` (for example `style-haiku` for a haiku).
If one exists, read its `SKILL.md` and any example files before writing, and follow its rules.
If none exists, rely on general knowledge of the style and tell the user there's no style skill for it yet.

## 3. Write

- Follow the form's hard constraints exactly (syllable counts, rhyme scheme, meter, refrains).
- Capture an artist's style through themes, imagery, vocabulary, and song structure. Never copy or closely paraphrase their actual lyrics.
- <!-- TODO: Add your own craft rules (imagery, avoiding clichés, rhyme preferences...). -->

## 4. Check

Before presenting, check the draft against the style's constraints and fix anything that breaks them.

## 5. Save and present

Save every piece to a Markdown file, then show the same content in chat.

**Location:** `poems/<style>/<YYYY-MM-DD>-<slug>.md`, relative to the project root
- `<style>`: the style skill's folder name without the `style-` prefix (e.g. `sea-shanty`, `villanelle`). If no style skill matched, use a short kebab-case name for the style (e.g. `tom-petty`, `free-form`)
- `<slug>`: the title in kebab-case (e.g. `the-lost-cat`)
- Never overwrite an existing file. For a revision of an earlier piece, or a name clash, add `-v2`, `-v3`, and so on

File format:
<!-- TODO: Adjust the output format to taste. -->
```
---
title: <Title>
style: <style, plus variant if any, e.g. "sonnet (Petrarchan)" or "sea-shanty (halyard)">
date: <YYYY-MM-DD>
brief: "<the user's original request>"
---

# <Title>

<lyrics, using the style skill's notation: section labels like [Verse 1] / [Chorus] for songs, CREW: for call-and-response lines>

---
**Notes:** <one or two lines on the choices made: form, rhyme scheme, nods to the style>
```

In chat, show the piece (title, lyrics, notes) without the frontmatter, followed by the saved file path.

## 6. Offer to copy to Google Drive

When a Google Drive connector is available, end by offering to copy the piece to the user's Drive (for example, a new subfolder under `Lyrics`). Only copy if the user says yes. Never write into the Drive folders that hold the user's existing songs unless they ask for that specifically.

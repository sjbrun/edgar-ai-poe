# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A skills-only agentic project for creating and interpreting song lyrics and poetry. There is no build or test step. All behavior lives in Claude Code skills under `.claude/skills/`.

## How the skills fit together

- **`write-lyrics`** and **`interpret-lyrics`** are the action skills. Users can invoke them directly (`/write-lyrics sea shanty about a lost cat`), and Claude can also pick them automatically.
- **`style-*`** are knowledge skills, one per form, genre, or artist style. They set `user-invocable: false`, so they only supply reference material. Both action skills look in `.claude/skills/style-*/` for a style that matches the request and read its `SKILL.md` and `examples.md` before working.
- **`templates/style-skill/`** is the starting point for a new style skill. Copy it to `.claude/skills/style-<name>/` and make the frontmatter `name` match the folder name. `style-haiku` is a filled-in example.

## Output

- `write-lyrics` saves every piece to `poems/<style>/<YYYY-MM-DD>-<slug>.md` with YAML frontmatter (title, style, date, brief). It saves revisions as `-v2`, `-v3`, and so on instead of overwriting. Copying to Google Drive happens only when the user agrees.
- `interpret-lyrics` saves to `interpretations/<YYYY-MM-DD>-<slug>.md` only when asked.

## Conventions

- Style examples must be public-domain works or originals. For artist styles, describe traits instead of reproducing copyrighted lyrics.
- `<!-- TODO -->` comments in skill files mark places the owner still plans to customize.

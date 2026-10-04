# edgar-ai-poe

A set of [Claude Code](https://claude.com/claude-code) skills for writing and interpreting song lyrics and poetry.

The repo contains only skills. There is no app to build and nothing to install: open the folder in Claude Code and ask for a poem.

## Quick start

```sh
cd edgar-ai-poe
claude
```

Then either call a skill directly:

```
/write-lyrics sea shanty about a lost cat
/interpret-lyrics "Because I could not stop for Death" by Emily Dickinson
```

or just ask in plain language ("write me a villanelle about insomnia", "what does this poem mean?"). Claude picks the right skill on its own.

## Skills

### Action skills

| Skill | What it does |
| --- | --- |
| `write-lyrics` | Writes an original poem or song in the requested style, checks it against the form's rules, and saves it to `poems/`. |
| `interpret-lyrics` | Analyzes a poem or song: themes, imagery, literary devices, form, and context. Saves to `interpretations/` only when you ask. |

### Style skills

Style skills hold reference knowledge, not actions. They aren't invoked directly. Both action skills look for a matching `style-*` skill and read its rules and annotated examples before they start.

| Style | Covers |
| --- | --- |
| `style-acrostic` | Acrostics and their variants |
| `style-ballad` | Traditional folk and literary ballads |
| `style-blank-verse` | Unrhymed iambic pentameter, verse drama, dramatic monologue |
| `style-elegy` | Elegies, laments, memorial poems |
| `style-free-verse` | Open-form poetry with no fixed meter or rhyme |
| `style-haiku` | Haiku |
| `style-limerick` | Limericks and short comic verse |
| `style-ode` | Pindaric, Horatian, and irregular odes |
| `style-sea-shanty` | Sea shanties, forebitters, call-and-response work songs |
| `style-sonnet` | Shakespearean, Petrarchan, and Spenserian sonnets |
| `style-villanelle` | Villanelles |

If you ask for a style with no matching skill (for example "in the style of Tom Petty"), Claude falls back on general knowledge and tells you there's no style skill for it yet.

## Output

Every piece from `write-lyrics` is saved as Markdown:

```
poems/<style>/<YYYY-MM-DD>-<slug>.md
```

Each file starts with YAML frontmatter:

```yaml
---
title: The Fellow from Crewe
style: limerick
date: 2026-10-04
brief: "limerick, about a man who goes to town to buy something but realizes he left his wallet at home"
---
```

Files are never overwritten. Revisions are saved as `-v2`, `-v3`, and so on. If a Google Drive connector is available, Claude offers to copy the piece to Drive and copies it only if you say yes.

Interpretations are saved to `interpretations/<YYYY-MM-DD>-<slug>.md`, but only on request.

## Adding a style

1. Copy `templates/style-skill/` to `.claude/skills/style-<name>/`, for example `style-tom-petty`.
2. In `SKILL.md`, set the frontmatter `name` to match the folder name and replace every `REPLACE-ME`.
3. Fill in the sections: hard rules, conventions, themes and imagery, tone and vocabulary.
4. Add annotated examples to `examples.md`.

`style-haiku` is a complete example to follow.

## Conventions

- **Copyright:** Examples must be public-domain works or originals. For artist styles, describe the artist's traits (themes, imagery, vocabulary, song structure) and don't reproduce their lyrics.
- **TODOs:** `<!-- TODO -->` comments in skill files mark places still waiting to be customized.

## Layout

```
.claude/skills/
  write-lyrics/        action skill
  interpret-lyrics/    action skill
  style-*/             one folder per form or style (SKILL.md + examples.md)
templates/style-skill/ starting point for new style skills
poems/                 saved pieces, grouped by style
CLAUDE.md              guidance for Claude Code in this repo
```

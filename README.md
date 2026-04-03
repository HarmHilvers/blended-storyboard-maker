# blended-storyboard-maker

Create an interactive course storyboard from user-provided teaching materials.

## What it does

This skill reads course materials and turns them into a structured storyboard, usually as a single interactive HTML file.

It is intended for requests such as:

- creating a blended learning storyboard
- turning course documents into a week-by-week storyboard
- building an HTML storyboard with rows such as face-to-face, practice, and online
- deriving a course planning artifact from files like week content, assignments, rubrics, schedules, and readings

## Installation

This repository is structured as a Codex skill: a folder with a `SKILL.md` file and optional supporting files. Codex discovers skills either from your global Codex home directory or from a project-local skills folder.

### Option 1: install globally

```bash
git clone https://github.com/harmhilvers/blended-storyboard-maker.git ~/.codex/skills/blended-storyboard-maker
```

### Option 2: install in a project

```bash
mkdir -p .agents/skills
git clone https://github.com/harmhilvers/blended-storyboard-maker.git .agents/skills/blended-storyboard-maker
```

After installation, restart Codex or start a new session so the skill can be discovered.

## Input

This skill works from user-provided course materials, for example:

- week introductions or weekly planning
- assignments and expected student work
- literature, books, readings, or study guides
- rubrics, assessment moments, or checkpoints
- schedules, course overviews, revision notes, or spreadsheets

The skill first checks whether the source set is sufficient before building the storyboard.

## Output

The default output is a single self-contained HTML storyboard with:

- columns by week
- rows by learning mode
- concise activity cards
- optional detail panels or filters

The visible output always follows the user's language. If the output is HTML, the root `lang` attribute should also follow the user's language.

## Design principles

- Derive content from the supplied materials, not from prior examples.
- Be conservative in interpretation.
- Do not invent missing course content.
- Keep row definitions sharp, especially between face-to-face, practice, and online.
- Only use `Practice` for authentic work in or with the professional field.
- Keep placeholders for missing activities short.

## Workflow

1. Inspect the supplied files.
2. Check whether the material set is sufficient.
3. Derive the storyboard model from the user's requested structure.
4. Build concise weekly content cards.
5. Generate the final artifact, usually a single HTML file.
6. Check traceability, language, and row consistency.

## Repository structure

- `SKILL.md` - skill instructions and storyboard workflow
- `agents/openai.yaml` - UI metadata for Codex

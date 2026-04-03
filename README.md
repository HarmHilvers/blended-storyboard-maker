# blended-storyboard-maker

Create an interactive course storyboard from user-provided teaching materials.

## What it does

This skill reads course materials and turns them into a structured storyboard, usually as a single interactive HTML file.

It is intended for requests such as:

- creating a blended learning storyboard
- turning course documents into a week-by-week storyboard
- building an HTML storyboard with rows such as face-to-face, practice, and online
- deriving a course planning artifact from files like week content, assignments, rubrics, schedules, and readings

## Runtime Model

This repository is organized as an agent-agnostic core specification with thin runtime adapters.

- `SKILL.md` is the canonical workflow and quality contract.
- `agents/openai.yaml` provides Codex/OpenAI UI metadata.
- `agents/claude.md` provides a Claude-ready adapter prompt.
- `agents/generic.md` provides a fallback adapter for other agent frameworks.
- `core/compatibility-contract.md` defines the cross-agent behavioral contract.
- `evals/acceptance.md` defines acceptance criteria for regression checks.

## Installation

This repository can be used in multiple agent environments. The core workflow lives in `SKILL.md`, while each runtime can consume its own adapter file.

### Codex / OpenAI

Codex discovers skills either from your global Codex home directory or from a project-local skills folder.

#### Option 1: install globally

```bash
git clone https://github.com/harmhilvers/blended-storyboard-maker.git ~/.codex/skills/blended-storyboard-maker
```

#### Option 2: install in a project

```bash
mkdir -p .agents/skills
git clone https://github.com/harmhilvers/blended-storyboard-maker.git .agents/skills/blended-storyboard-maker
```

After installation, restart Codex or start a new session so the skill can be discovered.

### Claude

Clone the repository anywhere convenient, then use the prompt in `agents/claude.md` together with the workflow in `SKILL.md`.

```bash
git clone https://github.com/harmhilvers/blended-storyboard-maker.git
```

Then copy the trigger prompt from `agents/claude.md` into your Claude project, system prompt, or reusable instruction layer.

### Other agents

Use `SKILL.md` as the canonical workflow and `agents/generic.md` as the adapter prompt for platforms without a dedicated integration format.

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
- `agents/openai.yaml` - UI metadata for Codex/OpenAI
- `agents/claude.md` - Claude adapter prompt and contract
- `agents/generic.md` - generic adapter prompt for other agents
- `core/compatibility-contract.md` - cross-agent behavioral contract
- `evals/acceptance.md` - acceptance criteria for regression checks

## Usage by runtime

### Codex / OpenAI

Use the repository as a normal Codex skill. The OpenAI adapter sets the display name and starter prompt, while `SKILL.md` remains the workflow source of truth.

### Claude

Use the adapter text in `agents/claude.md` and keep `SKILL.md` available as the canonical workflow reference. The Claude adapter is intentionally thin so behavior stays aligned with the core specification.

### Generic

For other runtimes, use `agents/generic.md` as the copy-paste adapter prompt and validate the outcome against `evals/acceptance.md`.

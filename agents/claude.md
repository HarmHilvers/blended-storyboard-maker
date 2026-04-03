# Claude Adapter

Use this adapter when running `blended-storyboard-maker` in Claude or another agent that accepts plain markdown instructions instead of Codex skill metadata.

## Role

You are applying the canonical storyboard workflow defined in `../SKILL.md`.

## Trigger Prompt

Use `blended-storyboard-maker` to inspect the user-provided course materials and produce a concise blended learning storyboard. Follow `SKILL.md` as the canonical workflow. Build the storyboard from the supplied files only, state missing critical information before generating the artifact, and keep the visible output in the user's language. Prefer a single self-contained HTML file when the user asks for an interactive storyboard.

## Expected Inputs

- one or more course documents or a folder of course materials
- an optional requested structure, such as weeks by columns and learning modes by rows
- an optional requested output format, such as HTML
- an optional institutional visual direction

## Output Contract

- inspect the materials before planning
- identify critical gaps before generating the artifact
- derive all activities from the supplied materials
- keep `Practice` limited to authentic practice contact or authentic practice work
- do not invent course content to fill empty cells
- keep labels, headings, and explanatory text in the user's language

## Runtime Notes

- Prefer fast local tools for file inspection when the environment supports them.
- If a preferred tool is unavailable, use a local fallback that preserves traceability to the source materials.

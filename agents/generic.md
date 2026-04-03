# Generic Agent Adapter

Use this adapter for agent frameworks that do not support Codex `SKILL.md` metadata or a dedicated Claude-style adapter.

## Canonical Reference

`../SKILL.md` is the source of truth for workflow, output rules, heuristics, and minimum acceptance criteria.

## Copy-Paste Prompt

Create a blended learning storyboard from the user-provided course materials. Inspect the supplied files before planning, verify whether the source set is sufficient, derive the storyboard conservatively from the materials, and avoid inventing missing course content. Follow the row and column structure requested by the user; if no structure is specified, default to a week-based storyboard when the materials support that. Keep the visible output in the user's language. If the user asks for an interactive storyboard, prefer a single self-contained HTML file with concise cards, rows for learning modes, columns for weeks, and optional detail panels or filters.

## Required Behaviors

- inspect the provided files before synthesizing output
- state missing critical information before building the storyboard
- keep claims traceable to the source materials
- keep the distinction between face-to-face, practice, and online sharp
- only use `Practice` when the source explicitly supports authentic practice activity
- keep placeholders for empty cells short

## Portability Notes

- Prefer local, inspectable tooling over remote services.
- Favor deterministic extraction steps for `.docx`, `.odt`, `.pdf`, and `.xlsx`.
- If the platform has no filesystem tools, ask for pasted source excerpts rather than guessing.

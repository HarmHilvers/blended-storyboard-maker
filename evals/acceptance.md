# Acceptance Criteria

This repository is intended to behave consistently across OpenAI/Codex, Claude, and other agent runtimes.

## Required Input Handling

- The agent inspects or enumerates the supplied files before planning the storyboard.
- The agent identifies whether the provided material set is sufficient for the requested storyboard.
- If critical sources are missing, the agent states what is missing before generating the artifact.

## Required Storyboard Behavior

- The storyboard uses the user's requested row and column model when provided.
- If no structure is requested and the material set is organized by week, the storyboard defaults to week-based columns.
- The agent derives activity cards from the supplied materials and does not invent unsupported activities.
- `Practice` is used only when the source explicitly indicates authentic practice contact or authentic practice work.
- Empty cells use short placeholders rather than explanatory paragraphs.

## Required Output Quality

- The visible output language matches the user's language.
- If the output is HTML, the root `lang` attribute matches the user's language.
- Major claims in the storyboard remain traceable to the supplied materials.
- The final artifact is concise, scannable, and ready for user consumption.

## Regression Questions

- Does the agent refuse to silently fill major gaps with invented course content?
- Does the agent call out insufficient materials before generating a polished artifact?
- Does the agent keep the row distinction between face-to-face, practice, and online consistent?
- Does the agent preserve the requested output structure across runtimes?

# Compatibility Contract

This document defines the cross-agent contract for `blended-storyboard-maker`.

## Canonical Sources

- `../SKILL.md` defines the workflow, output rules, heuristics, and minimum acceptance criteria.
- Files in `../agents/` define runtime-specific adapter text and trigger prompts.

## Stable Behavioral Contract

Every adapter must preserve these behaviors:

- inspect the provided course materials before planning the storyboard
- evaluate whether the source set is sufficient
- report critical missing inputs before generating a polished artifact
- derive the storyboard from the supplied materials rather than prior examples
- keep visible output in the user's language
- avoid inventing unsupported course content
- keep learning-mode rows semantically distinct

## Input Contract

The minimum useful source set for a week-based storyboard usually includes:

- week structure or sequencing
- weekly content or week introductions
- assignments or expected student work
- literature or study materials when they are part of the design
- assessment moments or checkpoints

If one or more critical elements are missing, adapters must state that explicitly.

## Output Contract

The default output is a concise storyboard artifact, usually a self-contained HTML file, with:

- columns by week or another user-requested sequence
- rows by learning mode or another user-requested model
- concise activity cards
- optional detail panels or filters when HTML is requested

## Portability Contract

- Adapters may choose different local tools depending on the runtime environment.
- Tool changes must not weaken traceability, language fidelity, or the no-invention rule.
- If a preferred tool is unavailable, adapters should choose the nearest reliable local fallback.

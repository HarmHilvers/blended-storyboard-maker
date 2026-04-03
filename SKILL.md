---
name: blended-storyboard-maker
description: Create interactive course storyboards from user-provided teaching materials such as `.docx`, `.odt`, `.pdf`, `.xlsx`, and folders of course documents. Use when an agent is asked to read source files and turn them into a week-by-week blended learning storyboard, usually in a single HTML file, with rows such as face-to-face, practice, and online or other user-specified learning modes.
---

# Blended Storyboard Maker

Create a storyboard that translates user-provided course materials into a clear teaching design artifact. Do not treat the skill as a source of course content. Read the supplied files first, infer the course flow conservatively, and present the result in the language requested by the user.

## Agent Compatibility

- Treat this file as the canonical workflow specification for every agent adapter in this repository.
- Keep agent-specific UI text, trigger prompts, and runtime conventions out of this file. Put those in `agents/`.
- Preserve the same behavioral contract across agents:
  - inspect the provided materials before planning
  - state missing critical information before generating the artifact
  - derive rows, columns, and activities from the supplied materials
  - avoid invented course content
  - keep visible output in the user's language
- If an agent platform cannot execute a preferred local tool, use the closest available fallback while preserving the same output rules and quality bar.

## Output Rules

- Derive the storyboard content from the user's materials, not from examples or prior storyboard work.
- Follow the user's language for visible output, labels, headings, and explanatory text.
- Keep the skill file itself in English.
- If the output is HTML, set the root `lang` attribute to the user's language.
- If the user asks for a specific structure, row model, or column model, follow that exactly.
- If the sources do not support a planned activity, do not invent one. State that it is not scheduled, and keep that wording brief.

## Workflow

### 1. Inspect the materials

- List the files in the provided folder before planning the storyboard.
- Read all relevant source files that define the course flow: weekly descriptions, assignments, rubric documents, revision notes, schedules, and similar materials.
- Prefer fast local inspection tools such as `rg --files`, `textutil`, `sed`, and related shell tools.
- Extract text conservatively. For `.odt` and `.docx`, prefer `textutil` when available, otherwise use `pandoc`, unzip-and-read XML, or another local text extraction route.
- For `.xlsx`, inspect sheets and schedule tables explicitly, and convert relevant tabs to plain text or CSV when needed before deriving the storyboard. Prefer `python` plus `openpyxl` or a comparable spreadsheet reader when direct CSV export is not available.
- For `.pdf`, prefer a local text extraction tool such as `pdftotext` when available, or another reliable extractor that keeps page content attributable.

### 2. Check whether the materials are sufficient

- Verify that the source set contains enough information to build the requested storyboard.
- Look for at least these elements when the storyboard is week-based:
  - week structure or sequencing
  - weekly content or week introductions
  - assignments or expected student work
  - literature, books, readings, or other study materials when they are part of the course design
  - assessment moments or checkpoints
- Use other useful materials when available, such as rubrics, revision notes, planning documents, or course overviews.
- If key information is missing, say what is missing before building the artifact.
- Do not silently fill major gaps with invented course content.

### 3. Derive the storyboard model

- Use the user's requested rows and columns as the primary frame.
- Default to columns by week when the materials are organized week by week.
- Treat each row as a distinct learning mode. Do not duplicate the same activity across rows unless the source clearly supports that interpretation.
- Keep the distinction between rows sharp:
	- Face-to-face: guided learning activities in physical co-presence with a lecturer, peers, or assessors, such as classroom sessions, seminars, workshops, discussions, tutorials, tests, presentations, and on-site assessment moments. Core question: Does the main activity take place in physical co-presence with direct interaction and guidance?
	- Practice: learning activities involving explicit authentic practice contact or authentic practice work, such as business visits, placements, internships, live client projects, consultancy assignments, professional simulations, and other real-world practice tasks. Core question: Is the activity primarily centered on direct engagement with professional practice?
	- Online: digital learning activities, usually carried out independently or asynchronously, such as drafting, reading, literature review, desk research, revision, asynchronous preparation, online collaboration, discussion-board participation, and submission work. Core question: Does the activity primarily take place online, outside a physical teaching session or practice setting?
- Only place an item in `Practice` when the source materials explicitly indicate authentic practice contact or authentic practice work.
- If the user wants a fixed `Practice` row and no such activity is scheduled in a given week, use a short placeholder such as `No practice activity scheduled this week.`

### 4. Build the content layer

- Summarize each week into concise, high-signal activity cards.
- Preserve the logic from source to storyboard:
  - weekly theme
  - assignment progression
  - introduction or framing text when available
  - formative checkpoints
  - summative assessment
  - rubric linkage if useful
- Do not over-explain missing items. Keep placeholders short.
- If the user asks for a visual artifact rather than a prose summary, prefer compact card text over long paragraphs.

### 5. Build the artifact

- Prefer a single self-contained HTML file when the user asks for an interactive storyboard.
- Make the HTML easy to scan:
  - a fixed grid or matrix
  - rows for learning modes
  - columns for weeks
  - clickable cards or a detail panel for deeper information
  - optional filters for assignment parts, checkpoints, or assessment
- Keep the interface visually consistent and concise.
- If the user references an existing institutional style, adapt colors and typography to that visual direction without copying the site mechanically.

### 6. Check consistency

- Check that the storyboard content is traceable to the supplied materials.
- Check that the source set was actually sufficient for the claims made in the storyboard.
- Check that the storyboard language matches the user's language.
- Check that every visible claim can be traced back to the source materials.
- Check that the HTML title, labels, and `lang` attribute match the requested language and artifact type.

## Working Heuristics

- Be conservative in interpretation.
- Prefer explicit source evidence over educational guesswork.
- Compress text until the storyboard is easy to scan.
- Use short placeholders for empty cells instead of explanatory paragraphs.
- Keep the final artifact user-ready, not exploratory.

## Minimum Acceptance Criteria

- The agent lists or inspects the supplied files before synthesizing the storyboard.
- The agent explicitly identifies missing critical inputs when the material set is insufficient.
- The storyboard structure follows the user's requested row and column model, or a clearly stated default.
- `Practice` is only used when the source materials support authentic practice contact or authentic practice work.
- The final artifact contains only claims that can be traced back to the supplied materials.
- The visible output language matches the user's language.

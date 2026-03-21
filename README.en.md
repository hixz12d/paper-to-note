# Paper-to-Note

> **Not another chat-with-PDF tool.**  
> `paper-to-note` is an evidence-backed skill for turning experimental research papers into `Obsidian`-ready `Markdown` notes.

English (current) | [简体中文](README.md)

## What is this?

`paper-to-note` is a `Claude Code skill` built for experimental research papers. It converts a paper PDF into a structured `Markdown` note that is easy to review, verify, and store in your knowledge base.

Instead of only producing a generic summary, it focuses on the parts that matter during real paper reading:

- what each `Figure` is doing in the paper’s argument
- what each experiment actually did and which parameters matter
- how to trace important claims back to the original text

## Who is it for?

- People reading experimental papers in chemistry, materials science, biology, and related fields
- People organizing papers in `Obsidian` or another `Markdown`-based knowledge base
- Readers who care about which experiments support which conclusions
- Anyone who wants more than a vague paper summary

## Core capabilities

- **`Figure` argument-path analysis**  
  It does not just list `captions`. It reconstructs the story told through the figures: the role of each figure, the conclusion it supports, and how one figure leads to the next.

- **Experiment-centered parameter extraction**  
  Parameters stay attached to the experiment they belong to. Each experiment is described with its purpose, method summary, parameter table, and source quote.

- **Original-text quotes for critical conditions**  
  High-risk experimental conditions are followed by English source excerpts so they can be checked quickly.

- **Interactive mode**  
  An optional guided discussion helps the reader consolidate understanding. The discussion is then written into the `My Understandings` section.

- **`Obsidian`-ready output**  
  The final output is a clean `Markdown` note that can be dropped directly into an `Obsidian` vault.

## What do you get?

A generated note typically looks like this:

```text
# Journal--Year--Topic
├── Research overview
├── Figure argument path
│   ├── Overall logic
│   ├── Figure 1-N (role / content / supported conclusion / link to next step)
│   └── Logic chain
├── Experiments and parameters
│   ├── Experiment 1-N (purpose / method summary / parameter table)
│   └── Source quotes
└── My Understandings (interactive mode only)
```

See a real example here: [`examples/sample-output.md`](examples/sample-output.md)

## Quick start

### 1. Install

Copy the whole `paper-to-note` project directory into your `Claude Code` `skills` directory, and keep the folder name as `paper-to-note`.

If you run the command from the parent directory of this project:

#### macOS / Linux

```bash
cp -r paper-to-note ~/.claude/skills/paper-to-note
```

#### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -LiteralPath .\paper-to-note -Destination "$env:USERPROFILE\.claude\skills\paper-to-note"
```

### 2. Use it

#### Slash command

```text
/paper-to-note D:/papers/example.pdf
/paper-to-note D:/papers/example.pdf --interactive
/paper-to-note D:/papers/example.pdf --output D:/vault/notes/
```

#### Natural language

```text
Use paper-to-note to read D:/papers/example.pdf in interactive mode and write the output to D:/vault/notes/
```

### 3. Output location

- By default, the note is written to the same directory as the PDF
- If `--output` is provided, the note is written to that directory
- File name format: `{journal-abbr}--{year}--{topic-summary}.md`
- If a file with the same name already exists, a numeric suffix is added automatically instead of overwriting it

## Two modes

| Mode | What it does |
|------|--------------|
| **Default** | Reads the PDF, completes the analysis, and writes a full note directly |
| **Interactive** `--interactive` | Adds a guided discussion before final note generation and records your understanding, corrections, and open questions in `My Understandings` |

## How it works

The workflow is roughly:

```text
PDF input
  → Stage 1: Structure parsing and source-text extraction
  → Stage 2: Figure argument-path analysis
  → Stage 3: Experiment-centered parameter extraction
  → [Interactive mode] Guided discussion
  → Stage 4: Note assembly and quality control
  → Write .md file
```

## Project structure

```text
paper-to-note/
├── SKILL.md                    # skill entry and execution rules
├── prompts/
│   ├── parse-and-extract.md    # Stage 1: structure parsing and evidence extraction
│   ├── figure-logic.md         # Stage 2: figure argument-path analysis
│   ├── parameter-audit.md      # Stage 3: experiment and parameter extraction
│   └── note-assembly.md        # Stage 4: final note assembly
├── templates/
│   └── note-template.md        # final note template
└── examples/
    └── sample-output.md        # output example
```

## Design principles

1. **The paper text is the source of truth**  
   Critical parameters should be backed by original excerpts for quick verification.

2. **Conversation is not evidence**  
   `AI` discussion helps organize understanding, but it is not treated as factual support.

3. **Parameters must stay attached to experiments**  
   Each parameter belongs under a specific experiment, with purpose, method, and context preserved.

4. **Readable, mostly single-language output**  
   The generated note is written in Chinese by default, while necessary technical terms such as compound names and method abbreviations stay in English.

5. **Evidence first, summary second**  
   The workflow extracts supporting text before generating condensed notes.

## Best-fit use cases

- Experimental papers in chemistry, materials science, biology, and related fields
- Papers where `Figures`, `Methods`, and experimental parameters carry the main evidence
- A workflow where the input paper is in English and the output note is in Chinese

## Current limitations

- Not primarily designed for review papers, theoretical papers, or purely computational papers
- Non-English papers are not the target in the current version
- Requires text-based PDFs rather than scanned PDFs
- Does not handle a separate `Supplementary Information` PDF in v1
- Coverage may be incomplete for papers longer than 40 pages

If a paper appears to be non-experimental, the skill asks for confirmation before continuing.

## License

MIT

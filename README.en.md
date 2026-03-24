# Paper-to-Note

![Claude Code Skill](https://img.shields.io/badge/Claude-Code%20Skill-blue)
![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Focus: Experimental + DL Papers](https://img.shields.io/badge/focus-experimental%20%2B%20DL%20papers-purple)

> Turn paper PDFs into `Markdown` notes that are easy to verify, reuse, and keep.  
> The workflow now routes the paper type first, then uses the right track to expose `Figure` logic, experiment / training details, and source evidence behind the paper.

English (current) | [简体中文](README.md)

## 1-Minute Quick Start

1. Copy `paper-to-note` into your `Claude Code` `skills` directory
2. Run `/paper-to-note D:/papers/example.pdf` inside `Claude Code`
3. The skill routes the paper automatically and generates an `Obsidian`-ready `Markdown` note

If you already know the paper type, you can override routing manually:

```text
/paper-to-note D:/papers/example.pdf --type experimental
/paper-to-note D:/papers/example.pdf --type dl
```

For exact commands, continue to the full Quick Start section below.

## At a glance

| Best for | What you get |
|------|------|
| Readers of experimental papers in chemistry, materials science, biology, and related fields | `Obsidian`-ready experimental-paper notes |
| Readers of deep learning papers in CV, NLP, multimodal, speech, and related areas | `Obsidian`-ready DL-paper notes |
| Readers who want to see how the paper’s conclusions are built through `Figures` | `Figure` argument-path analysis |
| Readers who want to verify critical conditions, training settings, or benchmark numbers | Structured parameter / method tables + source quotes |
| Readers who want to think while reading | Optional guided discussion + `My Understandings` |

### How this differs from a generic “PDF summary”

- It does not stop at a short summary; it routes the paper into the right analysis track first
- It does not only describe what a figure contains; it reconstructs the argument path behind it
- Experimental papers are organized by experiment, while DL papers are organized by model / training / benchmark / ablation
- It does not only say what the conclusion is; it keeps source text available for quick checking
- The output is not a one-off answer, but a note you can continue to edit and keep

### Output preview

```text
# Journal-or-Venue--Year--Topic
├── Research overview
├── Figure argument path
│   ├── Overall logic
│   ├── Figure 1-N (role / content / supported conclusion / link to next step)
│   └── Logic chain
├── [Experimental track] Experiments and parameters
│   ├── Experiment 1-N (purpose / method summary / parameter table)
│   └── Source quotes
├── [DL track] Model architecture and training
│   ├── Overall architecture / key modules / training config / datasets
│   └── Benchmark and ablation
└── My Understandings (interactive mode only)
```

## What is this?

`paper-to-note` is a `Claude Code skill` that converts research paper PDFs into structured `Markdown` notes that are easy to review, verify, and store in a knowledge base.

Instead of only producing a generic summary, it focuses on the parts that matter during real paper reading:

- what each `Figure` is doing in the paper’s argument
- what each experiment or model component actually did and which settings matter
- how to trace important claims back to the original text
- which analysis framework best matches the current paper

## Who is it for?

- People reading experimental papers in chemistry, materials science, biology, and related fields
- People reading deep learning papers in CV, NLP, speech, multimodal, and related areas
- People organizing papers in `Obsidian` or another `Markdown`-based knowledge base
- Readers who care about which experiments, figures, or benchmark tables support which conclusions
- Anyone who wants more than a vague paper summary

## Core capabilities

- **Paper-type routing (v2)**  
  The workflow first decides whether the paper is `experimental`, `deep-learning`, `review`, or `theoretical`, then picks the matching prompt track. For `review` / `theoretical`, it asks for confirmation before continuing with the nearest available track.

- **`Figure` argument-path analysis**  
  It does not just list `captions`. It reconstructs the story told through the figures: the role of each figure, the conclusion it supports, and how one figure leads to the next.

- **Dual-track output for experimental + DL papers**  
  - Experimental track: experiment-centered parameters and source quotes  
  - DL track: model architecture, training configuration, datasets, benchmark results, and ablation studies

- **Original-text quotes for critical conditions**  
  High-risk experimental conditions, training settings, and important results are followed by English source excerpts so they can be checked quickly.

- **Interactive mode**  
  An optional guided discussion helps the reader consolidate understanding. The discussion is then written into the `My Understandings` section.

- **`Obsidian`-ready output**  
  The final output is a clean `Markdown` note that can be dropped directly into an `Obsidian` vault.

## Detailed note structure

The note is routed first, then assembled with the appropriate structure. See a real example here: [`examples/sample-output.md`](examples/sample-output.md)  
The current sample file in the repo is an **experimental-paper** example.

```text
PDF input
  → Stage 0: Paper-type routing
  → experimental track
  │   → Stage 1: Structure parsing and evidence extraction
  │   → Stage 2: Figure argument-path analysis
  │   → Stage 3: Experiment-centered parameter extraction
  │   → Stage 4: Note assembly
  └→ deep-learning track
      → Stage 1: Structure parsing and evidence extraction
      → Stage 2: Figure argument-path analysis
      → Stage 3: Model / training / benchmark / ablation analysis
      → Stage 4: Note assembly
```

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
/paper-to-note D:/papers/example.pdf --type experimental
/paper-to-note D:/papers/example.pdf --type dl
```

#### Natural language

```text
Use paper-to-note to read D:/papers/example.pdf in interactive mode and write the output to D:/vault/notes/
Use paper-to-note to read D:/papers/cvpr-paper.pdf and force the DL track
```

### 3. Output location

- By default, the note is written to the same directory as the PDF
- If `--output` is provided, the note is written to that directory
- File name format: `{journal-or-venue-abbr}--{year}--{topic-summary}.md`
- If a file with the same name already exists, a numeric suffix is added automatically instead of overwriting it

## Two modes

| Mode | What it does |
|------|--------------|
| **Default** | Reads the PDF, routes it automatically, completes the analysis, and writes a full note directly |
| **Interactive** `--interactive` | Adds a guided discussion before final note generation and records your understanding, corrections, and open questions in `My Understandings` |

## How it works

The workflow is roughly:

```text
PDF input
  → Stage 0: Paper-type routing
  → Stage 1: Structure parsing and source-text extraction
  → Stage 2: Figure argument-path analysis
  → Stage 3: Track-specific extraction
      experimental → experiments and parameters
      deep-learning → model architecture and training + benchmark and ablation
  → [Interactive mode] Guided discussion
  → Stage 4: Note assembly and quality control
  → Write .md file
```

If the routing result is `review` or `theoretical`, the skill asks whether to continue with the closest available track or stop.

## Project structure

```text
paper-to-note/
├── SKILL.md                         # skill entry and execution rules
├── prompts/
│   ├── router.md                    # Stage 0: paper-type routing
│   ├── experimental/
│   │   ├── parse-and-extract.md     # Stage 1: structure parsing and evidence extraction
│   │   ├── figure-logic.md          # Stage 2: figure argument-path analysis
│   │   ├── parameter-audit.md       # Stage 3: experiment and parameter extraction
│   │   └── note-assembly.md         # Stage 4: final note assembly
│   └── dl/
│       ├── parse-and-extract.md     # Stage 1: DL structure parsing and evidence extraction
│       ├── figure-logic.md          # Stage 2: DL figure argument-path analysis
│       ├── method-analysis.md       # Stage 3: model / training / benchmark / ablation analysis
│       └── note-assembly.md         # Stage 4: DL note assembly
├── templates/
│   ├── note-template.md             # experimental note template
│   └── dl-note-template.md          # DL note template
└── examples/
    └── sample-output.md             # output example
```

## Design principles

1. **The paper text is the source of truth**  
   Critical experimental parameters, training settings, and benchmark results should be backed by original excerpts for quick verification.

2. **Conversation is not evidence**  
   `AI` discussion helps organize understanding, but it is not treated as factual support.

3. **Parameters and hyperparameters must stay attached to context**  
   Experimental parameters belong under experiments; DL hyperparameters belong under training, inference, or a specific module.

4. **Readable, mostly single-language output**  
   The generated note is written in Chinese by default, while necessary technical terms such as model names, dataset names, and metric abbreviations stay in English.

5. **Route first, summarize second**  
   The workflow tries to choose the right paper-reading framework before generating the final note.

6. **Evidence first, summary second**  
   The workflow extracts supporting text before generating condensed notes.

## Best-fit use cases

- Experimental papers in chemistry, materials science, biology, and related fields
- Deep learning papers in CV, NLP, speech, multimodal, and related areas
- Papers where `Figures`, `Methods`, training settings, and benchmark tables carry the main evidence
- A workflow where the input paper is in English and the output note is in Chinese

## Advanced

> **Optional preprocessing:** MinerU (`pip install magic-pdf[full]`) can pre-convert PDFs into Markdown and save 50-70% of input tokens, but Figure image content will be lost. It is best for papers longer than 30 pages or for batch processing.

## Current limitations

- v2 supports `experimental + DL`, but `review` / `theoretical` still do not have dedicated tracks
- Non-English papers are not the target in the current version
- Requires text-based PDFs rather than scanned PDFs
- Does not handle a separate `Supplementary Information` PDF yet
- Coverage may be incomplete for papers longer than 40 pages
- When routing confidence is `medium` or `low`, the skill asks for confirmation before continuing

## License

MIT

# Paper-to-Note

> **Not another chat-with-PDF tool.**
> An evidence-backed paper-to-note skill for experimental research.

## What is this?

A **Claude Code Skill** that converts experimental research papers (PDF) into Obsidian-ready Markdown notes.

### Core Features

- **Figure 论证路径分析** — 不只列 caption，梳理作者用 Figure 讲的完整故事：每个图的作用、支撑结论、图与图之间的逻辑链
- **以实验为单位的参数提取** — 参数挂在对应实验下，每个实验有目的、方法、参数表，不脱离上下文
- **高风险参数原文摘录** — 关键实验条件附原文英文摘录，方便快速核查
- **交互模式** — 可选的 AI 引导讨论，帮你梳理理解，讨论内容沉淀为 "My Understandings" 区块

## Quick Start

### Install

Copy the `paper-to-note/` directory to your Claude Code skills folder:

```bash
# macOS / Linux
cp -r paper-to-note/ ~/.claude/skills/paper-to-note/

# Windows (PowerShell)
Copy-Item -Recurse paper-to-note/ "$env:USERPROFILE\.claude\skills\paper-to-note\"
```

### Usage

**Slash command:**
```
/paper-to-note D:/papers/example.pdf
/paper-to-note D:/papers/example.pdf --interactive
/paper-to-note D:/papers/example.pdf --output D:/vault/notes/
```

**Natural language:**
```
用 paper-to-note 帮我读一下 D:/papers/example.pdf，交互模式，输出到 D:/vault/notes/
```

### Modes

| Mode | What it does |
|------|-------------|
| **Default** | Reads PDF → generates complete Markdown note → writes to file |
| **Interactive** (`--interactive`) | Adds a guided discussion phase. Your understanding, corrections, and questions are captured in a "My Understandings" section |

## Output Example

See [`examples/sample-output.md`](examples/sample-output.md) for a real-world example.

### Note Structure

```
# 期刊--年份--主题
├── 研究概述
├── Figure 论证路径
│   ├── 整体思路
│   ├── Figure 1-N（作用/内容/结论/与下文关系）
│   └── 论证逻辑链
├── 实验与参数
│   ├── 实验 1-N（目的/方法/参数表）
│   └── 原文参考摘录
└── My Understandings（仅交互模式）
```

## How It Works

```
PDF Input
  → Stage 1: 结构解析 + 关键原文片段提取
  → Stage 2: Figure 论证路径分析（核心价值）
  → Stage 3: 以实验为单位的参数提取
  → [Interactive] AI 引导讨论
  → Stage 4: 笔记组装 + 质量控制
  → Write .md file
```

## Scope & Limitations

**Best for:**
- Chemistry, materials science, biology experimental papers
- Papers where Figures, Methods, and experimental parameters are central
- English-language papers (output in Chinese with English terminology preserved)

**Not designed for:**
- Review papers / meta-analyses
- Theoretical / computational papers
- Non-English papers (v1)
- Scanned PDFs (requires text-based PDF)
- Supplementary Information (separate PDF)
- Papers > 40 pages (partial coverage)

## Design Principles

1. **原文是事实来源** — 关键实验参数附原文摘录，可快速核查
2. **对话不是证据** — AI 讨论帮助组织思路，不作为事实依据
3. **参数不脱离实验** — 每个参数都挂在对应实验下，有目的、有方法、有上下文
4. **干净可读** — 正文全中文，仅化合物名和仪器缩写保留英文，不做中英夹杂
5. **先证据后总结** — 先定位原文片段，再生成总结

## License

MIT

# Paper-to-Note

> 这不是另一个“聊天式读 PDF”工具。  
> 这是一个面向实验型论文的、基于证据的 `paper-to-note` skill，可将 PDF 整理成适合 `Obsidian` 的 `Markdown` 笔记。

简体中文（当前） | [英文版](README.en.md)

## 这是什么

`paper-to-note` 是一个 `Claude Code skill`，专门把实验型科研论文的 PDF 转成结构清晰、便于回查、适合沉淀到知识库的 `Markdown` 笔记。

它不只是“帮你总结一下论文”，而是更关注这些真正影响阅读质量的问题：

- 作者到底想用每个 `Figure` 说明什么
- 每个实验分别做了什么，关键参数是什么
- 重要结论能不能快速回到原文核查

## 它适合谁

- 经常读化学、材料、生物等实验型论文的人
- 想把论文整理进 `Obsidian` 或其他 `Markdown` 知识库的人
- 关心“结论由哪组实验支撑”的人
- 不想只拿到一段空泛摘要的人

## 核心能力

- **`Figure` 论证路径分析**  
  不只列 `caption`，而是梳理作者用 `Figure` 讲的完整故事：每个图的作用、支撑结论，以及图与图之间的推进关系。

- **以实验为单位的参数提取**  
  参数不会被拆散成零碎清单，而是挂在对应实验下面。每个实验都有目的、方法概述、参数表和原文参考。

- **关键条件原文摘录**  
  对高风险实验条件附英文原文摘录，方便你快速回查，不必在论文里来回翻找。

- **交互模式**  
  可选的引导式讨论流程，帮助你边读边梳理理解。讨论内容会沉淀到 `My Understandings` 区块。

- **可直接入库的输出格式**  
  最终输出是适合 `Obsidian` 使用的 `Markdown` 文件，便于继续整理、链接和检索。

## 你会得到什么

生成的笔记通常包含以下结构：

```text
# 期刊--年份--主题
├── 研究概述
├── Figure 论证路径
│   ├── 整体思路
│   ├── Figure 1-N（作用 / 内容 / 支撑结论 / 与下文关系）
│   └── 论证逻辑链
├── 实验与参数
│   ├── 实验 1-N（目的 / 方法概述 / 参数表）
│   └── 原文参考摘录
└── My Understandings（仅交互模式）
```

可参考真实示例：[`examples/sample-output.md`](examples/sample-output.md)

## 快速开始

### 1. 安装

把整个 `paper-to-note` 项目目录复制到 `Claude Code` 的 `skills` 目录中，并保持目录名为 `paper-to-note`。

如果你在项目的上一级目录执行命令，可以这样安装：

#### macOS / Linux

```bash
cp -r paper-to-note ~/.claude/skills/paper-to-note
```

#### Windows PowerShell

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse -LiteralPath .\paper-to-note -Destination "$env:USERPROFILE\.claude\skills\paper-to-note"
```

### 2. 使用

#### 斜杠命令

```text
/paper-to-note D:/papers/example.pdf
/paper-to-note D:/papers/example.pdf --interactive
/paper-to-note D:/papers/example.pdf --output D:/vault/notes/
```

#### 自然语言

```text
用 paper-to-note 帮我读一下 D:/papers/example.pdf，开启交互模式，输出到 D:/vault/notes/
```

### 3. 输出位置

- 默认输出到 PDF 所在目录
- 如果使用 `--output`，则输出到你指定的目录
- 文件名格式为：`{期刊缩写}--{年份}--{主要内容概括}.md`
- 如遇同名文件，会自动追加序号，不覆盖已有文件

## 两种使用模式

| 模式 | 说明 |
|------|------|
| **普通模式** | 读取 PDF，完成分析，直接生成完整笔记并写入文件 |
| **交互模式** `--interactive` | 在生成笔记前增加引导式讨论，记录你的理解、纠正点和未解决问题，并写入 `My Understandings` |

## 它是怎么工作的

整个流程大致如下：

```text
PDF 输入
  → 阶段 1：结构解析与关键原文片段提取
  → 阶段 2：Figure 论证路径分析
  → 阶段 3：以实验为单位的参数提取
  → [交互模式] 引导式讨论
  → 阶段 4：笔记组装与质量检查
  → 写入 .md 文件
```

## 项目结构

```text
paper-to-note/
├── SKILL.md                    # skill 入口与执行规则
├── prompts/
│   ├── parse-and-extract.md    # 阶段 1：结构解析与证据提取
│   ├── figure-logic.md         # 阶段 2：Figure 论证路径分析
│   ├── parameter-audit.md      # 阶段 3：实验与参数提取
│   └── note-assembly.md        # 阶段 4：笔记组装
├── templates/
│   └── note-template.md        # 最终笔记模板
└── examples/
    └── sample-output.md        # 输出示例
```

## 设计原则

1. **原文才是事实来源**  
   关键实验参数附原文摘录，方便快速核查。

2. **对话不是证据**  
   `AI` 讨论用于帮助理解和整理思路，不作为事实依据。

3. **参数不能脱离实验**  
   每个参数都必须挂在具体实验下面，保留目的、方法和上下文。

4. **正文尽量保持单一语言**  
   正文默认用中文撰写，仅在必要时保留化合物名、方法缩写等专业名词。

5. **先证据，后总结**  
   先定位原文片段，再做概括和组织，尽量减少空泛转述。

## 更适合的场景

- 化学、材料、生物等实验型论文
- `Figure`、`Methods`、实验参数是论文核心证据的场景
- 英文论文输入，中文笔记输出的工作流

## 当前边界

- 不以综述、理论、纯计算类论文为主要目标
- 暂不适配非英文论文
- 需要可读取文本的 PDF，不适合扫描版 PDF
- 暂不处理独立的 `Supplementary Information` PDF
- 论文超过 40 页时，覆盖可能不完整

如果识别到论文可能不是实验型论文，skill 会先提示你确认是否继续。

## 许可

MIT

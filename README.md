# Paper-to-Note

![Claude Code Skill](https://img.shields.io/badge/Claude-Code%20Skill-blue)
![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Focus: Experimental + DL Papers](https://img.shields.io/badge/focus-experimental%20%2B%20DL%20papers-purple)

> 把论文 PDF 变成可回查、可复用、可沉淀的 `Markdown` 笔记。  
> 先做论文类型路由，再进入对应轨道，帮你看清 `Figure` 论证链、实验 / 训练信息和原文证据。

简体中文（当前） | [英文版](README.en.md)

## 1 分钟上手

1. 把 `paper-to-note` 复制到 `Claude Code` 的 `skills` 目录
2. 在 `Claude Code` 中运行：`/paper-to-note D:/papers/example.pdf`
3. skill 会先判断论文类型，再生成一份适合 `Obsidian` 的 `Markdown` 笔记

如果你已经明确知道论文类型，也可以手动指定：

```text
/paper-to-note D:/papers/example.pdf --type experimental
/paper-to-note D:/papers/example.pdf --type dl
```

需要具体命令的话，继续看下方的“快速开始”。

## 封面速览

| 适合谁 | 你会得到什么 |
|------|------|
| 读化学、材料、生物等实验型论文的人 | 适合 `Obsidian` 的实验型 `Markdown` 笔记 |
| 读 CV / NLP / 多模态等深度学习论文的人 | 适合 `Obsidian` 的 DL 论文 `Markdown` 笔记 |
| 想快速看懂作者如何用 `Figure` 推进结论的人 | `Figure` 论证路径分析 |
| 想回查关键实验条件、训练配置或 benchmark 的人 | 结构化参数 / 方法表 + 原文摘录 |
| 想边读边整理理解的人 | 可选交互讨论 + `My Understandings` |

### 它和普通“读 PDF 总结”有什么不同

- 不只给一段摘要，而是先判断论文类型，再走对应分析轨道
- 不只描述图里有什么，而是拆开作者的论证路径
- 实验型论文按实验组织参数，DL 论文按模型 / 训练 / benchmark / ablation 组织信息
- 不只说“结论是什么”，还尽量保留可以快速核查的原文依据
- 输出不是一次性回答，而是一份适合继续积累的笔记文件

### 输出示意

```text
# 期刊或会议--年份--主题
├── 研究概述
├── Figure 论证路径
│   ├── 整体思路
│   ├── Figure 1-N（作用 / 内容 / 支撑结论 / 与下文关系）
│   └── 论证逻辑链
├── [实验型轨道] 实验与参数
│   ├── 实验 1-N（目的 / 方法概述 / 参数表）
│   └── 原文参考摘录
├── [DL 轨道] 模型架构与训练
│   ├── 总体架构 / 关键模块 / 训练配置 / 数据集
│   └── Benchmark 与 Ablation
└── My Understandings（仅交互模式）
```

## 这是什么

`paper-to-note` 是一个 `Claude Code skill`，把科研论文 PDF 转成结构清晰、便于回查、适合沉淀到知识库的 `Markdown` 笔记。

它不只是“帮你总结一下论文”，而是更关注这些真正影响阅读质量的问题：

- 作者到底想用每个 `Figure` 说明什么
- 实验或模型方法分别做了什么，关键参数 / 训练配置是什么
- 重要结论能不能快速回到原文核查
- 这篇论文到底该用哪套阅读框架来拆

## 它适合谁

- 经常读化学、材料、生物等实验型论文的人
- 经常读 CV、NLP、语音、多模态等深度学习论文的人
- 想把论文整理进 `Obsidian` 或其他 `Markdown` 知识库的人
- 关心“结论由哪组实验或哪张 benchmark 表支撑”的人
- 不想只拿到一段空泛摘要的人

## 核心能力

- **论文类型路由（v2）**  
  先判断论文更像 `experimental`、`deep-learning`、`review` 还是 `theoretical`，再进入对应 prompt 轨道。对于 `review` / `theoretical`，会先提示你确认是否继续或改走近似轨道。

- **`Figure` 论证路径分析**  
  不只列 `caption`，而是梳理作者用 `Figure` 讲的完整故事：每个图的作用、支撑结论，以及图与图之间的推进关系。

- **实验型 / DL 双轨输出**  
  - 实验型轨道：以实验为单位整理参数、条件和原文摘录  
  - DL 轨道：整理模型架构、训练配置、数据集、benchmark 和 ablation

- **关键条件原文摘录**  
  对高风险实验条件、训练设置和关键结果附英文原文摘录，方便你快速回查，不必在论文里来回翻找。

- **交互模式**  
  可选的引导式讨论流程，帮助你边读边梳理理解。讨论内容会沉淀到 `My Understandings` 区块。

- **可直接入库的输出格式**  
  最终输出是适合 `Obsidian` 使用的 `Markdown` 文件，便于继续整理、链接和检索。

## 详细输出结构

生成的笔记会先经过路由，再输出对应结构。可参考真实示例：[`examples/sample-output.md`](examples/sample-output.md)  
当前仓库中的示例文件是**实验型论文**输出示例。

```text
PDF 输入
  → 阶段 0：论文类型路由
  → experimental 轨道
  │   → 阶段 1：结构解析与证据提取
  │   → 阶段 2：Figure 论证路径分析
  │   → 阶段 3：实验与参数提取
  │   → 阶段 4：笔记组装
  └→ deep-learning 轨道
      → 阶段 1：结构解析与证据提取
      → 阶段 2：Figure 论证路径分析
      → 阶段 3：模型架构 / 训练 / benchmark / ablation 分析
      → 阶段 4：笔记组装
```

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
/paper-to-note D:/papers/example.pdf --type experimental
/paper-to-note D:/papers/example.pdf --type dl
```

#### 自然语言

```text
用 paper-to-note 帮我读一下 D:/papers/example.pdf，开启交互模式，输出到 D:/vault/notes/
用 paper-to-note 帮我读一下 D:/papers/cvpr-paper.pdf，按 DL 轨道处理
```

### 3. 输出位置

- 默认输出到 PDF 所在目录
- 如果使用 `--output`，则输出到你指定的目录
- 文件名格式为：`{期刊/会议缩写}--{年份}--{主要内容概括}.md`
- 如遇同名文件，会自动追加序号，不覆盖已有文件

## 两种使用模式

| 模式 | 说明 |
|------|------|
| **普通模式** | 读取 PDF，自动路由并完成分析，直接生成完整笔记并写入文件 |
| **交互模式** `--interactive` | 在生成笔记前增加引导式讨论，记录你的理解、纠正点和未解决问题，并写入 `My Understandings` |

## 它是怎么工作的

整个流程大致如下：

```text
PDF 输入
  → 阶段 0：论文类型路由
  → 阶段 1：结构解析与关键原文片段提取
  → 阶段 2：Figure 论证路径分析
  → 阶段 3：按轨道提取关键信息
      experimental → 实验与参数
      deep-learning → 模型架构与训练 + Benchmark 与 Ablation
  → [交互模式] 引导式讨论
  → 阶段 4：笔记组装与质量检查
  → 写入 .md 文件
```

如果路由结果是 `review` 或 `theoretical`，skill 会先提示你：当前暂无专用轨道，可改走最接近的轨道或终止。

## 项目结构

```text
paper-to-note/
├── SKILL.md                         # skill 入口与执行规则
├── prompts/
│   ├── router.md                    # 阶段 0：论文类型路由
│   ├── experimental/
│   │   ├── parse-and-extract.md     # 阶段 1：结构解析与证据提取
│   │   ├── figure-logic.md          # 阶段 2：Figure 论证路径分析
│   │   ├── parameter-audit.md       # 阶段 3：实验与参数提取
│   │   └── note-assembly.md         # 阶段 4：笔记组装
│   └── dl/
│       ├── parse-and-extract.md     # 阶段 1：DL 结构解析与证据提取
│       ├── figure-logic.md          # 阶段 2：DL Figure 论证路径分析
│       ├── method-analysis.md       # 阶段 3：模型 / 训练 / benchmark / ablation 分析
│       └── note-assembly.md         # 阶段 4：DL 笔记组装
├── templates/
│   ├── note-template.md             # 实验型笔记模板
│   └── dl-note-template.md          # DL 笔记模板
└── examples/
    └── sample-output.md             # 输出示例
```

## 设计原则

1. **原文才是事实来源**  
   关键实验参数、训练配置和 benchmark 结果尽量附原文摘录，方便快速核查。

2. **对话不是证据**  
   `AI` 讨论用于帮助理解和整理思路，不作为事实依据。

3. **参数 / 超参数不能脱离上下文**  
   实验参数要挂在实验下面；DL 超参数要挂在训练、推理或具体模块下面。

4. **正文尽量保持单一语言**  
   正文默认用中文撰写，仅在必要时保留模型名、数据集名、指标缩写等专业名词。

5. **先路由，后总结**  
   先判断论文属于哪类，再进入对应分析框架，尽量减少“拿错模板”的情况。

6. **先证据，后总结**  
   先定位原文片段，再做概括和组织，尽量减少空泛转述。

## 更适合的场景

- 化学、材料、生物等实验型论文
- CV、NLP、语音、多模态等深度学习论文
- `Figure`、`Methods`、训练配置、benchmark 是核心证据的场景
- 英文论文输入，中文笔记输出的工作流

## Advanced

> **可选预处理：** 使用 MinerU (`pip install magic-pdf[full]`) 将 PDF 预转换为 Markdown 可节省 50-70% 输入 token，但会丢失 Figure 图像内容。适合论文 >30 页或批量处理的场景。

## 当前边界

- v2 已支持 `experimental + DL`，但 `review` / `theoretical` 暂无专用轨道
- 暂不适配非英文论文
- 需要可读取文本的 PDF，不适合扫描版 PDF
- 暂不处理独立的 `Supplementary Information` PDF
- 论文超过 40 页时，覆盖可能不完整
- 当路由置信度为 `medium` 或 `low` 时，skill 会先提示你确认再继续

## 许可

MIT

---
name: paper-to-note
description: "将实验型与深度学习论文 PDF 转为 evidence-backed 的 Obsidian Markdown 笔记。支持论文类型路由、Figure 论证路径分析，以及实验/模型训练信息的结构化整理。"
---

# Paper-to-Note

将实验型与深度学习论文 PDF 转为 evidence-backed 的 Obsidian Markdown 笔记。

## 触发条件

以下任一情况触发本 skill：
1. 用户使用 `/paper-to-note` 命令
2. 用户提到 `paper-to-note` 并描述了要读论文或生成笔记的意图
3. 用户提到 `deep learning` / `DL` / `深度学习`，并明确想读论文、拆 Figure、整理实验或生成笔记

## 参数识别

从用户输入中提取以下信息：

| 参数 | 必需 | 识别方式 |
|------|------|----------|
| **PDF 路径** | 是 | 用户提供的文件路径 |
| **交互模式** | 否 | 用户提到 `--interactive`、"交互"、"讨论"、"聊聊"则启用 |
| **输出目录** | 否 | 用户提到 `--output` 或指定输出路径；默认为 PDF 所在目录 |
| **类型覆盖** | 否 | 用户提到 `--type experimental` 或 `--type dl`；不提供时默认自动路由 |
| **MinerU 预处理** | 否 | `--mineru` 启用（自动选择模式）；`--mineru light` / `--mineru api` / `--mineru local` 指定模式；不提供时 Claude 直读 PDF |

## 执行流程

### 1. 读取论文

#### 默认模式（Claude 直读 PDF）

若未启用 `--mineru`，使用 Read 工具直接读取 PDF：

- 若 PDF ≤ 20 页：一次性读取全文
- 若 PDF > 20 页：先读 1-20 页完成主体分析，再读剩余页补充 Methods / Appendix / Supplementary 信息
- 若 PDF > 40 页：提示用户 "论文较长（{页数} 页），分析可能不完整，建议重点关注核心区域"
- 若读取失败：提示用户检查文件路径和 PDF 格式（需为文本型 PDF，非扫描型），终止流程

#### MinerU 预处理模式

若用户指定了 `--mineru`，先通过 MinerU 将 PDF 转为结构化 Markdown + 图片，再由 Claude 读取 Markdown 进行后续分析。

读取 `prompts/mineru-preprocess.md`，按其中的指令执行预处理。

预处理成功后：
- 后续所有阶段读取 MinerU 输出的 Markdown（公式已为 LaTeX，表格已为 HTML）
- Figure 分析时使用 Read 工具加载 `images/` 目录中的图片文件
- 原始 PDF 仍可作为补充参考

预处理失败时：
- 告知用户失败原因
- 自动回退至默认模式（Claude 直读 PDF），继续流程

### 2. 阶段 0：论文类型路由

若用户提供 `--type experimental` 或 `--type dl`，将其视为**手动覆盖**：
- `experimental` → 使用实验型轨道
- `dl` → 视为 `deep-learning` 轨道，使用 DL 轨道

若未提供手动覆盖，读取 `prompts/router.md`，按其中的指令执行。

根据路由结果选择 prompt 集：
- `experimental` → `prompts/experimental/` + `templates/note-template.md`
- `deep-learning` → `prompts/dl/` + `templates/dl-note-template.md`
- 其他类型（`review` / `theoretical`）→ 提示用户：该类型暂无专用轨道，可选择最接近的轨道继续或终止

若 `confidence` 为 `medium` 或 `low`，先提示用户确认检测结果再继续。

后续阶段 1-4 使用路由选中的 prompt 目录中的文件。

### 3. 阶段 1：结构解析与证据提取

根据当前轨道读取对应文件并执行：
- 实验型轨道：`prompts/experimental/parse-and-extract.md`
- DL 轨道：`prompts/dl/parse-and-extract.md`

### 4. 阶段 2：Figure 论证路径分析

根据当前轨道读取对应文件并执行：
- 实验型轨道：`prompts/experimental/figure-logic.md`
- DL 轨道：`prompts/dl/figure-logic.md`

### 5. 阶段 3：实验 / 方法分析

根据当前轨道读取对应文件并执行：
- 实验型轨道：`prompts/experimental/parameter-audit.md`
- DL 轨道：`prompts/dl/method-analysis.md`

### 6. 模式分流

**普通模式：** 直接进入阶段 4（笔记组装）。

**交互模式：** 进入引导讨论阶段：

#### 进入对话

告知用户：
> "论文已分析完毕，进入讨论阶段。我会针对这篇论文提问，帮你梳理理解。随时说「结束」即可生成笔记。"

#### 引导顺序（参考，非强制）

1. **整体感知**: "读完这篇文章，你觉得它主要在做一件什么事？"
2. **逐 Figure 讨论**: "Figure 1 你看到了什么？你觉得作者放这个图想说明什么？" → 逐个过
3. **思路串联**: "你觉得作者整个论证思路大概是怎么推进的？"
4. **开放疑问**（可选）: "有没有哪个地方你觉得没看懂，或者觉得奇怪的？"

#### 交互原则

- **用户掌握主动权** — AI 准备好引导路线，但用户随时可以改道，AI 跟着走
- **每次只问一个问题** — 不一次性抛多个问题
- **用户可跳过** — 说 "跳过" / "继续 Figure 3" → AI 立刻跟上
- **用户可回溯** — 想聊回之前的 Figure → AI 跟上
- **仅由用户主动结束** — 说 "结束" / "可以了" / "生成笔记" → 停止对话，AI 不自行终止
- **语气像导师带读论文** — 不是考官答辩，是引导式讨论
- **纠正附证据** — 用户理解有偏差时，基于原文和阶段产出纠正，不空口说"你错了"
- **只记录聊过的** — `My Understandings` 只包含实际讨论的内容，跳过的 Figure 或模块不补

### 7. 阶段 4：笔记组装

根据当前轨道选择模板与组装 prompt：
- 实验型轨道：读取 `templates/note-template.md` 和 `prompts/experimental/note-assembly.md`
- DL 轨道：读取 `templates/dl-note-template.md` 和 `prompts/dl/note-assembly.md`

按对应 prompt 的指令将所有阶段产出组装成最终笔记。

### 8. 生成文件名与写入

**文件名格式：** `{期刊/会议缩写}--{年份}--{主要内容概括}.md`

规则：
- 缩写中的空格用 `-` 替代（如 `ACS-Nano`、`CVPR`）
- 主要内容用中文概括
- `--` 双连字符作分隔符
- 文件名不含空格
- 文件系统非法字符（`/ : * ? " < > |`）替换为 `-`

**输出路径：** 用户指定的目录，或 PDF 所在目录（默认）。

**文件名冲突：** 若目标目录下已存在同名文件，自动追加序号（如 `-2`），不覆盖已有文件。

使用 Write 工具写入文件。完成后告知用户：
> "笔记已生成：{完整文件路径}"

## 通用格式规范

以下规则适用于所有轨道的最终输出：

- **数学公式**：论文中的数学表达式必须使用 LaTeX 语法。行内公式用 `$...$`，独立公式（目标函数、损失函数等）用 `$$...$$` 并独占一行。不允许将公式写成纯文本（如 `p_data` 应为 `$p_{\text{data}}$`，`E[log D(x)]` 应为 `$\mathbb{E}[\log D(x)]$`）。详细规范见各轨道的 note-assembly prompt。

## 适用范围

- 实验型论文（化学、材料、生物等）
- 深度学习论文（CV、NLP、语音、多模态等）
- 英文论文输入
- 中文笔记输出（专业术语保留英文）

## 限制

- v2 已支持 `experimental + DL`，其他类型轨道仍在补充中
- 暂不处理独立的 `Supplementary Information` PDF
- 超 40 页论文分析可能不完整
- 扫描型 PDF 无法读取

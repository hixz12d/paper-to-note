# 阶段 1：DL 结构解析与证据提取

## 任务

你已经读取了一篇深度学习论文的 PDF。现在需要完成两件事：
1. 提取论文的元数据和结构
2. 从全文中提取可供后续阶段引用的关键原文片段

## 规则

### 1. 论文类型检查

如果这篇论文明显不是深度学习论文，而更像实验型、综述型或理论型论文，在输出开头先标注：

> ⚠️ 本文可能为 {类型} 论文，非深度学习轨道。paper-to-note 的 DL 轨道针对模型、训练配置、benchmark 和 ablation 设计，当前结构可能不完全适用。是否继续？

用户确认后继续，不强制中止。

### 2. 元数据提取

提取以下信息（识别不到的留空，绝不猜测）：
- 标题（英文原文）
- 作者列表
- Venue（如 CVPR / ICCV / ECCV / NeurIPS / ICLR / TPAMI / arXiv）
- 会议 / 期刊全名
- 发表年份
- DOI / URL

### 3. 结构切分

识别并提取以下区块：
- **Abstract**: 原文摘要全文
- **Introduction 要点**: 用 2-3 句话概括论文想解决的问题和研究动机
- **Related Work 摘要**: 归纳关键 prior approaches，以及作者认为的缺口
- **Method / Architecture**: 模型方法或架构描述的关键原文
- **Experiments / Benchmarks**: 实验设置、任务、评测协议、主要结果
- **Ablation Studies**: 消融实验原文或其摘要
- **Sections**: 各 section 标题 + 一句话标注内容
- **Figure captions**: 逐个列出所有 Figure caption（Figure 1, Figure 2, ...）
- **Tables**: benchmark / ablation / complexity 表格内容或文字描述
- **Conclusions**: 原文结论段

如果某个区块在论文中不存在，明确写 `[未明确给出]`，不要猜测补全。

### 4. 关键原文片段提取

从论文全文中提取关键英文原文片段，供后续阶段使用。这些片段**只在当前对话上下文中使用**，不会直接写入最终笔记。

按以下类别提取，类别名保持 English，片段内容保留原文 English，不翻译：

- `Model architecture descriptions`
- `Training configuration`
- `Dataset info`
- `Benchmark numbers`
- `Ablation results`
- `Author's core claims`

每条片段尽量附带来源区域，例如 `Section 3.2`, `Table 2`, `Figure 4 caption`。

### 5. 语言规则（最高优先级，严格执行）

1. 正文说明用中文撰写
2. 以下内容保留英文：
   - 模型名 / 架构名：`ResNet`, `ViT`, `YOLO`, `U-Net`, `DETR`, `SAM`, `GAN`, `Diffusion`
   - 指标缩写：`mAP`, `IoU`, `FID`, `PSNR`, `SSIM`, `BLEU`, `Top-1`, `AUC`
   - 数据集名：`ImageNet`, `COCO`, `VOC`, `ADE20K`, `Cityscapes`, `CIFAR-10`
   - 层 / 模块名：`Conv`, `BN`, `LN`, `ReLU`, `GELU`, `Softmax`, `MLP`, `Patch Embedding`
   - 优化器名 / 损失函数名在作为专有值时可保留英文，如 `AdamW`, `SGD`, `Cross-Entropy`
3. 以下常见术语统一译成中文：
   - `feature map` → 特征图
   - `backbone` → 骨干网络
   - `attention` → 注意力
   - `pooling` → 池化
   - `skip connection` → 跳跃连接
   - `head` → 检测头 / 任务头（按上下文）
   - `neck` → 特征融合层
   - `anchor` → 锚框
   - `embedding` → 嵌入
   - `fine-tuning` → 微调
   - `pre-training` → 预训练
   - `inference` → 推理
   - `epoch` → 训练轮数
   - `dropout` → 随机失活
   - `batch normalization` → 批归一化
   - `layer normalization` → 层归一化
   - `encoder` → 编码器
   - `decoder` → 解码器
   - `upsampling` → 上采样
   - `downsampling` → 下采样
   - `bounding box` → 边界框
   - `ground truth` → 真值标注
   - `feature pyramid` → 特征金字塔
   - `depthwise separable convolution` → 深度可分离卷积
   - `data augmentation` → 数据增强
   - `loss function` → 损失函数
   - `weight decay` → 权重衰减
4. 首次出现的重要概念可写成”中文（English）”，之后优先使用中文
5. 原文摘录始终保持英文，不翻译
6. 数学表达式使用 LaTeX 语法：行内用 `$...$`，独立公式用 `$$...$$`。下标用 `_{}`（如 `$p_{\text{data}}$`），数学算子用 `\min`、`\max`、`\log`，期望用 `\mathbb{E}`。不要将公式写成纯文本（如 `p_data`、`E[...]`）

## 输出格式

严格按以下格式输出：

---

## 元数据
- 标题: ...
- 作者: ...
- Venue: ...
- 会议/期刊: ...
- 年份: ...
- DOI/URL: ...

## 论文结构
- **Abstract**: （原文摘要）
- **Introduction 要点**: （2-3 句中文）
- **Related Work 摘要**: （中文概括）
- **Method / Architecture**: （关键原文或摘要）
- **Experiments / Benchmarks**: （关键原文或摘要）
- **Ablation Studies**: （关键原文或摘要）
- **Sections**: （列表）
- **Figure captions**: （逐个列出）
- **Tables**: （内容或描述）
- **Conclusions**: （原文结论）

## 关键原文片段

### Model architecture descriptions
- [来源] "..."

### Training configuration
- [来源] "..."

### Dataset info
- [来源] "..."

### Benchmark numbers
- [来源] "..."

### Ablation results
- [来源] "..."

### Author's core claims
- [来源] "..."

---

## Notes

- 本阶段以提取为主，不做长篇总结，不做越界推断
- 元数据识别不到就留空，不允许猜测
- 证据片段宁多勿少，但只保留真正对后续分析有用的句子

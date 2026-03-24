# 阶段 2：DL Figure 论证路径分析

## 任务

基于阶段 1 提取的论文结构和关键原文片段，分析论文中每个 Figure 的作用，梳理作者如何通过 Figure 建立方法合理性、实验有效性和结论可信度。

**这仍然是整个 skill 的核心价值区块之一。**

## 规则

### 1. 对每个 Figure 的分析维度保持固定

每个 Figure 都必须分析以下 4 个维度：
1. **作用**：这个 Figure 在整篇论文论证中扮演什么角色？
2. **内容**：这个 Figure 具体展示了什么？有哪些关键对比、趋势或可视化对象？
3. **支撑结论**：作者希望用这个 Figure 证明什么具体结论？
4. **与下文关系**：这个 Figure 如何引出下一个 Figure、下一组实验或下一层论证？

如果某个 Figure 有子图（a / b / c / d ...）且作用明显不同，应分别说明。

### 2. 先判断 Figure 类型，再决定分析重点

| Figure 类型 | 分析重点 |
|-------------|----------|
| Architecture overview | 数据流如何推进、模块如何组合、创新点具体落在哪一层 |
| Module detail diagram | 具体操作、维度变化、与标准做法相比改了什么 |
| Training curves | 收敛速度、稳定性、是否有过拟合信号、与 baseline 的差异 |
| Feature / attention visualization | 模型学到了什么、可解释性证据在哪里 |
| Qualitative comparison | 与 SOTA 的视觉差异在哪里，如检测框、分割 mask、生成效果 |
| Ablation charts / tables | 每个组件带来的性能贡献有多大 |
| t-SNE / feature distribution | 表征空间是否更可分、类间 / 类内结构是否更清晰 |
| Efficiency / tradeoff curves | 精度-延迟、精度-参数量、精度-FLOPs 之间的取舍关系，模型在 Pareto 前沿的位置 |

### 3. 整体分析必须给出故事线

除了逐图分析，还要输出：
- **整体思路**：概括作者用 Figure 讲了一个什么故事
- **论证逻辑链**：用箭头链或短段落串联所有 Figure 之间的推进关系

### 4. 分析原则

- **必须回答“为什么作者要放这个图”，不能只描述“图里画了什么”**
- 优先基于 `Figure caption` + 正文中引用该 Figure 的段落进行分析
- 图像内容可作为辅助；当图像不可读时，完全基于文本分析并标注 `[图像未参考]`
- 如果作用不确定，明确标注 `[作用待确认]`，不要硬编
- 如果论文没有 Figure，输出 `本文未包含 Figure，跳过此区块`

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

## Figure 论证路径

### 整体思路

（概括性段落）

### Figure 1: （简短描述）

- **作用**: ...
- **内容**: ...
- **支撑结论**: ...
- **与下文关系**: ...

### Figure 2: （简短描述）

（同结构，按实际 Figure 数量展开）

### 论证逻辑链

Figure 1（描述 → 结论）
  → Figure 2（描述 → 结论）
  → Figure 3（描述 → 结论）
  → ...

---

## Notes

- 不编造论文中不存在的信息
- 每个 Figure 的分析都要有据可依，尤其要和正文中的 claim 对齐
- 对 DL 论文而言，Figure 常同时承担“解释方法”和“证明有效”的双重角色，这两层都要看见

# 阶段 0：论文类型路由

## 任务

你已经读取论文 PDF。现在只做一件事：根据论文的标题、摘要、section 标题、关键词、Figure / Table 说明和正文内容，判断这篇论文最适合进入哪条分析轨道。

候选类型只有 4 类：
- `experimental`
- `deep-learning`
- `review`
- `theoretical`

目标是给后续阶段提供**简洁、保守、可解析**的路由结果，而不是写一篇长分析。

## 规则

### 1. 必须综合多种信号判断，不能只看单一关键词

| 类型 | 重点检测信号 |
|------|--------------|
| `experimental` | `Methods` / `Experimental` 区块、合成步骤、表征数据（XRD / TEM / SEM / NMR 等）、化学式、产率、反应条件 |
| `deep-learning` | `Architecture` / `Model` 区块、`Training` / `Dataset` 区块、benchmark 表、loss / accuracy 曲线、超参数（learning rate / batch size / epochs）、模型名（CNN / Transformer / GAN / Diffusion）、ablation study |
| `review` | 标题中出现 `review` / `survey`、系统化分类梳理、没有原创实验、引用驱动的 taxonomy |
| `theoretical` | 数学推导、定理 / 证明、解析公式占主体、没有实验验证或实验仅为极少量附带说明 |

### 2. 推荐判断顺序

按以下顺序快速交叉核验：
1. 标题 + 摘要：看论文自我定位
2. Section 标题：看主体结构
3. Figure / Table：看证据形式
4. Methods / Appendix / Experiments：看是否存在具体实验或训练细节
5. 结论：看作者最终 claim 是方法、实验发现、综述总结还是理论证明

### 3. 多类型混合时的判定

- 如果检测到多种类型，选**主导类型**作为 `paper_type`
- 同时用 `secondary_type` 记录次要类型；若没有明显次要类型，填 `none`
- 主导类型应由**核心贡献 + 篇幅占比 + 证据密度**共同决定
- 例如：带少量湿实验验证的模型论文，若主体是模型设计、训练、benchmark、ablation，应归为 `deep-learning`

### 4. 置信度标准

- `high`：结构和信号高度一致，几乎没有冲突
- `medium`：主导类型较明显，但混有另一条轨道的强信号
- `low`：信息不足、结构混杂，或论文过短导致难以确认

### 5. 缺失 section 时的处理

- 没有明确 `Methods` / `Experimental` 标题，不等于不是实验论文
- 没有明确 `Architecture` / `Training` 标题，不等于不是 DL 论文
- 可以用 benchmark 表、ablation、公式密度、citation 组织方式补充判断

### 6. 输出必须短

- 只输出路由结果
- 不写长段落解释
- `evidence` 只列 3-6 条最关键的可观察信号
- 不要输出任何寒暄或额外建议

## 输出格式

严格按以下格式输出：

```text
paper_type: experimental | deep-learning | review | theoretical
confidence: high | medium | low
secondary_type: experimental | deep-learning | review | theoretical | none
evidence:
  - ...
  - ...
  - ...
```

## Notes

- 本阶段只做路由，不做结构提取，不做笔记组装
- 所有 `evidence` 必须来自当前论文中可观察到的内容，不能用常识代替证据
- 无法确认时，保持保守：给出最可能类型 + `low` 置信度

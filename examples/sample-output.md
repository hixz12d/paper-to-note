# Nat-Commun--2021--超分辨形态相关细胞器识别追踪多细胞器$Zn^{2+}$

> **Title**: Simultaneous Zn2+ tracking in multiple organelles using super-resolution morphology-correlated organelle identification in living cells
> **Authors**: Hongbao Fang, Shanshan Geng, Mingang Hao, Qixin Chen, Minglun Liu, Chunyan Liu, Zhiqi Tian, Chengjun Wang, Takanori Takebe, Jun-Lin Guan, Yuncong Chen, Zijian Guo, Weijiang He & Jiajie Diao
> **Journal**: Nature Communications, 2021
> **DOI**: https://doi.org/10.1038/s41467-020-20309-7

---

## 研究概述

游离 $Zn^{2+}$ 在细胞代谢和信号调控中发挥重要作用，被视为潜在的"第二信使"[[#^ref-4|[4]]]，锌火花（zinc sparks）和锌波（zinc waves）等新现象的发现进一步揭示了其信号活性[[#^ref-8|[8]]]。不同细胞器具有不同的 $Zn^{2+}$ 水平和动态变化[[#^ref-10|[10]]]，多个涉及多细胞器协作的生理过程（尤其是自噬）与 $Zn^{2+}$ 波动密切相关[[#^ref-11|[11]]]。然而，此前没有方法能用单个探针同时追踪两个以上细胞器中的 $Zn^{2+}$ 信号——荧光成像需要多轮双染色和不同探针[[#^ref-21|[21]]]，同步辐射 X 射线荧光显微镜（SXRF）虽可同时检测但仅适用于脱水细胞。

本文提出了**多细胞器同步 $Zn^{2+}$ 追踪方法（Zn-STIMO）**，结合结构光照明显微镜（SIM，空间分辨率 ~100 nm[[#^ref-28|[28]]]）和单一 $Zn^{2+}$ 荧光探针 NapBu-BPEA，通过超分辨形态识别在活细胞中同步追踪多个细胞器的 $Zn^{2+}$ 动态。探针设计的核心策略是通过调节萘酰亚胺衍生物的亲脂性，使其在不添加靶向基团的情况下分布于除细胞核外的多个细胞器。

利用 Zn-STIMO，作者发现 CCCP 诱导的线粒体自噬伴随游离 $Zn^{2+}$ 升高，且不同细胞器中的 $Zn^{2+}$ 变化存在显著差异——自噬体/自噬溶酶体中增幅最大，线粒体次之，内质网最小；而 EBSS 诱导的饥饿自噬则表现为 $Zn^{2+}$ 降低。此外，NapBu-BPEA 在人源肝脏类器官中也实现了超分辨细胞器成像，展示了该方法向更复杂生物系统拓展的潜力。

---

## Figure 论证路径

### 整体思路

作者通过 8 个 Figure 构建了一条从概念提出→探针设计与验证→细胞内功能验证→生物学应用→方法拓展的完整论证链。先展示 Zn-STIMO 的方法概念和探针设计逻辑（Fig. 1），然后在体外验证探针的光谱性质和 $Zn^{2+}$ 响应（Fig. 2），接着在活细胞中验证多细胞器分布和 SIM 成像能力（Fig. 3），再确认细胞内 $Zn^{2+}$ 可逆传感（Fig. 4），随后进入核心生物学应用——自噬过程中的 $Zn^{2+}$ 动态（Fig. 5），用 Zn-STIMO 揭示不同细胞器的差异化响应（Fig. 6），展示时间分辨动态追踪（Fig. 7），最终将方法拓展到三维类器官系统（Fig. 8）。

### Figure 1: Zn-STIMO 概念与探针分子设计

- **作用**: 提出整体研究方案，展示通过调节亲脂性设计多细胞器分布探针的策略
- **内容**: (a) Zn-STIMO 概念示意图——用 SIM + 单一探针实现形态识别的多细胞器 $Zn^{2+}$ 追踪；(b) 探针分子设计——以 1,8-萘酰亚胺（Nap）为母核[[#^ref-35|[35]]]，BPEA 为 $Zn^{2+}$ 螯合基团[[#^ref-37|[37]]]，通过将乙二醇尾链替换为烷基链（乙基→NapEt-BPEA、丁基→NapBu-BPEA）提高亲脂性
- **支撑结论**: 亲脂性调节可有效改变探针的亚细胞分布——前体 Naph-BPEA 在 $Zn^{2+}$ 加载后会重分布至细胞核[[#^ref-39|[39]]]，而 NapBu-BPEA 通过增大 $\log P$ 避免了这一问题
- **与下文关系**: 确立了探针候选分子 NapBu-BPEA，引出其体外光谱表征

### Figure 2: NapBu-BPEA 光谱特性与 $Zn^{2+}$ 响应

- **作用**: 系统验证探针的光学性质、$Zn^{2+}$ 特异性响应及可逆性
- **内容**: 吸收/发射光谱；$Zn^{2+}$ 滴定荧光增强曲线（$F/F_0 = 3.6$）；阳离子选择性测试（$\text{Na}^+$、$\text{K}^+$、$\text{Ca}^{2+}$、$\text{Mg}^{2+}$ 1000 当量无干扰）；TPEN 螯合后荧光恢复的可逆性循环；pH 独立性
- **支撑结论**: NapBu-BPEA 具有高量子产率（$\Phi = 0.80$）、高选择性、可逆的 $Zn^{2+}$ 荧光增强响应，$K_d = 4.98\ \text{nM}$ 适合检测细胞器中游离 $Zn^{2+}$（0.2–70 nM 范围）
- **与下文关系**: 体外验证完毕，转向细胞内分布和 SIM 成像验证

### Figure 3: SIM 超分辨成像与多细胞器共定位

- **作用**: 证明 NapBu-BPEA 可分布于多个细胞器，且 SIM 成像下可通过形态识别细胞器
- **内容**: 与四种细胞器标记物的共定位（PCC：内质网 0.717、线粒体 0.563、溶酶体 0.509、细胞核 0.086）；SIM vs 共聚焦对比——SIM 下可清晰分辨点状溶酶体、棒状线粒体嵴和网状内质网；FWHM 达 100 nm（与 Atto 647N 的 91 nm 相当[[#^ref-47|[47]]]）；光稳定性优于 MitoTracker Deep Red
- **支撑结论**: NapBu-BPEA 在 SIM 下实现了 ~100 nm 空间分辨率，可通过形态特征区分线粒体、内质网和溶酶体，且光稳定性优异
- **与下文关系**: 成像基础建立，转向验证探针在细胞内能否可逆感应 $Zn^{2+}$

### Figure 4: 细胞内可逆 $Zn^{2+}$ 传感

- **作用**: 验证 NapBu-BPEA 在活细胞中对外源 $Zn^{2+}$ 的可逆响应能力
- **内容**: ZnPT 加载后荧光即时增强（前 4 min 线性增长）；TPEN 螯合后荧光恢复；剂量依赖性；加载/螯合过程中探针点状分布模式不变（区别于 Naph-BPEA 向细胞核重分布[[#^ref-39|[39]]]）
- **支撑结论**: NapBu-BPEA 可在活细胞中可逆追踪游离 $Zn^{2+}$，且 $Zn^{2+}$ 结合不改变其亚细胞分布，满足 Zn-STIMO 的核心要求
- **与下文关系**: 传感功能验证完成，正式进入生物学应用——自噬中的 $Zn^{2+}$ 动态

### Figure 5: 线粒体自噬中的 $Zn^{2+}$ 变化

- **作用**: 揭示 CCCP 诱导的线粒体自噬与游离 $Zn^{2+}$ 升高之间的关联
- **内容**: 自噬细胞 vs 非自噬细胞荧光对比（~2.0 倍增强）；TPEN 验证增强来自游离 $Zn^{2+}$；CCCP 处理后动态追踪（初始 5 min 快速升高，随后缓慢）；ATG13 KO[[#^ref-51|[51]]] 和 FIP200 KO[[#^ref-50|[50]]] HeLa 细胞作为对照——CCCP 不诱导自噬也不引起 $Zn^{2+}$ 升高；EBSS 诱导的非选择性自噬反而导致 $Zn^{2+}$ 降低
- **支撑结论**: CCCP 诱导的线粒体自噬伴随游离 $Zn^{2+}$ 升高，该效应依赖自噬通路（KO 验证）；不同类型自噬对 $Zn^{2+}$ 的影响方向不同
- **与下文关系**: 整体 $Zn^{2+}$ 变化确认后，引出核心问题——不同细胞器中 $Zn^{2+}$ 如何差异化变化？

### Figure 6: Zn-STIMO 揭示细胞器差异化 $Zn^{2+}$ 响应

- **作用**: 核心创新——首次用单一探针在亚细胞水平定量展示不同细胞器的 $Zn^{2+}$ 差异化响应
- **内容**: CCCP 诱导线粒体自噬后各细胞器 $Zn^{2+}$ 增强倍数——自噬体/自噬溶酶体最高、线粒体 ~1.89×、内质网 ~1.55×；NapBu-BPEA 与 DAPRed 在 CCCP 处理细胞中 PCC ~0.70（确认探针进入自噬体）；$Zn^{2+}$ 热力图显示线粒体和内质网内部分布不均匀；EBSS 诱导自噬中线粒体和内质网 $Zn^{2+}$ 均降低
- **支撑结论**: Zn-STIMO 成功实现了亚细胞水平 $Zn^{2+}$ 的差异化定量，CCCP 自噬中 $Zn^{2+}$ 升高主要来源于自噬体/溶酶体区室
- **与下文关系**: 静态差异化结果确认，引出时间分辨动态追踪

### Figure 7: 动态 Zn-STIMO 时间分辨追踪

- **作用**: 展示 Zn-STIMO 方法的时间分辨动态追踪能力
- **内容**: CCCP 处理后的时间序列 SIM 成像，展示各细胞器 $Zn^{2+}$ 随时间的变化趋势
- **支撑结论**: CCCP 处理 5 min 即可观察到明显 $Zn^{2+}$ 增强，自噬体/自噬溶酶体的增强最为显著
- **与下文关系**: 方法在细胞层面全面验证，引出向更复杂系统的拓展

### Figure 8: 肝脏类器官中的超分辨成像

- **作用**: 将 Zn-STIMO 从二维细胞培养拓展至三维人源类器官系统
- **内容**: CCCP 处理的人 iPSC 分化肝脏类器官[[#^ref-56|[56]]]的 Z-stack SIM 成像（深度 2.4、6.4、14.4 $\mu\text{m}$）；分辨率 <200 nm；可通过形态识别内质网
- **支撑结论**: NapBu-BPEA + SIM 可在复杂三维类器官中实现细胞器识别和 $Zn^{2+}$ 分布追踪
- **与下文关系**: 终点——展示 Zn-STIMO 在类器官及更复杂组织中的应用前景

### 论证逻辑链

Figure 1（概念与探针设计 → 亲脂性调控策略）
  → Figure 2（体外光谱验证 → 高量子产率、高选择性、可逆响应）
  → Figure 3（细胞多细胞器分布 + SIM 100 nm 分辨率 → 形态识别可行）
  → Figure 4（细胞内 $Zn^{2+}$ 可逆传感 → 分布不变，功能确认）
  → Figure 5（线粒体自噬 + $Zn^{2+}$ 升高 → 生物学关联建立）
  → Figure 6（Zn-STIMO 差异化定量 → 自噬体 > 线粒体 > 内质网）
  → Figure 7（动态时间分辨追踪 → 方法完整性验证）
  → Figure 8（类器官成像 → 拓展至三维复杂系统）

---

## 实验与参数

### 实验 1: NapBu-BPEA 体外光谱表征

**目的**: 系统评价 NapBu-BPEA 的光学性质和 $Zn^{2+}$ 响应特性
**方法概述**: 在 HEPES 缓冲液中测量吸收/发射光谱、$Zn^{2+}$ 滴定曲线、阳离子选择性和可逆性

| 参数 | 值 |
|------|-----|
| 探针浓度 | $10\ \mu\text{M}$ |
| 缓冲液 | HEPES（50 mM，含 100 mM $\text{KNO}_3$，10% DMSO，pH 7.2） |
| 激发波长 | 450 nm |
| 最大吸收波长 ($\lambda_{\max}$) | 454 nm |
| 摩尔消光系数 ($\varepsilon$) | $1.226 \times 10^4\ \text{M}^{-1}\text{cm}^{-1}$ |
| 发射峰 | 540 nm（加 $Zn^{2+}$ 后蓝移至 535 nm） |
| 量子产率——游离态 ($\Phi$) | 0.32 |
| 量子产率——$Zn^{2+}$ 络合态 ($\Phi$) | 0.80 |
| 荧光增强倍数 ($F/F_0$) | 3.6（540 nm） |
| 解离常数 ($K_d$) | 4.98 nM |
| 化学计量比 | 1:1（Job's plot + HR-MS 确认） |
| pH 响应范围 | 4.0–8.0（$Zn^{2+}$ 响应不受 pH 影响） |
| $\log P$（游离态） | 4.97 |
| $\log P_{\text{Zn}}$（络合态） | 8.53 |
| $\Delta E_{\text{ST}}$ | ~1.04 eV（不利于系间窜越→低 ROS，高光稳定性） |

> **原文参考** — "The broad absorption band of NapBu-BPEA was centered at 454 nm with the molar absorption coefficient ε = 1.226 × 10⁴ M⁻¹cm⁻¹. The emission was centered at 540 nm; quantum yield Φ = 0.32. The fluorescence spectra of NapBu-BPEA with the gradual addition of Zn²⁺ showed a linear emission enhancement, and a stable emission spectrum was achieved at 1 equivalent of Zn²⁺."

### 实验 2: 细胞培养与细胞毒性评价

**目的**: 评估 NapBu-BPEA 对 HeLa 细胞的毒性和孵育条件
**方法概述**: HeLa 细胞与 NapBu-BPEA 共孵育，WST 法（LDH 释放）检测细胞活力

| 参数 | 值 |
|------|-----|
| 细胞系 | HeLa（野生型、FIP200 KO、ATG13 KO） |
| 培养基 | DMEM + 10% FBS |
| 探针浓度 | $20\ \mu\text{M}$ |
| 孵育时间 | 1 h（10 min 开始出现荧光，1 h 分布稳定） |
| 细胞毒性检测 | WST 法（LDH 释放） |
| 24 h 细胞活力 | >80% |

> **原文参考** — "Cell viability >80% after 24 h incubation with 20 μM probe (low cytotoxicity). Punctate fluorescence in cytoplasm (not nucleus) after 10 min; stabilized at 1 h."

### 实验 3: SIM 超分辨成像

**目的**: 利用 SIM 实现 NapBu-BPEA 标记的活细胞超分辨成像
**方法概述**: 使用 Nikon N-SIM 系统对活细胞进行结构光照明成像

| 参数 | 值 |
|------|-----|
| 成像系统 | Nikon N-SIM |
| 激发波长 | 488 nm |
| 发射收集范围 | 500–550 nm |
| 空间分辨率（FWHM） | ~100 nm |
| 参考基准 | Atto 647N: 91 nm |
| 光稳定性 | 300 s SIM 激发下荧光几乎不衰减 |
| 对照光稳定性 | MitoTracker Deep Red 120 s 后降至 <30% |

> **原文参考** — "SIM via NapBu-BPEA achieved FWHM down to 100 nm (comparable to Atto 647N at 91 nm). NapBu-BPEA fluorescence nearly stable over 300 s SIM excitation; MTDR dropped to <30% after 120 s."

### 实验 4: 共定位分析

**目的**: 定量验证 NapBu-BPEA 在不同细胞器中的分布
**方法概述**: 与商用细胞器标记物双通道 SIM 成像，计算 Pearson 相关系数（PCC）

| 参数 | 值 |
|------|-----|
| 溶酶体标记物 | LysoTracker Red |
| 溶酶体 PCC | 0.509 |
| 线粒体标记物 | MitoTracker Deep Red |
| 线粒体 PCC | 0.563 |
| 内质网标记物 | ER-Tracker Red |
| 内质网 PCC | 0.717 |
| 细胞核标记物 | Hoechst 33258 |
| 细胞核 PCC | 0.086（基本不进入细胞核） |
| 分析软件 | CellProfiler |

> **原文参考** — "Co-localization Pearson's correlation coefficients (PCCs): LysoTracker Red (lysosomes) 0.509, MitoTracker Deep Red (mitochondria) 0.563, ER-Tracker Red (ER) 0.717, Hoechst 33258 (nucleus) 0.086."

### 实验 5: 细胞内 $Zn^{2+}$ 可逆传感

**目的**: 验证 NapBu-BPEA 在活细胞中对外源 $Zn^{2+}$ 加载和螯合的可逆响应
**方法概述**: 用 ZnPT 向细胞递送 $Zn^{2+}$，观察荧光增强；再用 TPEN 螯合，验证可逆性

| 参数 | 值 |
|------|-----|
| $Zn^{2+}$ 递送载体 | ZnPT |
| 荧光增强特征 | 加入 ZnPT 后即刻增强，前 4 min 近线性增长，~4 min 后稳定 |
| 剂量响应 | ZnPT 浓度越高，荧光增强越大 |
| 螯合剂 | TPEN |
| 螯合效果 | 荧光显著降低，确认可逆性 |
| 分布变化 | 加载/螯合全程保持点状细胞质分布，不进入细胞核 |

> **原文参考** — "Exogenous Zn²⁺ loading via ZnPT: instant fluorescence enhancement, almost linear increase in first 4 min, stable after 4 min. Punctate cytoplasmic distribution retained upon Zn²⁺ loading (unlike Naph-BPEA which redistributes to nucleus)."

### 实验 6: 自噬诱导与多细胞器 $Zn^{2+}$ 追踪（Zn-STIMO）

**目的**: 研究不同自噬模型中各细胞器的 $Zn^{2+}$ 动态变化
**方法概述**: CCCP 或 EBSS 分别诱导线粒体自噬和非选择性自噬，用 NapBu-BPEA/SIM 进行多细胞器 $Zn^{2+}$ 差异化追踪

| 参数 | 值 |
|------|-----|
| CCCP 浓度 | $10\ \mu\text{M}$ |
| CCCP 长期处理 | 24 h |
| CCCP 动态追踪 | 初始 5 min 快速升高，随后缓慢 |
| 自噬检测试剂 | DAPRed（$1\ \mu\text{M}$，孵育 30 min） |
| NapBu-BPEA 与 DAPRed 的 PCC（CCCP 处理后） | ~0.70 |
| 自噬细胞整体 $Zn^{2+}$ 增强 | ~2.0 倍（vs 非自噬细胞） |
| 线粒体 $Zn^{2+}$ 增强 | ~1.89× |
| 内质网 $Zn^{2+}$ 增强 | ~1.55× |
| 自噬体/自噬溶酶体 | $Zn^{2+}$ 增幅最大 |
| EBSS 诱导结果 | $Zn^{2+}$ 降低（与 CCCP 相反） |
| 基因敲除对照 | ATG13 KO、FIP200 KO HeLa：CCCP 不诱导自噬也不引起 $Zn^{2+}$ 升高 |
| 统计方法 | 均值 $\pm$ 标准差，双尾 Student's $t$-test，$p < 0.05$ |

> **原文参考** — "NapBu-BPEA fluorescence in mitophagic cells: ~2.0-fold higher than non-autophagic cells. ATG13 KO and FIP200 KO HeLa cells: CCCP did not induce autophagy or Zn²⁺ enhancement, confirming CCCP-induced Zn²⁺ release is autophagy-associated."

### 实验 7: 肝脏类器官超分辨成像

**目的**: 验证 Zn-STIMO 方法在三维人源类器官中的适用性
**方法概述**: 在 CCCP 处理的 iPSC 分化肝脏类器官中进行 Z-stack SIM 成像

| 参数 | 值 |
|------|-----|
| 类器官来源 | 人 iPSC 诱导分化肝脏类器官 |
| 分化方案 | 参照 Koike 等人方案 |
| CCCP 处理 | 同细胞实验条件 |
| 探针孵育时间 | 2 h |
| Z-stack 成像深度 | 2.4、6.4、14.4 $\mu\text{m}$ |
| 空间分辨率 | <200 nm |
| 可识别细胞器 | 内质网（基于网状形态） |

> **原文参考** — "Z-stack SIM imaging of CCCP-treated liver organoids incubated with NapBu-BPEA (2 h). Non-uniform fluorescence in cytoplasm at depths of 2.4, 6.4, and 14.4 μm. Imaging resolution <200 nm in organoids."

---

## 参考文献索引

4. Berg, J. M. & Shi, Y. The galvanization of biology: a growing appreciation for the roles of zinc. *Science* 271, 1081–1085 (1996).
  ^ref-4

8. Que, E. L. et al. Quantitative mapping of zinc fluxes in the mammalian egg reveals the origin of fertilization-induced zinc sparks. *Nat. Chem.* 7, 130–139 (2015).
  ^ref-8

10. Kambe, T. et al. The physiological, biochemical, and molecular roles of zinc transporters in zinc homeostasis and metabolism. *Physiol. Rev.* 95, 749–784 (2015).
  ^ref-10

11. Liuzzi, J. P. et al. Zinc and autophagy. *Biometals* 27, 1087–1096 (2014).
  ^ref-11

21. Miranda, J. G. et al. New alternately colored FRET sensors for simultaneous monitoring of Zn²⁺ in multiple cellular locations. *PLoS ONE* 7, e49371 (2012).
  ^ref-21

28. Huang, X. et al. Fast, long-term, super-resolution imaging with Hessian structured illumination microscopy. *Nat. Biotechnol.* 36, 451–459 (2018).
  ^ref-28

35. Li, X. et al. A fast and specific fluorescent probe for thioredoxin reductase that works via disulphide bond cleavage. *Nat. Commun.* 10, 2745 (2019).
  ^ref-35

37. Xu, Z. et al. Fluorescent chemosensors for Zn²⁺. *Chem. Soc. Rev.* 39, 1996–2006 (2010).
  ^ref-37

39. Zhang, C. et al. In vitro and in vivo imaging application of a 1,8-naphthalimide-derived Zn²⁺ fluorescent sensor with nuclear envelope penetrability. *Chem. Commun.* 49, 11430–11432 (2013).
  ^ref-39

47. Han, Y. et al. Cell-permeable organic fluorescent probes for live-cell long-term super-resolution imaging reveal lysosome-mitochondrion interactions. *Nat. Commun.* 8, 1307 (2017).
  ^ref-47

50. Liu, F. & Guan, J. L. FIP200, an essential component of mammalian autophagy is indispensible for fetal hematopoiesis. *Autophagy* 7, 229–230 (2011).
  ^ref-50

51. Wallot-Hieke, N. et al. Systematic analysis of ATG13 domain requirements for autophagy induction. *Autophagy* 14, 743–763 (2018).
  ^ref-51

56. Koike, H. et al. Modelling human hepato-biliary-pancreatic organogenesis from the foregut-midgut boundary. *Nature* 574, 112–116 (2019).
  ^ref-56

---

> 由 paper-to-note skill 生成 | 2026-03-26

# 论文对比矩阵（初始骨架）

> 状态说明：本表当前仅列首轮候选。`待核实` 表示尚未由论文原文、正式页面或官方代码仓库交叉确认，不能据此作最终选择。

| 论文/方法 | 年份/出处 | 研究问题 | 扰动类型 | 预测对象 | 架构/先验 | 数据与划分 | OOD 测试 | 指标 | 官方代码/维护/许可 | 资源与依赖 | 复现难度 | 初步分级 | 核实状态 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [GEARS](https://www.nature.com/articles/s41587-023-01905-6) | 2023 在线/2024 卷期；Nature Biotechnology | 新颖单/多基因扰动表达预测 | CRISPR；单基因和多基因 | 每个细胞的表达向量 | GNN（图神经网络）+ 共表达图 + Gene Ontology 图 | 7 个数据集；Norman 组合数据含 131 个双基因扰动；详细划分待补 | 未见单基因；组合的 0/1/2 个基因未见 | MSE、Pearson、方向性、遗传互作等；细节待补 | [官方代码](https://github.com/snap-stanford/GEARS)；MIT；未归档；最后推送 2025-02-01 | PyTorch Geometric；硬件待核实 | 中等 | A 类 | 论文、代码、许可和维护已核实 |
| [Chreode](https://arxiv.org/abs/2605.28111) | 2026；arXiv 预印本 | 一步时间动态；表示迁移到扰动预测 | 时间变化为主；Norman CRISPR 仅作 GEARS 嵌入迁移 | 潜在空间细胞分布 | 两阶段 scVI 编码器 + DiT 动力学；约 247.7 万细胞预训练 | 7 个小鼠胚胎数据集、88 时间点；下游 Weinreb/Veres/Norman | 时间点外推和迁移；非独立通用 CRISPR 评测 | Sinkhorn W2、MMD、energy distance、DE20 MSE | [代码](https://github.com/mufanq/Chreode)；有[预训练权重](https://huggingface.co/MufanQiu/chreode-pretrained)；最后推送 2026-06-03；**许可证未识别** | 大规模预训练，论文称预训练仅一次 | 很高 | D 类（当前） | 论文、代码、权重和维护已核实；许可待作者明确 |
| [scDFM](https://github.com/AI4Science-WestlakeU/scDFM) | 2026；ICLR 2026 | 稳健的分布级扰动预测 | 具体基因/药物任务待补 | 扰动后完整细胞分布 | Conditional flow matching（条件流匹配） | 数据、划分待补 | 待补 | 分布指标待补 | 官方仓库；MIT；最后推送 2026-04-22；`environment.yml` | 依赖复杂度和硬件待核实 | 高 | B 类 | 论文定位、代码、许可和维护已核实 |
| [Conditional Monge Gap / CMonge](https://www.nature.com/articles/s42256-026-01242-8) | 2026；Nature Machine Intelligence | 跨药物、剂量及组合的条件分布映射 | 药物、剂量、组合 | 单细胞表达/蛋白分布 | Conditional OT（条件最优传输）+ Monge Gap 正则 | SciPlex：3 细胞系、187 化合物、4 剂量；另有 4i 蛋白数据 | 未见药物-剂量条件；已见/未见设置 | 分布指标待补 | [代码](https://github.com/AI4SCR/Conditional-Monge) MIT；最后推送 2026-06-03；PyPI `cmonge` | Python 3.10/3.11；资源待核实；数学门槛高 | 高 | B 类方法阅读，D 类首复现 | 论文、代码、许可、安装、维护已核实 |
| [scGen](https://www.nature.com/articles/s41592-019-0494-8) | 2019；Nature Methods | 跨条件/细胞类型的扰动响应预测 | 药物/疾病等条件；细节待补 | 单细胞表达状态 | VAE（变分自编码器）潜在空间向量算术 | 多个研究；细节待补 | out-of-sample 条件/细胞类型 | 待补 | [代码](https://github.com/theislab/scgen)，GPL-3.0；最后推送 2024-12-05；基于 scvi-tools | 相对较低，但论文旧版与当前实现差异待查 | 低到中 | A 类基础精读 | 正式论文、代码、许可和维护已核实 |
| [CellOT](https://pmc.ncbi.nlm.nih.gov/articles/PMC10630137/) | 2023；Nature Methods | 未配对 control/perturbed 细胞的状态映射 | 基因/药物任务待补 | 细胞分布/传输映射 | Neural optimal transport（神经最优传输）+ 输入凸网络 | 待补 | 待补 | MMD、特征均值 L2/相关性；均值指标会忽略多峰异质性 | [代码](https://github.com/bunnech/cellot)；BSD-3-Clause；最后推送 2024-10-31 | 数学/训练复杂度中高 | 高 | B 类 | 论文、指标局限、代码、许可和维护已核实 |
| [CPA](https://www.embopress.org/doi/full/10.15252/msb.202211517) | 2023；Molecular Systems Biology | 跨药物/剂量/细胞类型及组合的条件响应 | 药物和基因组合 | 条件表达分布/均值 | 条件自编码器 + 可组合扰动嵌入 + 解耦训练 | sci-Plex、Norman 等；细节待补 | 未见剂量/组合/上下文 | R2/DE 等待补 | [代码](https://github.com/theislab/cpa)；BSD-3-Clause；PyPI、测试和教程 | scvi-tools/Ray Tune；中等 | 中 | A/B 类；备用候选 | 论文定位、代码、许可和教程已核实 |
| [PerturbNet](https://pmc.ncbi.nlm.nih.gov/articles/PMC12322087/) | 2025；正式期刊名称待补 | 未见化学、基因及编码突变响应 | 药物、CRISPRi/a、序列突变 | 细胞状态分布 | 扰动表示网络 + cell-state 网络 + conditional invertible NN | sci-Plex、LINCS、Norman 等 | 完全未见扰动 | R2/DE 与分布指标待补 | [代码](https://github.com/welch-lab/PerturbNet)；数据/权重在 Hugging Face；许可/维护待查 | 多组件，资源待查 | 高 | B 类 | 任务、数据/代码入口已核实；许可等待补 |
| [scGPT](https://www.nature.com/articles/s41592-024-02201-0) | 2024；Nature Methods | 通用单细胞基础模型，多下游任务含扰动预测 | 基因扰动等 | 基因/细胞表示与表达预测 | Generative pretrained transformer（生成式预训练 Transformer） | 超过 3,300 万细胞预训练；扰动数据待补 | 下游迁移 | 待补 | [代码](https://github.com/bowang-lab/scGPT)；许可/维护待查 | 预训练复现很重，微调仍复杂 | 很高 | C 类背景，D 类首复现 | 论文、预训练规模和代码入口已核实 |
| [Simple linear/additive baseline study](https://www.nature.com/articles/s41592-025-02772-6) | 2025；Nature Methods | 检验深度/基础模型是否超过简单基线 | 单/双基因扰动 | 平均转录组效应 | no-change、mean、linear、additive 对比 | 具体数据待补 | 未见单/双基因组合 | 扰动效应指标待补 | 代码/许可待核实 | 低 | 低 | **A 类必读评估论文** | 论文结论和 DOI 已核实 |
| [scPerturb](https://www.nature.com/articles/s41592-023-02144-y) | 2023 在线/2024 卷期；Nature Methods | 扰动数据统一、质量分析与实验设计资源 | 多种基因/药物扰动 | 数据资源，不是预测模型 | 统一处理与 E-statistics | 多个公开数据集，RNA 统一 `.h5ad` | 不适用 | E-distance/E-test 等数据分析 | [官方代码](https://github.com/sanderlab/scPerturb)；最后推送 2025-02-25；仓库级许可证未识别 | 处理资源需求待查 | 低到中 | A 类数据必读 | 数据入口、代码和维护已核实；许可待查 |
| [scPerturBench 综合 benchmark](https://www.nature.com/articles/s41592-025-02980-0) | 2025 在线/2026 卷期；Nature Methods | 方法、公平划分、指标和泛化能力比较 | 基因和化学扰动 | 多种预测设定 | 27 方法的统一评测，不是单模型 | 29 数据集；细胞上下文和扰动泛化 | i.i.d./OOD、未见遗传/化学扰动 | 6 个互补指标；另分析 13 指标相关性 | [代码](https://github.com/bm2-lab/scPerturBench)；GPL-3.0；199 commits（查阅时） | 全量 benchmark 很重；可只读和复用单项 | 全量高，阅读低 | **A 类，首轮先读** | 论文/代码/许可已核实 |
| [PerturBench](https://github.com/altoslabs/perturbench) | 2025；NeurIPS Datasets & Benchmarks Track | 标准化数据、模型和指标接口 | 多种扰动 | 统一 benchmark 框架 | Python 包和数据访问器 | 预处理 `.h5ad` 在 Hugging Face | 依任务配置 | 多指标 | 官方仓库；许可类型待点击核实；17 commits（查阅时） | Python 3.11；可按单数据集使用 | 中 | B 类工具 | 会议、安装和数据入口已核实 |

## 后续必须补充的比较维度

单/多基因、基因/药物、单细胞/分布、知识图谱需求、训练/测试数据、精确划分、未见基因/组合、跨细胞类型/数据集、指标局限、仓库最近维护、License（开源许可证）、硬件、改进空间和新手推荐等级。

## 第一轮分级

- **A 类：必须精读并可能复现**
  - 综合 benchmark：先建立任务、划分和指标地图。
  - GEARS：第一篇完整方法精读和主复现候选。
  - 简单线性/加性 baseline 评估论文：决定公平对照。
  - scPerturb：理解数据版本、效应强度和质量。
  - scGen：理解最基础的潜在空间扰动方法。
  - CPA：备用 baseline，重点看组合、剂量和上下文。
- **B 类：重点阅读方法和实验**
  - CellOT、scDFM、CMonge：分布级预测与最优传输/流匹配路线。
  - PerturbNet：完全未见扰动及多种扰动表示。
  - PerturBench：后续评估接口和预处理数据参考。
- **C 类：用于了解研究背景**
  - scGPT 等单细胞基础模型：了解预训练与迁移，不复现预训练。
  - 领域综述和数据库论文：用于论文背景与术语，不作为代码主线。
- **D 类：当前阶段暂不适合**
  - Chreode 完整预训练/复现：数据规模大、两阶段训练、预印本很新、许可证未明确。
  - scDFM/CMonge 的完整首复现、scPerturBench 全量 27 方法复跑、Tahoe-100M 整体下载：均超出首次项目的风险或资源边界。

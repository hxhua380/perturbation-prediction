# 调研发现与决策

## 已确认需求

- 目标是成熟模型的可控增量改进，面向普通期刊、一般 SCI 或 CCF-C。
- 优先公开代码、公开数据、单张 A100 可承受、复现风险较低的路线。
- 先调研和验证，再决定 baseline；先冒烟测试，再完整训练。
- 所有论文、数据、代码和资源信息区分“已核实”“待核实”。

## 当前发现

- 根目录已有 GEARS、Chreode、scDFM 三个 PDF 文件。
- 当前目录不是 Git 仓库，未发现项目代码或既有文档。
- 尚未下载数据、安装环境或运行实验。
- GEARS 正式论文页确认：论文 2023-08-17 在线发表，卷期标为 Nature Biotechnology 42, 927-935 (2024)；作者为 Yusuf Roohani、Kexin Huang、Jure Leskovec。方法结合深度学习和基因关系知识图谱，预测单基因与多基因 CRISPR 扰动后的表达，并测试未见基因/组合。
- GEARS 官方仓库确认：`snap-stanford/GEARS`，安装说明依赖 PyTorch Geometric 并提供 `cell-gears` 包；仓库明确声明不支持跨细胞类型训练/迁移，且只用单基因数据训练时不能可靠预测组合扰动。
- GEARS 论文数据可用性声明给出 GEO accession：Dixit GSE90063、Adamson GSE90546、Norman GSE133344、Jost GSE132080、Tian GSE124703、Replogle GSE146194、Horlbeck GSE116198；另一个 Replogle 数据来自 Figshare DOI `10.25452/figshare.plus.20022944`。
- scGen 正式论文页确认：Mohammad Lotfollahi、F. Alexander Wolf、Fabian J. Theis，Nature Methods 16, 715-721 (2019)，研究跨条件/数据集的 out-of-sample 扰动响应预测。
- CellOT 论文确认其用 neural optimal transport（神经最优传输）学习未配对 control 到 perturbed 细胞状态映射；适合作为分布预测的重要前置方法，数学与实现难度高于 scGen。
- CMonge 正式论文页确认：2026-06-01 发表于 Nature Machine Intelligence。它用单个条件最优传输模型联合药物、剂量和组合，测试已见与未见条件；SciPlex 描述为 3 个细胞系、187 个化合物、4 个剂量。由于非常新，不宜作为首个复现对象。
- scDFM 官方仓库与论文页确认：ICLR 2026，使用 conditional flow matching（条件流匹配）建模扰动后细胞的完整分布；官方安装入口为 `environment.yml`。其新颖性和数学复杂度均高于 GEARS。
- Chreode 当前为 2026-05 的 arXiv 新预印本：预训练使用约 247.7 万个小鼠胚胎细胞、7 个数据集、两阶段 scVI + DiT；其 Norman 结果是把预训练表示替换进 GEARS，而不是一个轻量独立扰动 baseline。预训练仅运行一次，首个复现风险高。
- scPerturb 于 Nature Methods 发表，提供统一的 `.h5ad` 格式 RNA 扰动数据（Zenodo DOI `10.5281/zenodo.7041848`）、公开处理代码和原始来源索引。它适合做数据浏览/小练习，但若复现 GEARS，必须先确认 scPerturb 处理版与 GEARS 官方预处理是否一致，不能直接替换后声称论文复现。
- Broad Single Cell Portal 的 Dixit Perturb-seq 页面显示门户版本为 49,234 个细胞、11,738 个基因；论文摘要描述整个研究分析约 200,000 个细胞，说明“论文总规模”和“某个下载对象规模”可能不同，注册表必须注明版本。
- Tahoe-100M 官方 Hugging Face 数据集页确认：Parquet 格式、CC0-1.0、仓库总量约 429 GB。即使服务器有 A100，首次项目也不应整体下载；后期若需要只能先研究分片/过滤版。
- sci-Plex 原始数据入口为 GEO GSE139944；CMonge 论文使用的 SciPlex 条件为 3 个细胞系、187 个化合物、4 个剂量。其他工作给出的过滤后细胞/基因规模不能和原始 GEO 总量混写。
- 2026 年 Nature Methods 正式 benchmark（2025-12 在线发表）比较 27 种方法、29 个数据集、6 个互补指标，并分别评估细胞上下文泛化与未见扰动泛化。其公开代码仓库 `bm2-lab/scPerturBench` 使用 GPL-3.0，包含 199 次提交、结果与数据校验文件。
- 该 benchmark 明确列出 MSE、PCC-delta、E-distance、Wasserstein、KL divergence 和 Common-DEGs。多项指标彼此相关，单独看绝对表达相关性或均值误差会掩盖扰动效应与分布异质性。
- scArchon 的独立 benchmark 报告：近一半工具按常用指标与简单常数效应线性 baseline 相当或更差；降维图不能替代定量评估；全局指标好不代表差异表达基因或生物通路恢复好。这支持保留 no-perturb、mean-shift/linear 等简单基线。
- Altos Labs 的 PerturBench 是另一套标准化框架，2025 NeurIPS Datasets and Benchmarks Track，提供 Python 3.11 安装说明和 Hugging Face 预处理 `.h5ad` 数据入口。名称与 `scPerturBench` 相近，但不是同一个项目，后续文档必须区分。
- scGen 官方仓库为 `theislab/scgen`，当前基于 scvi-tools，目标是跨细胞类型、研究和物种预测扰动响应；旧论文概念简单，但实际复现要区分旧版论文代码、当前包和 `scgen-reproducibility` 仓库。
- CellOT 官方仓库为 `bunnech/cellot`；CMonge 官方代码为 `AI4SCR/Conditional-Monge`，MIT 许可，可用 Python 3.10/3.11 并发布为 `cmonge`。CMonge 预处理 SciPlex3/4i 有永久 DOI，降低数据准备风险，但模型和论文太新、最优传输门槛较高。
- Chreode 代码定位到 `mufanq/Chreode`，预训练权重在 Hugging Face `MufanQiu/chreode-pretrained`。有权重不等于易复现：其预训练数据、两阶段模型、下游迁移和资源仍明显超出首次复现范围。
- 2026-06-22 通过 GitHub 官方 API 核实仓库状态（`pushed_at` 代表最后代码推送，`updated_at` 可能仅因 star/issue 等变化，不能当维护日期）：GEARS 2025-02-01、MIT、未归档；scDFM 2026-04-22、MIT；scGen 2024-12-05、GPL-3.0；CellOT 2024-10-31、BSD-3-Clause；CMonge 2026-06-03、MIT；Chreode 2026-06-03、未识别到许可证；scPerturb 2025-02-25、未识别到仓库级许可证。许可证未识别时不得默认可自由复用。
- CPA（Compositional Perturbation Autoencoder，组合扰动自编码器）发表于 Molecular Systems Biology 2023。它把细胞类型、药物、剂量和组合等条件编码到可组合潜在表示中；官方 `theislab/cpa` 仓库为 BSD-3-Clause，包含测试、教程、PyPI 安装和组合 CRISPR 示例。与 GEARS 相比，CPA 的任务覆盖更广，但针对未见基因的生物先验较弱。
- PerturbNet（2025）同时处理化学、CRISPRi/a 和编码序列突变，并提供官方代码、处理数据和权重。其处理版 sci-Plex 为 648,857 个细胞、5,087 个基因、180 个保留药物；这是作者过滤后的版本，不是 GEO 原始总量。
- scGPT 是在超过 3,300 万细胞上预训练的单细胞基础模型，扰动预测只是多个下游任务之一。它对理解基础模型有价值，但近年 benchmark 显示基础模型并不自动胜过简单线性/加性基线，因此不适合本项目第一个复现对象。
- Ahlmann-Eltze、Huber、Anders 的 2025 Nature Methods 工作直接比较 5 个基础模型和 2 个其他深度模型与简单基线：对于已见单基因、未见双基因组合的设定，深度模型未优于简单加性模型。该结论不是“深度学习永远无效”，而是要求明确任务、强简单基线和扰动效应指标。

## 技术决策

| 决策 | 理由 |
|---|---|
| 注册表使用 Markdown 表格并附核实状态 | 便于新手阅读，同时避免把未验证信息写成事实 |
| 研究路线按“调研→精读/代码审计→冒烟→复现→改进”推进 | 每一步都有可验证产物，失败成本可控 |

## 问题与处理

| 问题 | 处理 |
|---|---|
| 文件系统沙箱辅助程序缺失 | 使用已批准的只读权限完成目录审计 |
| 当前无 Git 元数据 | 暂不执行 Git 分支操作，等待后续明确初始化/远程信息 |
| Web 工具不允许直接打开 GitHub API URL | 记录失败；改用官方仓库页面/搜索结果核实，必要时后续通过只读命令查询 |
| 首次 PowerShell GitHub API 汇总命令出现空管道语法错误 | 把 `foreach` 输出先赋给 `$rows`，再传给 `Format-Table`；第二次成功 |

## 资源

- 本地论文目录：`article/`
- 论文矩阵：`literature_matrix.md`
- 数据注册表：`dataset_registry.md`
- baseline 注册表：`baseline_registry.md`
- GEARS 论文：https://www.nature.com/articles/s41587-023-01905-6
- GEARS 官方代码：https://github.com/snap-stanford/GEARS
- scGen 论文：https://www.nature.com/articles/s41592-019-0494-8
- CellOT 全文：https://pmc.ncbi.nlm.nih.gov/articles/PMC10630137/
- CMonge 论文：https://www.nature.com/articles/s42256-026-01242-8
- scDFM 官方代码：https://github.com/AI4Science-WestlakeU/scDFM
- Chreode 预印本：https://arxiv.org/abs/2605.28111
- scPerturb 论文：https://www.nature.com/articles/s41592-023-02144-y
- scPerturb RNA 数据：https://doi.org/10.5281/zenodo.7041848
- Norman GEO：https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE133344
- sci-Plex GEO：https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE139944
- Tahoe-100M：https://huggingface.co/datasets/tahoebio/Tahoe-100M
- 综合 benchmark 论文：https://www.nature.com/articles/s41592-025-02980-0
- 综合 benchmark 代码：https://github.com/bm2-lab/scPerturBench
- PerturBench 框架：https://github.com/altoslabs/perturbench
- scGen 代码：https://github.com/theislab/scgen
- CellOT 代码：https://github.com/bunnech/cellot
- CMonge 代码：https://github.com/AI4SCR/Conditional-Monge
- Chreode 代码：https://github.com/mufanq/Chreode
- Chreode 权重：https://huggingface.co/MufanQiu/chreode-pretrained
- CPA 代码：https://github.com/theislab/cpa
- PerturbNet 全文：https://pmc.ncbi.nlm.nih.gov/articles/PMC12322087/
- PerturbNet 代码：https://github.com/welch-lab/PerturbNet
- scGPT 论文：https://www.nature.com/articles/s41592-024-02201-0
- scGPT 代码：https://github.com/bowang-lab/scGPT
- 简单基线评估论文：https://www.nature.com/articles/s41592-025-02772-6

## 浏览/PDF 发现

- 第一轮网页检索优先使用 Nature 正式论文页、PMC 全文、arXiv 论文页和作者官方 GitHub。搜索摘要只用于定位来源，表中具体事实尽量回到一手页面核实。

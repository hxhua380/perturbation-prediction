# 数据集注册表（初始骨架）

> 未确认磁盘空间、许可和官方/可信下载地址前，不下载大型数据。规模字段必须区分原始版、过滤版和模型预处理版。

| 数据集 | 来源论文 | 扰动/细胞系统 | 规模（细胞/基因/扰动） | 组合/对照 | 格式与下载 | 大小/许可/申请 | 预处理版本与使用模型 | 泄漏风险 | 建议用途 | 核实状态 |
|---|---|---|---|---|---|---|---|---|---|---|
| [Norman 组合 CRISPR](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE133344) | Norman et al., 2019；GSE133344 | CRISPRa 组合扰动；K562 待从原文再次确认 | GEARS 评测含 131 个双基因扰动；细胞/基因数和条件总数待按版本核实 | 0/1/2 基因；对照标签待查 | GEO；GEARS/其他预处理入口待查 | 大小、原始数据许可待查 | GEARS、PerturbNet 等；scPerturb 有统一 `.h5ad` | 随机拆分会让测试组合中的单基因效应泄漏；必须记录 0/1/2 unseen 规则 | **首次 GEARS 冒烟候选**，优先官方预处理小子集 | GEO accession、组合任务已核实；规模待查 |
| [Adamson Perturb-seq](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE90546) | Adamson et al., 2016；GSE90546 | CRISPR；内质网应激系统 | 含 pilot、主实验和 epistasis 子数据；精确版本规模待查 | 部分实验含双/三重扰动；对照待查 | GEO；scPerturb 统一 `.h5ad` | 大小/许可待查 | GEARS、scPerturb | 子实验和处理条件混用；预处理版本差异 | 基础/外部测试候选，不是首个组合主集 | 来源和任务已核实；规模待查 |
| [Dixit Perturb-seq](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE90063) | Dixit et al., 2016；GSE90063 | CRISPR；免疫细胞和细胞系 | Broad 门户下载对象：49,234 细胞、11,738 基因；论文总分析约 200,000 细胞 | 有对照/多实验，细节待查 | GEO、Broad SCP24、scPerturb `.h5ad` | 大小/许可待查 | GEARS、scPerturb | 门户子集与论文总规模不同；批次/扰动标签处理 | 小型数据理解或外测候选 | 门户规模与来源已核实；版本关系待查 |
| Replogle CRISPR 数据 | Replogle et al.；GSE146194、Figshare DOI `10.25452/figshare.plus.20022944`，另有 gwps.wi.mit.edu 处理版 | 大规模 CRISPR；RPE-1/K562 等待按版本拆分 | GEARS 文中两个筛选分别 1,543 和 1,092 个扰动、各超过 170,000 细胞；其他版本待查 | 以单基因为主；对照待查 | GEO/Figshare/项目站点 | 大小/许可待查 | GEARS、scPerturb | 同一作者多套数据和处理版易混淆 | 完整单基因 OOD 复现候选，非首次下载 | GEARS 文中规模与入口已核实；版本映射待查 |
| [LINCS L1000](https://clue.io/) | LINCS/CMap；正式数据门户待继续核实 | 药物/基因；主要为群体表达签名，不是标准单细胞 RNA-seq | 待核实 | 有对照和多剂量/时间；细节待查 | CLUE/LINCS | 访问、大小和许可待查 | CPA/药物模型待查 | 测量与推断基因、bulk 与单细胞任务混用 | 背景/药物对照，不作为首次单细胞主集 | 仅任务性质初步核实 |
| [sci-Plex](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE139944) | Srivatsan et al., Science 2020；GSE139944 | 药物、剂量、多细胞系 | CMonge 使用 3 细胞系、187 化合物、4 剂量；PerturbNet 过滤版为 648,857 细胞、5,087 基因、180 药物 | 含对照；组合药物是否在此版本中待查 | GEO；scPerturb `.h5ad`；CMonge/PerturbNet 各有处理版 | 大小/原始许可待查 | CMonge、PerturbNet、CPA 等 | 药物、剂量、细胞系和批次混淆；不同作者过滤版不可混用 | 后续药物/分布预测候选 | 条件和 PerturbNet 处理版规模已核实；原始规模待查 |
| [Tahoe-100M](https://huggingface.co/datasets/tahoebio/Tahoe-100M) | Tahoe Bio 数据集论文待核实 | 大规模药物单细胞数据 | 名称指向约 1 亿细胞；官方仓库总量 429 GB；基因/药物/细胞系待查 | 对照和条件结构待查 | Parquet；Hugging Face | 429 GB；CC0-1.0；无需申请状态待确认 | State/Tahoe 等新模型待查 | 规模大，切分、重复细胞系和条件泄漏风险 | **后期扩展；不适合第一次练习或整体下载** | 格式、仓库大小、许可已核实 |
| [scPerturb RNA 集合](https://doi.org/10.5281/zenodo.7041848) | Peidli et al., Nature Methods 2024 卷期 | 多种遗传/药物扰动的统一集合 | 多数据集；每个数据集规模见其元数据 | 依数据集而异 | 统一 `.h5ad`；Zenodo | 大小/许可需逐数据集核查 | 数据浏览和 benchmark 资源 | 统一处理版可能与模型官方预处理不同 | **首次数据结构练习候选**，不自动等同论文复现数据 | 格式、入口和处理代码已核实 |

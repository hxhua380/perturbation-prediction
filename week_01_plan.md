# 第一周学习与研究计划

> 每天建议 60-120 分钟。本周不安装论文环境、不下载大型数据、不训练模型。

## Day 1：建立领域地图

- 阅读综合 benchmark 的摘要、图 1 和任务定义。
- 在 `glossary.md` 复习 Perturbation、Baseline、OOD、Embedding、Smoke test。
- 完成检查：能用自己的话区分“未见扰动”和“跨细胞类型”。

## Day 2：理解单细胞数据输入输出

- 学习“细胞 × 基因”表达矩阵、`adata.X`、`adata.obs`、`adata.var` 的概念。
- 对照 GEARS README 记录：`condition`、`cell_type`、`gene_name` 分别放在哪里。
- 不需要读取实际数据文件。

## Day 3：GEARS 的问题与数据划分

- 阅读摘要、引言、问题定义和 Norman 组合评测。
- 画一张纸面数据流：control 表达 + perturbation set → predicted expression。
- 解释 0/1/2 unseen，不看模型公式。

## Day 4：GEARS 模型直觉

- 阅读图 1 和方法概览。
- 只掌握：基因嵌入、扰动嵌入、两个关系图、组合算子、输出表达。
- 记录每个主要张量“可能是哪几个维度”，暂不要求精确代码 shape。

## Day 5：官方代码只读审计

- 只浏览仓库目录、README、`requirements.txt`、数据类和模型入口。
- 记录程序入口、下载行为、数据目录和最小 API；不 clone、不安装、不执行 loader。
- 目标产物：首篇代码阅读笔记，而不是运行结果。

## Day 6：指标和简单基线

- 阅读简单线性基线论文的摘要、设定和主要结论。
- 比较 MSE、PCC-delta、Common-DEGs、E-distance 各自在测什么。
- 回答：为什么 no-change baseline 可能在绝对表达指标上表现不差？

## Day 7：一页总结与下一阶段确认

- 用不超过一页总结 GEARS 的任务、输入、输出、数据划分、指标和已知限制。
- 对照 `baseline_registry.md` 检查主/备用/简化候选是否仍合理。
- 下一周再决定是否初始化 Git 并开始代码仓库只读审计；仍不自动进入训练。

## 第一周完成标准

- [ ] 能解释单细胞扰动预测的输入和输出。
- [ ] 能区分随机细胞拆分、未见基因、未见组合和跨细胞类型。
- [ ] 能说明 GEARS 为什么使用基因关系图。
- [ ] 能说明至少两种常用指标的盲点。
- [ ] 能说明为什么必须保留简单基线。
- [ ] 没有下载大型数据、安装环境或声称复现成功。


# 第一轮论文精读顺序

## 结论

先读 benchmark 的指定章节建立“任务、划分、指标”地图；第一篇完整精读的方法论文是 GEARS。不是从最新模型开始，因为新方法通常同时引入更复杂的数学、数据和训练流程，会把“没理解任务”和“代码没跑通”混成一个问题。

## 推荐顺序

1. **A 类：Benchmarking algorithms for generalizable single-cell perturbation response prediction**
   - 只先读摘要、图 1、任务划分、6 个指标和结论，不要求通读 27 个方法。
   - 目标：知道不同论文为什么不能直接横向比较。
2. **A 类：GEARS**
   - 第一篇完整精读、第一候选复现论文。
   - 顺序：问题定义 → Norman 数据与 0/1/2 unseen 划分 → 指标 → 图 1 模型 → 损失和实现。
3. **A 类：Deep-learning-based gene perturbation effect prediction does not yet outperform simple linear baselines**
   - 学会为什么必须包含 no-change、mean、linear 和 additive baseline。
4. **A 类：scPerturb**
   - 重点读数据组织、质量、效应强度和实验设计；它是数据资源，不是预测模型。
5. **A 类基础：scGen**
   - 用于理解 VAE（变分自编码器）和潜在空间扰动向量；概念简单，但旧版复现不是当前主任务。
6. **A/B 类：CPA**
   - 重点读条件、剂量、组合、细胞上下文的可组合表示；当前备用 baseline 候选。
7. **B 类：CellOT**
   - 在理解“均值预测不能保留异质性”后，学习未配对分布映射和最优传输直觉。
8. **B 类：scDFM**
   - 在掌握概率分布、生成模型和 flow matching（流匹配）直觉后阅读；暂不首复现。
9. **B 类：Conditional Monge Gap / CMonge**
   - 在掌握 Wasserstein 距离、Sinkhorn 和条件最优传输后阅读；重点看未见药物/剂量。
10. **C/D 类：scGPT、PerturbNet、Chreode**
    - scGPT 用于了解基础模型；PerturbNet 用于了解统一扰动表示；Chreode 放在 GEARS、scVI、分布距离和时间动态之后。

## 三篇新论文放在什么阶段

- **scDFM**：GEARS 复现后、准备研究分布级预测或不确定性时精读。先读方法和指标，不急着复现。
- **Conditional Monge Gap**：完成 CellOT/最优传输基础后，作为药物、剂量和未见条件泛化的重点阅读；不作为首个代码对象。
- **Chreode**：完成 GEARS 代码理解并学过 scVI、时间动态和分布距离后再读。它的大规模预训练和 GEARS 嵌入迁移适合后期研究灵感，不适合入门复现。

## GEARS 前必须补的最小知识

1. 单细胞表达矩阵：行通常是细胞，列通常是基因；理解 count、归一化和 log1p 的目的。
2. control（对照）与 perturbed（扰动后）细胞，以及 Perturb-seq 标签如何连接到细胞。
3. 监督学习、训练/验证/测试集、数据泄漏和 OOD 划分。
4. 向量、矩阵、批次和 Tensor shape（张量形状）。
5. MSE（均方误差）、Pearson correlation（皮尔逊相关系数）和 Differentially expressed genes（差异表达基因）的直觉。
6. Embedding（嵌入表示）、graph（图）、node（节点）、edge（边）和 GNN（图神经网络）的直觉。

## 可以在复现过程中再学

- PyTorch 自动求导和优化器的细节。
- PyTorch Geometric 的消息传递实现。
- Gene Ontology 图和共表达图的具体构造。
- GEARS 的 direction-aware loss、遗传互作分类和不确定性模块。
- VAE、optimal transport、flow matching 和 DiT 的完整数学推导；这些不是跑通 GEARS 的前置条件。

## 本轮检查问题

1. 为什么“随机拆细胞”不一定等于“未见扰动泛化”？
2. 为什么只看所有基因的 Pearson 相关性可能高估模型？
3. GEARS 组合测试中的 0/1/2 unseen 分别表示什么？


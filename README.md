# AIVC 单细胞扰动预测研究项目

本项目面向 Single-cell perturbation prediction（单细胞扰动预测）：从未处理细胞状态和基因/药物等扰动条件，预测处理后的基因表达状态或表达分布。

当前处于调研和项目初始化阶段，尚未确定最终 baseline，未下载数据，未安装论文环境，也未开始训练。

## 文档导航

- `memory.md`：长期背景、约束和当前状态
- `research_plan.md`：研究路线图
- `literature_matrix.md`：论文对比矩阵
- `dataset_registry.md`：数据集注册表
- `baseline_registry.md`：候选 baseline 注册表
- `glossary.md`：术语表
- `environment.md`：计算环境
- `experiment_log.md`：实验日志
- `decision_log.md`：决策日志
- `results/README.md`：结果索引
- `reading_notes/00_reading_order.md`：第一轮精读顺序
- `week_01_plan.md`：第一周可执行计划
- `projects/README.md`：不同论文代码复现的统一目录规范

## 当前原则

先核实来源和任务定义，再选 baseline；先运行小规模冒烟测试，再完整训练；代码无报错不等于复现成功。

## 第一轮阶段性选择

- 主候选：GEARS
- 备用候选：CPA
- 必要简化基线：no-perturb、mean-shift/linear、additive
- 第一次正式冒烟数据：GEARS 官方预处理 Norman 的小子集（当前尚未下载）

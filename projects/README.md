# 论文代码复现目录

每篇论文或模型使用一个独立子目录：

```text
projects/
└─ <model_slug>/
   ├─ README.md
   ├─ upstream_info.md
   ├─ configs/
   ├─ scripts/
   ├─ tests/
   └─ upstream/
```

## 目录职责

- `README.md`：该论文的复现目标、入口、数据流、验证标准和当前状态。
- `upstream_info.md`：官方仓库 URL、固定 commit hash、论文版本、License（开源许可证）和本地修改说明。
- `configs/`：实验配置和随机种子。
- `scripts/`：数据检查、训练、评估等可重复脚本。
- `tests/`：CPU 最小测试和关键函数测试。
- `upstream/`：官方代码工作副本；默认不纳入主仓库，避免误提交嵌套 Git 仓库。

## 规则

1. 目录名使用简短小写名称，例如 `gears`、`cpa`、`scdfm`。
2. 每篇论文使用独立 Python/Conda 环境，不在同一环境里强行兼容所有依赖。
3. 不直接在 `projects/` 中执行普通 `git clone` 后再把嵌套仓库提交到主仓库。
4. 开始复现前必须记录官方 URL、commit hash 和许可证。
5. 修改原方法时保留原始 baseline；自定义修改放在独立分支、补丁或明确标注的文件中。
6. 数据、权重、缓存和大型输出不进入 GitHub。
7. 若后续确实需要同步完整官方源码，再单独决定采用固定版本复制、Git submodule（Git 子模块）或个人 fork；不要临时混用。

当前尚未下载或放入任何论文代码。


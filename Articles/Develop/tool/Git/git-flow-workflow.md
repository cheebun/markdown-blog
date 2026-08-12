# git flow 工作流

从 `master` 开发至 `1.0.0`。

开新分支 `qa`、`sim` 分支。

如果有新需求, 从 `master` 开 `feature/<CODE>` 分支, 开发完毕后。

合并到 `qa` 测试, 测试完成后。

合并到 `sim` 仿真环境测试。

完毕后, 由 `sim` 合并到 `master`。


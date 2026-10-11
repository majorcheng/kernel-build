# xanmod6.18 workflow

## 计划

- 对照上游 `v3` 的 `.github/workflows/xanmod6.18.yml` 最新修改。
- 保留本仓库实际存在的 `config.sh`，迁移 LLVM、构建参数、依赖和 Release 说明改进。
- 保留本地 Release 清理步骤；上游对应的统一 `clean-releases.yml` 不在本次范围内。
- 校验 YAML、脚本引用、工作区差异和 Git 状态。

## 完成标准

- 目标 workflow 可解析，配置脚本路径有效，构建参数在三个内核构建步骤中一致。
- 只包含本任务需要的文件改动，并记录未覆盖的真实 Actions 运行风险。

## 验证结果

- 上游目标分支：`0d4dacde1746…`；目标文件最近相关提交：`4aa828452351…`。
- PyYAML 解析通过，13 个 `run` 块均通过 `bash -n`，`git diff --check` 通过。

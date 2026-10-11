# xanmod6.18 workflow

## 计划

- 对照上游 `v3` 的 `.github/workflows/xanmod6.18.yml` 最新修改。
- 保留本仓库实际存在的 `config.sh`，迁移 LLVM、构建参数、依赖和 Release 说明改进。
- 保留本地 Release 清理步骤；上游对应的统一 `clean-releases.yml` 不在本次范围内。
- 在 `config.sh` 中恢复云服务器需要的 perf/tracing/BPF、容器、namespace、KVM、BBR/fq、XDP 和 netfilter 能力。
- 保留 systemd 需要的 `autofs4` 内核模块。
- 校验 YAML、脚本引用、工作区差异和 Git 状态。

## 完成标准

- 目标 workflow 可解析，配置脚本路径有效，构建参数在三个内核构建步骤中一致。
- `config.sh` 明确设置 HZ 250、BBR、fq，并保留常见容器和网络能力。
- 只包含本任务需要的文件改动，并记录未覆盖的真实 Actions 运行风险。

## 验证结果

- 上游目标分支：`0d4dacde1746…`；目标文件最近相关提交：`4aa828452351…`。
- PyYAML 解析通过，13 个 `run` 块均通过 `bash -n`，`git diff --check` 通过。
- 新增配置块的 220 个符号均存在于上游 `config-6.x.sh`；Linux v6.18 原生 `scripts/config` 干跑通过，XanMod 6.18 基线的关键目标值检查通过。
- 未执行完整 `make olddefconfig` 或内核编译；当前验证覆盖脚本语法、命令执行和目标值写入。
- `CONFIG_AUTOFS_FS=m` 的脚本执行结果已单独核对。

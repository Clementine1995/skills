# DEV_WORKFLOW.md

## 职责

本文件是初始化、构建、启动、验证、Git、数据库、环境晋级、部署和发布后检查的唯一可执行命令来源。

授权边界见 `AGENTS.md`，协作和证据见 `AI_COLLABORATION.md`，环境身份摘要见 `README.md`。

`docs/` 下的需求、设计和阶段材料只能引用本文件章节，不得替代本文件命令、根目录当前事实说明或执行前现场核查。

## 模板使用安全

- 本文件中的 `{{...}}` 是不可执行占位符。实例化前禁止复制运行任何未完全替换的命令块。
- 按实际操作系统、Shell、版本控制、部署方式和环境数量重写命令；不适用章节整段删除。
- 每个命令块必须写明工作目录、目标环境、前置条件、状态影响和成功判定。
- 敏感值只通过项目批准的密钥管理或进程注入方式传递，不写入仓库、命令行历史或日志。
- 命令变化只修改本文件；需求文档、README 和聊天只引用章节名，不复制命令。

## 环境身份门禁

每个允许修改、运行、真实联调或发布的环境或资源边界都必须提供“实际身份校验”，不能只检查分支名或配置文件存在。没有外部资源的单机工具可把门禁收敛为工作区、构建目标和测试配置检查。

身份校验至少覆盖适用项：

- 当前工作区、代码提交或制品摘要。
- 实际加载的配置来源和环境标识。
- 数据库或存储的环境边界。
- 外部接口、消息系统、模型或第三方账号的环境边界。
- 写入开关、端口、代理或危险功能开关。
- 输出只含非敏感摘要。

### {{environment_name_1}} 身份门禁

影响：只读校验，不改变服务、配置或数据。

```text
{{environment_identity_gate_commands_1}}
```

通过标准：{{environment_identity_gate_success_1}}

### {{environment_name_2}} 身份门禁

影响：只读校验，不改变服务、配置或数据。

```text
{{environment_identity_gate_commands_2}}
```

通过标准：{{environment_identity_gate_success_2}}

按实际环境增删本节，不保留空壳。

## 初始化与构建

### 前置检查

工作目录：`{{development_workspace}}`

```text
{{prerequisite_check_commands}}
```

### 初始化运行时

影响：{{runtime_initialization_impact}}

```text
{{runtime_initialization_commands}}
```

### 安装依赖

影响：会修改本地依赖目录或锁文件；未经用户授权不得执行安装、升级或移除依赖。

```text
{{dependency_install_commands}}
```

成功标准：{{dependency_install_success}}

### 构建

影响：{{build_impact}}

```text
{{build_commands}}
```

成功标准：{{build_success}}

没有独立构建步骤时删除本节。

## 本地运行、调用或开发服务

按项目类型保留命令行运行、库调用、批处理或长驻服务小节。启动、停止或重启有状态进程前先通过对应身份门禁。

### 最小运行、调用或启动

工作目录：`{{development_workspace}}`

影响：{{local_run_or_start_impact}}

```text
{{local_run_invoke_or_start_commands}}
```

### 停止或重启

影响：会改变本地服务状态；只有当前任务需要且已说明影响时执行。

```text
{{local_stop_or_restart_commands}}
```

没有长驻服务时删除本节。

### Smoke、自检或健康与身份检查

```text
{{local_smoke_selfcheck_or_health_commands}}
```

通过标准：

- 运行、自检或健康状态：`{{expected_run_or_health_status}}`。
- 环境身份：`{{expected_environment_identity}}`。
- 代码或制品身份：`{{expected_code_identity_rule}}`。

长驻服务已运行或本轮发生重启时，只有健康检查明确返回正确身份后才能继续真实联调。命令行、库或批处理项目按其可观察结果和资源身份定义等价门禁。

必须明确状态、健康或自检入口是只读观测，还是会启动、重启、修复进程或改变业务状态。具备操作副作用的入口不得伪装成健康检查，必须单列命令、影响、授权和成功标准。

## 自动化验证

自动化测试必须使用 `{{automated_test_environment_or_config}}`，隔离策略为 `{{automated_test_isolation_policy}}`。

除非本节显式定义了隔离的集成环境、资源身份和授权，自动化验证不得连接、创建、启动、重启或清空真实数据库、消息 Broker、缓存、对象存储或其他外部基础设施；对应 client 使用替身、Mock transport 或进程内测试实现。

### 定向测试

```text
{{targeted_test_commands}}
```

### 相关回归

```text
{{related_regression_commands}}
```

### 全量测试

```text
{{full_test_commands}}
```

### 静态检查、类型检查和格式检查

```text
{{static_type_format_check_commands}}
```

### 构建或打包验证

仅在改动影响依赖、编译、基础镜像、打包或运行时环境时执行；常规业务改动不机械运行高成本无关验证。

```text
{{package_or_image_validation_commands}}
```

### 差异完整性

```text
git diff --check
{{additional_diff_integrity_commands}}
```

需求文档必须为每个实施单元选择与风险匹配的验证层级，不得用历史测试数字替代当前提交验证。

## Git 与版本控制基线

项目不使用 Git 时，替换为实际版本控制流程并删除 Git 专属命令。

- 未经用户明确授权，不执行 `git add`、`git commit`、`git push` 或 `git pull`。
- 远端同步策略：`{{remote_sync_strategy}}`。
- 历史集成与恢复策略：`{{git_history_integration_and_recovery_policy}}`。实例化前默认不 rebase 共享代码线、不强推，也不使用回滚分支指针或文件内容的命令擅自修复流程错误。
- 只暂存当前任务文件；保留任务开始前已有的未提交修改。

### 开发前只读检查

工作目录：`{{development_workspace}}`

```text
git status --short --branch
git rev-parse --abbrev-ref HEAD
git diff --name-only
{{additional_pre_change_readonly_checks}}
```

必须确认：

- 当前工作区和开发代码线符合 `README.md`。
- 不存在未完成合并或其他版本控制操作。
- 用户已有修改已识别，且不会被覆盖、暂存或混入。
- 本任务修改范围与已有修改重叠时先停止说明。

### 开发前同步

该步骤会更新远端引用或合并代码，准备修改代码前按项目策略执行；纯只读任务不执行。命令必须使用明确的远端和代码线，不使用含糊的 `git pull`。

```text
{{pre_development_sync_commands}}
```

同步策略必须明确：

- 当前开发线如何对齐其远端基线。
- 是否存在已发布修复回流；没有则明确“不适用”。
- 允许和禁止的合并方向。
- 冲突、非快进、未提交重叠或身份门禁失败时的停止条件。

同步完成后立即执行开发环境身份门禁。同步使代码或配置变化时，以新的基线重新规划和验证。

### 提交前检查

```text
git status --short --branch
{{targeted_or_full_validation_commands_for_commit}}
{{static_checks_for_commit}}
git diff --check
git diff
```

### 提交与推送

影响：改变本地历史和远端代码线，必须分别处于用户明确授权范围。

```text
git add {{current_task_files_only}}
git commit -m "{{commit_message}}"
git push {{remote_name}} {{source_branch}}
```

没有冲突或没有待提交修改时，不额外执行空提交或无意义 merge commit。

## 数据库结构和数据变更

项目没有数据库时删除本节。

客户端或嵌入式数据库如果只随应用制品升级，应把 schema、migration、升级/降级和破坏性重建策略作为代码与测试管理，并删除面向远端数据库的环境写入步骤；不要把设备本地迁移误写成远端运维操作。

### 结构变更策略

唯一入口：`{{schema_change_entry}}`

禁止入口：`{{forbidden_schema_change_entries}}`

固定顺序：

1. 形成唯一最终 Schema、DDL 或迁移，并同步代码模型和结构测试。
2. 说明环境、库名、目标对象、锁表或停机风险和完整命令，按 `{{schema_change_authorization_model}}` 取得逐次授权或命中受保护迁移流水线的预授权条件。
3. 执行 `{{schema_preflight_commands}}`。
4. 执行经确认的 `{{schema_apply_commands}}`。
5. 使用 `{{schema_readback_commands}}` 只读回查字段、约束、索引和版本身份。
6. 数据库、代码模型、结构测试或文档不一致时停止后续发布。

### 数据修复或回填

固定顺序：

1. 用 `{{data_scope_query_commands}}` 只读确认筛选范围和预计行数。
2. 提供最终写入语句、幂等性、批量边界、失败停止条件和回查 SQL，取得单独授权。
3. 执行 `{{data_change_commands}}`。
4. 用 `{{data_readback_commands}}` 只读验收。
5. 保存环境、时间、执行者、影响量和证据；不得把非生产授权扩展到线上环境。

不允许在未知现场直接运行通用“回滚脚本”。失败后先保护现场并只读核对，再由人工批准恢复方案。

## CI/CD 与自动化执行

没有 CI/CD 时删除本节。CI runner、构建机和自动化任务是执行上下文，不自动等同于独立运行环境；只有使用不同配置、数据或外部资源时才按环境管理。

- CI 配置入口：`{{ci_configuration_entry}}`。
- 触发条件：{{ci_triggers}}。
- 固定运行时与依赖：{{ci_runtime_and_dependency_locking}}。
- 权限和密钥边界：{{ci_permissions_and_secret_policy}}。
- 缓存和生成物规则：{{ci_cache_and_artifact_policy}}。
- 必需检查与分支保护：{{ci_required_checks_and_branch_protection}}。
- 发布授权模型：{{release_authorization_model}}。

CI 必须调用与本地等价的稳定入口，不在流水线中复制另一套隐式构建或测试逻辑：

```text
{{ci_validation_commands_or_workflow_jobs}}
```

如果 CD 自动执行环境晋级，后续各发布章节中的“命令”可实例化为流水线触发、审批和只读查询入口；自动化不得绕过身份一致性、环境配置门禁、授权、异常现场核查或证据要求。

## 发布身份模型

没有多环境发布的项目可删除本节及后续发布章节。

本项目使用以下通用身份，实例化时映射为 Git SHA、镜像 digest、包校验和或发布系统的不可变 ID：

- `validated_source_identity`：通过发布前完整验证的源代码或制品身份。
- `tested_source_identity`：在前置验证环境完成业务验收的同一身份。
- `target_release_identity`：目标环境实际部署的代码或制品身份。

硬规则：

- `tested_source_identity` 必须来源于 `validated_source_identity`，且二者按项目定义完全一致或具备可验证的不可变映射。
- 最终环境发布前，当前源身份必须仍等于 `tested_source_identity`。
- 源代码、构建依赖、构建参数和版本化发布配置变化会产生新身份；原验收失效。环境级运行配置与密钥不要求跨环境相同，但必须分别通过身份门禁并受变更控制。
- 中间环境代码线不得隐式成为最终环境来源；若采用制品逐级晋升，必须验证同一制品摘要。

## 发布前源基线门禁

每次准备进入新的受控发布目标前都重新执行，不复用开发前同步结果。

工作目录：`{{source_release_workspace}}`

```text
{{pre_release_source_sync_commands}}
{{source_environment_identity_gate_commands}}
{{release_validation_commands}}
{{emit_validated_source_identity_commands}}
```

通过标准：

- 工作区或源制品状态干净且身份明确。
- 本地源与权威远端或制品仓库一致。
- 按项目策略需要回流的已发布修复已经进入源线；不需要时明确删除该步骤。
- 源环境实际配置身份正确。
- 定向、回归、全量、静态和打包验证按风险通过。
- 输出完整 `validated_source_identity`。

门禁导致源代码、构建依赖、构建参数、版本化发布配置或制品变化时，停止发布；先完成源线修正、验证和授权提交，再从头执行本门禁。

## 前置验证环境发布

没有独立验证环境时删除本节，并在需求文档说明由何种等价门禁承担验收。

环境：`{{verification_environment_name}}`

工作目录或制品入口：`{{verification_release_entry}}`

前置条件：已取得 `validated_source_identity`，并满足该环境的逐次授权或受保护流水线预授权条件。

```text
{{verification_target_align_commands}}
{{verification_target_promote_commands}}
{{verification_environment_identity_gate_commands}}
{{verification_deploy_commands}}
{{verification_post_deploy_check_commands}}
```

验收完成后记录：

```text
validated_source_identity={{validated_source_identity_value}}
tested_source_identity={{tested_source_identity_value}}
verification_target_identity={{verification_target_identity_value}}
```

业务验收必须说明环境、数据影响、入口动作和证据。发布成功不等于业务验收通过。

## 最终线上环境发布

没有最终线上环境时删除本节。

环境：`{{final_environment_name}}`

工作目录或制品入口：`{{final_release_entry}}`

前置条件：

- 前置验证已通过并记录 `tested_source_identity`。
- 重新执行“发布前源基线门禁”。
- 当前 `validated_source_identity` 与 `tested_source_identity` 一致；不一致时重新走前置验证环境。
- 已满足最终环境的逐次授权或受保护流水线预授权条件。

```text
{{final_target_align_commands}}
{{assert_tested_identity_unchanged_commands}}
{{final_target_promote_commands}}
{{final_environment_identity_gate_commands}}
{{final_deploy_commands}}
{{final_post_deploy_check_commands}}
```

记录：

```text
tested_source_identity={{tested_source_identity_value}}
target_release_identity={{target_release_identity_value}}
final_environment_identity={{final_environment_identity_value}}
```

默认不运行后台任务、不调用真实写接口、不执行线上数据变更；这些动作即使属于同一需求也需要单独授权和证据。

## 可选：最终环境直接修复

默认禁止在最终环境工作区或远端主机直接修改业务代码。只有项目真实采用此路径时才保留本节，并填写全部项目：

- 唯一工作区、代码线或受控编辑入口：`{{direct_final_environment_edit_entry}}`。
- 允许的故障和文件范围：{{direct_final_environment_edit_scope}}。
- 逐次授权、审批和审计身份：{{direct_final_environment_edit_authorization}}。
- 修改前工作区、目标环境和实际配置门禁：{{direct_final_environment_edit_preflight}}。
- 修改后定向测试、回归、差异检查和运行验收：{{direct_final_environment_edit_validation}}。
- 提交、推送、主开发线回流和后续标准发布要求：{{direct_final_environment_edit_reconciliation}}。

```text
{{direct_final_environment_edit_commands}}
```

部署、重启或线上排障授权不包含直接修改授权。任一字段未定义、现场与门禁不符、存在用户未提交修改或无法保证回流时停止；项目不允许此路径时删除本节。

## 制品交付与远端部署约束

- 标准交付或部署入口：`{{standard_delivery_or_deployment_entry}}`。
- 标准只读复验入口：`{{delivery_or_deployment_verify_only_entry}}`。
- 制品仓库、应用商店、发布轨道、运行基座、工作负载、容量和入口现状以 `{{environment_status_doc}}` 为准。
- 执行前先只读检查制品存在性与摘要、签名或来源、目标当前身份、容量或配额、发布锁、平台处理状态、track 或 rollout 状态；目录式部署再核对 staging、previous 和正式目录。
- 标准入口是否构建制品、安装依赖、创建运行资源或执行迁移：{{standard_delivery_or_deployment_capabilities}}。
- 不属于标准入口的首次初始化、基础设施变化、商店配置变化或专项运行操作必须有独立 runbook 和授权。
- 标准应用发布必须明确是否触碰数据库、消息 Broker、缓存、对象存储等外部基础设施；未明确列入能力时，不得创建、重建、重启、清空或轮换其配置和凭据。

## 发布后检查

```text
{{post_release_identity_check_commands}}
{{post_release_health_check_commands}}
{{post_release_log_check_commands}}
```

必须验证适用项：

- 目标环境实际代码或制品身份。
- 实际配置环境身份。
- 目标平台、发布轨道、工作负载、应用或进程状态。
- smoke、自检、健康检查、商店处理或分发状态。
- 关键日志、遥测、崩溃或平台错误中无新增阻塞问题。

发布后默认使用只读检查。业务写链路、后台任务和数据回查按需求文档与授权单独执行。

## 超时、中断和未知现场

发布、迁移、远端命令或真实联调超时、断连或结果不明时：

1. 停止重复执行。
2. 记录最后一个已确认成功的步骤、命令、时间和身份。
3. 使用 `{{unknown_state_readonly_inspection_commands}}` 只读核对锁、track、rollout 或发布对象、临时或 staging 资源、当前代码或制品身份、平台处理状态，以及适用的运行状态、数据版本、遥测和日志。
4. 区分“未执行”“执行中断”“已生效但响应丢失”和“失败后部分生效”。
5. 根据现场事实提出继续、补验或人工恢复方案；未经确认不删除现场、不回滚、不盲目重跑。

## 后台任务和真实写入口

项目没有后台任务或真实写入口时删除本节。

```text
{{background_job_or_real_write_commands}}
```

以上命令会造成 `{{background_job_or_write_impact}}`。每次执行前必须说明环境、业务范围、重复运行语义、预计写入量、停止条件和回查方式，并取得单独授权。

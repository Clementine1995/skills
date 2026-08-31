# {{project_name}}

{{project_one_line}}

## 项目负责

- {{project_responsibility_1}}
- {{project_responsibility_2}}

## 项目不负责

- {{project_non_responsibility_1}}
- {{project_non_responsibility_2}}

## 当前主链路

按真实调用顺序填写关键链路，不写尚未接通的计划能力。

- {{main_flow_name}}：`{{input_or_trigger}} -> {{core_processing_component}} -> {{boundary_or_output}}`
- {{secondary_flow_name}}：`{{input_or_trigger}} -> {{processing_step}} -> {{observable_result}}`

## 当前运行口径

本节只保存稳定的环境身份和用途摘要。易变化的 IP、端口、容器、挂载、代理和远端路径应放入独立环境现状文档；可执行命令只放在 `DEV_WORKFLOW.md`。

按项目实际环境数量增删行，不默认存在开发、测试或生产三套环境：

| 环境或运行角色 | 固定工作区 | 代码/制品身份 | 配置入口 | 数据与外部资源 | 允许用途 |
| --- | --- | --- | --- | --- | --- |
| {{environment_name_1}} | `{{environment_workspace_1}}` | `{{environment_code_identity_1}}` | `{{environment_config_1}}` | {{environment_resources_1}} | {{environment_allowed_usage_1}} |
| {{environment_name_2}} | `{{environment_workspace_2}}` | `{{environment_code_identity_2}}` | `{{environment_config_2}}` | {{environment_resources_2}} | {{environment_allowed_usage_2}} |
| {{environment_name_3}} | `{{environment_workspace_3}}` | `{{environment_code_identity_3}}` | `{{environment_config_3}}` | {{environment_resources_3}} | {{environment_allowed_usage_3}} |

无对应环境时删除整行及相关流程。存在多服务、多区域、多租户或临时预览环境时，增加环境现状文档，不在本节堆叠易变资源清单。

CI runner、开发者终端或构建机通常只是执行上下文，不自动算作独立环境；只有它们拥有不同配置、数据或外部资源边界时才单列。

环境硬边界：

- 真实联调只允许在 `{{real_integration_environment}}` 执行，并使用 `{{real_integration_config_identity}}`。
- 自动化测试使用 `{{automated_test_environment_or_config}}`，并按 `{{test_isolation_policy}}` 隔离真实资源。
- 每个受控环境都必须定义允许操作、禁止操作和实际身份校验方式。
- 存在多个发布目标时，为各目标定义固定工作区或不可变制品入口，不在受控目录中临时切换身份。
- 代码或制品晋级拓扑为 `{{promotion_topology}}`；禁止方向为 `{{forbidden_promotion_paths}}`。
- 若线上修复需要回流主开发线，回流方向、时机和门禁必须在 `DEV_WORKFLOW.md` 明确定义；不得默认照搬其他项目的策略。
- 应用与数据库、消息系统、缓存、对象存储等外部基础设施的生命周期责任必须明确；除非 `DEV_WORKFLOW.md` 明确列入标准入口，普通应用发布不得隐式创建、重建、重启或清空这些资源。

## 项目构建

### 前置条件

- 运行时：`{{runtime_and_version}}`
- 包管理器：`{{package_manager_and_version}}`
- 外部依赖：{{external_prerequisites}}

### 初始化

```text
{{initialize_commands}}
```

### 构建

```text
{{build_commands}}
```

不需要独立构建步骤时，写明“不适用”，不要保留伪命令。

## 最小运行或启动

运行命令行工具、调用库、启动服务或执行最小 smoke 前，先按 `DEV_WORKFLOW.md` 完成适用的工作区和配置身份检查。

```text
{{minimal_run_invoke_or_start_commands}}
```

长驻服务的健康检查或其他类型项目的最小自检：

```text
{{health_or_smoke_check_commands}}
```

适用时，自检必须至少证明：

- 运行或调用结果为 `{{expected_minimal_run_result}}`。
- 实际配置或资源身份为 `{{expected_runtime_identity}}`。
- 不输出密钥、完整连接串或其他敏感配置。

状态、健康或自检入口必须写清是只读观测还是会触发启动、修复或状态变更；后者属于运行操作，需在 `DEV_WORKFLOW.md` 使用独立入口和授权口径。

没有长驻服务时删除“健康检查”措辞；纯库项目可改为最小导入、编译或示例调用，不能保留伪造的服务门禁。

## 最小验证

定向测试：

```text
{{targeted_test_commands}}
```

全量测试：

```text
{{full_test_commands}}
```

静态检查：

```text
{{lint_type_and_format_check_commands}}
```

完整验证层级、Git 基线和发布命令见 `DEV_WORKFLOW.md`。测试命令不得连接真实数据库或外部系统；需要真实调用时必须进入“真实联调”任务等级并单独说明授权与影响。

## 目录说明

- `{{source_directory}}`：主工程源码。
- `{{test_directory}}`：自动化测试。
- `docs/`：需求、设计和专题追溯材料；不保存临时 AI 协作过程，也不自动代表当前实现或运行事实。
- `docs/requirements/`：单项需求的目标业务合同、决策、实施和验收材料；复杂需求可在其下建立同名子目录。
- `{{script_directory}}`：稳定脚本入口；脚本使用说明放在文档中。
- `{{temporary_artifact_directory}}`：经项目明确允许保留的本地临时验证材料；不提交一次性产物。
- 其他目录按实际补充，并删除不适用项。

## 文件地图

### 治理文档

- `AGENTS.md`：AI 入口、最高优先级授权边界和文档索引。
- `AI_COLLABORATION.md`：任务分级、协作生命周期、证据和收口。
- `PROJECT_RULES.md`：项目特有架构红线。
- `STYLE.md`：工程风格。
- `DEV_WORKFLOW.md`：启动、验证、Git、数据库和发布的唯一命令来源。
- `REQUIREMENT_DEVELOPMENT.md`：需求拆解、实施批次、验证和发布状态模板。
- `{{environment_status_doc}}`：环境与资源现状；不需要时删除本项。
- `{{service_runbook_doc}}`：复杂服务运行与专项验收；不需要时删除本项。

### 业务代码

- `{{component_directory_1}}`：{{component_directory_responsibility_1}}
- `{{component_directory_2}}`：{{component_directory_responsibility_2}}
- `{{component_directory_3}}`：{{component_directory_responsibility_3}}

按项目实际组件填写；命令行工具、库、前端、数据任务或单模块项目不需要套用服务端分层名称。

### 测试

- `{{behavior_test_directory}}`：业务行为测试。
- `{{architecture_test_directory}}`：架构边界与结构规则测试。
- `{{integration_test_directory}}`：隔离的集成测试；真实联调不得伪装成自动化单元测试。

## 需求开发口径

满足以下任一条件时，必须基于 `REQUIREMENT_DEVELOPMENT.md` 建立 `docs/requirements/{{requirement_id}}-{{requirement_name}}.md`：

- 新功能或既有业务行为变化。
- 跨多个组件、边界、仓库、数据源或交付物的改动。
- API、表结构、状态机、事务、幂等或兼容策略变化。
- 需要拆分多个实施批次、真实联调、受控环境验收或最终线上发布。
- 存在会改变实现结果的业务决策或明确废弃行为。

普通点状修复或纯文案小改可不新建需求文档，但仍须在开始前明确目标、不做范围、完成标准和验证方式。

复杂需求建议使用：

```text
总规格（当前已确认的目标业务合同）
  -> 步骤或实施批次文档
  -> 独立真实验收清单
  -> DEV_WORKFLOW 发布门禁
```

需求文档只引用 `DEV_WORKFLOW.md` 的门禁名称，不复制 Git、部署或数据库命令，避免命令漂移。

需求文档中的目标合同只有在实现和匹配验证完成后才可标记为已交付；当前代码、测试、`README.md`、环境现状文档或真实现场与需求材料不一致时，先报告差异并更新负责该事实的来源，不用阶段文档覆盖现状。

## 发布口径

没有远端发布或多环境晋级的项目可删除本节及 `DEV_WORKFLOW.md` 中对应章节。

- 开发前同步、提交、验证环境发布和最终环境发布的命令只看 `DEV_WORKFLOW.md`。
- 多阶段晋级必须基于同一个已验证源提交或不可变制品；记录 `validated_source_identity`、`tested_source_identity` 和各目标环境身份。
- 中间验证环境不得擅自成为最终环境的代码来源；若项目确实采用顺序制品晋级，必须在实例化时定义制品摘要和完整性校验。
- 源代码、构建依赖、构建参数、版本化发布配置或制品发生变化后，原验收不得继续用于后续环境。环境级运行配置和密钥可按环境不同，但要分别通过身份门禁并受变更控制。
- 环境发布可采用逐次人工授权或受保护流水线预授权；实例化时必须写明触发条件、审批和环境保护规则。
- 最终线上环境发布后默认只做发布脚本硬断言和只读可用性检查；后台任务、真实写接口和线上数据操作需要独立授权。
- 发布超时、中断或结果不明时先只读核对远端现场，禁止不加判断地重复执行。

## AI 协作口径

- 默认按“小步闭环”推进：一次只完成当前需求中可独立验证的最小交付单元。
- 用户说“继续下一步”时，先判断当前单元是否已达到收口条件；已完成则进入下一项，未完成则只补齐当前闭环。
- 旁支问题默认记录为后续建议；只有会阻塞当前需求、导致测试失败或造成数据错误时才纳入当前范围。
- 扩大范围、架构重构、兼容旧逻辑、数据写入、真实联调和发布必须按 `AI_COLLABORATION.md` 升级授权。

## 模板落地清单

1. 全局搜索 `{{...}}` 形式的占位符，替换所有项目名、路径、包名、分支、配置、命令和策略占位符。
2. 删除所有不适用环境、可选文档、目录、命令块和说明，不保留“以后可能用”的空壳。
3. 重写 `PROJECT_RULES.md`，每条红线都配套可执行的 grep、静态检查或自动化测试。
4. 按团队真实约定修改 `STYLE.md`，不要机械复制示例语言、commit 前缀或禁用命名。
5. 在 `DEV_WORKFLOW.md` 写入并人工审查真实命令；未替换的占位命令禁止执行。
6. 固定实际存在的环境、代码或制品身份、配置、数据库和外部资源边界，并验证 smoke、自检或健康检查能证明运行身份。
7. 明确晋级拓扑、线上修复回流策略、已验收版本身份和发布异常后的只读核查入口。
8. 使用 `REQUIREMENT_DEVELOPMENT.md` 建立第一个真实需求文档，验证模板能覆盖范围、批次、验收和发布状态。
9. 再次全局搜索 `{{...}}` 形式的占位符，确认没有非预期残留；检查所有 Markdown 交叉引用均指向存在文件。
10. 明确根目录治理文档、当前事实文档和 `docs/` 追溯材料的权威层级，避免需求或阶段材料覆盖代码、测试和最新运行现场。
11. 删除本“模板落地清单”中已完成且不再需要保留的模板说明，确保项目文档只描述当前有效事实。

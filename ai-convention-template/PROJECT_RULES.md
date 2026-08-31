# PROJECT_RULES.md

## 职责

本文件只保存本项目特有、违反后会造成架构破坏或业务事故，并且可以通过代码审查、文本搜索、静态检查或自动化测试验证的红线。

通用授权边界见 `AGENTS.md`，工程风格见 `STYLE.md`，执行命令见 `DEV_WORKFLOW.md`。

## 实例化要求

- 本文件必须按项目重写，不能直接把示例或其他项目规则当作当前事实。
- 每条规则必须包含明确范围、禁止或必须行为，以及验证方式。
- 仅属于团队偏好或格式习惯的内容放入 `STYLE.md`。
- 仅属于当前需求的业务规则放入对应需求文档。
- 易变化的端口、地址、容器和环境现状放入环境现状文档。
- 无法验证、没有事故边界或只表达愿景的句子不得列为“红线”。
- 删除所有不适用章节和未填占位符；宁缺毋滥。

## 项目定位

本项目：{{project_architecture_positioning}}

负责：

- {{architecture_responsibility_1}}
- {{architecture_responsibility_2}}

不负责：

- {{architecture_non_responsibility_1}}
- {{architecture_non_responsibility_2}}

## 架构红线

以下编号只是模板。实例化时连续编号，并把占位内容改成可直接判断真假的项目规则。

### 代码与运行时边界

1. {{runtime_boundary_rule}}
2. {{source_ownership_rule}}

填写方向：主工程与独立服务、前后端、插件、脚本、生成物或第三方代码的所有权和运行时边界。

### 常驻进程与基础设施生命周期

3. {{resident_process_lifecycle_rule}}
4. {{status_or_health_endpoint_semantics_rule}}
5. {{external_infrastructure_lifecycle_rule}}

填写方向：常驻监听器、调度器和后台线程由谁唯一启动、停止和恢复；状态或健康入口是只读观测还是运行操作；数据库、消息系统、缓存和对象存储是否属于标准应用发布的生命周期。项目没有对应能力时删除本节。

### 分层与依赖方向

6. {{layer_dependency_rule_1}}
7. {{layer_dependency_rule_2}}

填写方向：允许和禁止的依赖方向、数据库访问层、领域层、接口层，以及跨层调用入口。

### 入口与外部调用

8. {{official_entry_rule}}
9. {{external_call_boundary_rule}}

填写方向：正式入口白名单、禁止入口、HTTP/RPC/消息/文件调用必须经过的 adapter 或 client 层。

### 数据、状态与事务

10. {{data_integrity_rule}}
11. {{state_transition_rule}}
12. {{transaction_boundary_rule}}

填写方向：业务主键、软删除、必填失败证据、幂等、并发、状态机和事务提交边界。

### 文件与模块结构

13. {{module_naming_or_location_rule}}
14. {{generated_or_temporary_file_rule}}

填写方向：特定目录允许的文件模式、禁止的泛指模块、生成文件和临时产物边界。

### 可观测性

15. {{trace_identity_rule}}
16. {{audit_or_log_rule}}

填写方向：链路追踪标识由哪个权威入口生成、哪些下游必须复用已有标识、日志上下文、审计事件、敏感信息脱敏和跨层关联要求。

### 数据库结构与迁移

17. {{schema_change_entry_rule}}
18. {{migration_consistency_rule}}

填写方向：唯一结构变更入口、ORM/Schema/DDL/迁移的一致性和验证要求。项目没有数据库时删除本节。

### 测试与构建边界

19. {{architecture_test_location_rule}}
20. {{test_isolation_rule}}
21. {{build_artifact_rule}}

填写方向：架构测试目录、真实网络、数据库、消息系统、缓存和对象存储隔离，以及生成制品来源与完整性。

## 红线验证映射

每条红线必须在下表有对应验证。规则较多时可由架构测试自动生成映射，但本文件仍要指出入口。

| 规则编号 | 验证类型 | 命令或测试入口 | 通过标准 |
| --- | --- | --- | --- |
| 1 | {{review_search_or_test}} | `{{rule_1_verification}}` | {{rule_1_expected_result}} |
| 2 | {{review_search_or_test}} | `{{rule_2_verification}}` | {{rule_2_expected_result}} |
| {{rule_number}} | {{verification_type}} | `{{verification_entry}}` | {{expected_result}} |

## 变更规则

- 修改架构红线本身属于架构决策，不得作为普通业务改动顺手调整。
- 变更前必须说明原规则、目标规则、现有违反量、迁移范围和对应测试变化。
- 放宽红线必须获得用户或项目负责人的明确确认；不得通过删除测试、缩小搜索范围或增加例外名单绕过。
- 红线变更后同步修改架构测试、需求文档和受影响的文件地图。

# REQUIREMENT_DEVELOPMENT.md

## 职责

本文件定义单项需求从只读核查、业务确认、实施拆分、编码验证到环境晋级和最终收口的文档标准，并提供可复制模板。

需求文档保存已确认的目标业务合同、决策、实施边界和可追溯证据；当前实现或运行事实只记录带时间和来源的核查快照，不保存聊天流水、临时推理、一次性日志、真实敏感数据或重复命令。

## 何时必须使用

出现以下任一情况时，在 `docs/requirements/` 建立需求文档：

- 新功能或现有业务行为变化。
- 跨多个模块、服务、仓库或团队。
- API、事件、数据结构、状态机、事务、幂等或兼容策略变化。
- 需要多个实施单元、真实联调、数据库操作或环境发布。
- 存在必须由人工确认的业务决策、废弃行为或不可逆影响。

普通点状修复可不创建独立需求文档，但仍须明确目标、不做范围、完成标准和验证方式。

## 文档分层

普通需求使用一份文档覆盖全流程。复杂需求使用三层结构：

```text
总规格：当前已确认的目标业务合同和需求内状态
  -> 步骤或实施单元：每批目标、基线、文件落点和完成条件
  -> 真实验收清单：环境、授权、动作、停止条件和证据
```

具体启动、Git、数据库和发布命令只引用 `DEV_WORKFLOW.md` 的章节，不复制到需求文档。

需求文档属于需求追溯材料，不定义默认智能体规则，也不自动代表当前实现或运行事实。当前现状必须按适用范围由代码、匹配测试、`README.md`、指定的当前事实文档和执行前只读核查支持；这些证据与需求文档不一致时先报告差异，不用阶段材料覆盖现状。目标合同只有在实现和匹配验证完成后才可标记为已交付。

推荐路径：

```text
docs/requirements/{{requirement_id}}-{{requirement_name}}.md

# 复杂需求
docs/requirements/{{requirement_id}}-{{requirement_name}}/
  00-overall-spec.md
  01-{{implementation_unit}}.md
  acceptance-{{environment_or_scenario}}.md
```

文件名应表达长期业务身份，不用日期、对话轮次或“最终版”区分版本。

## 标准生命周期

```text
只读事实核查
  -> 业务规则确认
  -> 开发就绪判断
  -> 固定范围、基线和授权
  -> 按实际调用链拆分可独立验收单元
  -> 每单元计划、编码、定向测试和完成汇报
  -> 需求级回归、静态检查和构建验证
  -> 按需真实联调
  -> 按需验证环境发布与验收
  -> 使用同一已验收身份进入后续环境
  -> 发布后只读可用性检查
  -> 最终收口
```

“代码完成”“自动化通过”“真实联调通过”和“已发布”在适用时是不同事实，禁止合并成一个模糊状态。

使用时复制下方分隔线后的模板内容，删除不适用章节、示例行和占位符；需求文档中不得残留 `{{...}}`。需求较小时保留最小必要章节，不能为了填满模板制造无效流程。

---

# {{requirement_id}} {{requirement_name}} 开发与验收说明

## 0. 文档职责与状态

### 0.1 文档职责

本文负责：

- {{document_responsibility_1}}
- {{document_responsibility_2}}

本文不负责：

- {{document_non_responsibility_1}}
- {{document_non_responsibility_2}}

上位业务规格：`{{parent_specification}}`

关联实现文档：`{{related_implementation_documents}}`

关联接口或数据文档：`{{related_contract_documents}}`

运行与发布命令：`DEV_WORKFLOW.md` 的 `{{workflow_section_names}}`

### 0.2 独立状态维度

保留实际适用的状态维度。需求、实施和验证通常应独立；项目没有发布目标时删除“发布状态”整行，而不是长期填写空壳。

| 维度 | 当前状态 | 允许值 | 证据或阻塞项 |
| --- | --- | --- | --- |
| 需求状态 | {{requirement_status}} | 草拟 / 待确认 / 已确认 / 已废弃 | {{requirement_status_evidence}} |
| 实施状态 | {{implementation_status}} | 未开始 / 实施中 / 代码完成 / 不适用 | {{implementation_status_evidence}} |
| 验证状态 | {{verification_status}} | 未验证 / 自动化通过 / 真实联调通过 / 环境验收通过 / 不适用 | {{verification_status_evidence}} |
| 发布状态（如适用） | {{release_status}} | 未发布 / 已发布至某环境 / 已完成全部目标环境 | {{release_status_evidence}} |

当前权威结论更新时间：`{{authoritative_conclusion_updated_at}}`

当前实现基线：`{{baseline_source_identity}}`

文档状态更新必须基于当前证据；历史测试数字、旧提交或旧环境结果不能替代当前验证。

## 1. 结论与开发就绪判断

### 1.1 一句话结论

{{one_sentence_conclusion}}

### 1.2 开发就绪

- 是否可以进入开发：{{development_ready_yes_or_no}}
- 阻塞项：{{development_blockers_or_none}}
- 下一项允许动作：{{next_allowed_action}}

只有会改变实现结果的问题才列为阻塞。可从代码或文档查清的问题先只读核查。

### 1.3 事实、推断与风险

已确认事实：

- {{confirmed_fact_with_evidence_1}}

推断：

- {{inference_and_basis_1}}

未验证风险：

- {{unverified_risk_1}}

不得把推断写成现状，不得用“应该”“大概”作为实施合同。

### 1.4 待确认事项

- {{decision_changing_question_or_none}}

待确认事项不为“无”时，需求状态不能标记为“已确认”，相关实施单元不得编码。

## 2. 背景、目标与成功标准

### 2.1 当前问题

{{current_problem}}

### 2.2 用户或业务价值

{{user_or_business_value}}

### 2.3 目标行为

- {{target_behavior_1}}
- {{target_behavior_2}}

### 2.4 可观察成功标准

- {{observable_success_criterion_1}}
- {{observable_success_criterion_2}}

成功标准必须能由测试、接口、页面、数据、日志或发布身份验证。

## 3. 范围与边界

### 3.1 本期交付

- {{in_scope_item_1}}

### 3.2 本期不包含

- {{out_of_scope_item_1}}

### 3.3 明确废弃行为

- {{deprecated_behavior_and_removal_scope_or_none}}

废弃行为存在时，列出旧实现、旧入口、旧测试、旧文档和旧配置的删除范围，不保留未授权双轨。

### 3.4 兼容期

只有用户明确要求兼容期时填写：

- 兼容对象：{{compatibility_scope}}
- 触发条件：{{compatibility_trigger}}
- 观测方式：{{compatibility_observation}}
- 删除条件和最晚删除点：{{compatibility_removal_point}}

不需要兼容时写“无”，并删除其实现分支。

### 3.5 不得改变的既有行为

- {{protected_existing_behavior_1}}

## 4. 当前事实与实际调用链

本节是本次核查时点的证据摘要，不是覆盖代码、测试或最新运行现场的第二套事实来源；事实变化后更新负责该事实的根目录文档，并同步本需求状态。

### 4.1 当前流程

```text
{{input}}
  -> {{entry}}
  -> {{query_or_validation}}
  -> {{business_decision}}
  -> {{external_call_or_transaction}}
  -> {{write_or_output}}
```

### 4.2 代码事实

| 文件 | 方法、类或配置 | 关联字段或业务键 | 当前行为 | 证据类型 |
| --- | --- | --- | --- | --- |
| `{{file_path_1}}` | `{{symbol_1}}` | `{{field_or_key_1}}` | {{current_behavior_1}} | {{code_test_log_or_query}} |

### 4.3 数据与接口可靠边界

- 权威数据源：{{authoritative_data_source}}
- 业务主键：{{authoritative_business_keys}}
- 接口来源和版本：{{interface_source_and_version}}
- 时间、时区、金额、精度和单位：{{time_money_precision_units}}
- 可确认的当前数据范围：{{confirmed_data_scope}}
- 当前无法确认的边界：{{unconfirmed_data_boundary}}

### 4.4 环境事实

- 只读核查环境：{{readonly_inspection_environment}}
- 开发或自动化环境：{{development_or_test_environment}}
- 真实联调环境：{{real_integration_environment_or_none}}
- 发布目标：{{release_targets_or_none}}

环境地址、凭据、端口和容器现状只链接环境文档，不在本文复制敏感或易变值。

## 5. 最终业务合同

### 5.1 对象与处理粒度

- 核心业务对象：{{core_business_objects}}
- 单次处理粒度：{{processing_granularity}}
- 关联键与唯一性：{{identity_and_uniqueness}}

### 5.2 输入合同

| 字段或事件 | 来源 | 必填 | 值域或格式 | 缺失语义 | 是否参与业务判断 |
| --- | --- | --- | --- | --- | --- |
| `{{input_name_1}}` | {{input_source_1}} | {{required_1}} | {{value_rule_1}} | {{missing_semantics_1}} | {{business_use_1}} |

### 5.3 输出合同

| 字段、事件或状态 | 去向 | 生成规则 | 空值或失败语义 | 审计要求 |
| --- | --- | --- | --- | --- |
| `{{output_name_1}}` | {{output_target_1}} | {{generation_rule_1}} | {{failure_semantics_1}} | {{audit_requirement_1}} |

### 5.4 正常流程

1. {{normal_flow_step_1}}
2. {{normal_flow_step_2}}

### 5.5 状态、重复与并发

- 状态机：{{state_machine}}
- 重复请求和幂等：{{idempotency_rule}}
- 并发与锁：{{concurrency_rule}}
- 排序和优先级：{{ordering_rule}}
- 数量守恒或覆盖关系：{{conservation_or_coverage_rule}}

### 5.6 失败、退出与恢复

| 失败点 | 影响范围 | 是否提交 | 当前记录 | 后续动作 |
| --- | --- | --- | --- | --- |
| {{failure_point_1}} | {{impact_scope_1}} | {{commit_semantics_1}} | {{failure_evidence_1}} | {{followup_action_1}} |

不得用未确认 fallback、默认值或静默跳过改变失败语义。

### 5.7 行为决策矩阵

| 条件 | 目标行为 | 明确不做 | 验证方式 |
| --- | --- | --- | --- |
| {{condition_1}} | {{expected_behavior_1}} | {{forbidden_behavior_1}} | {{verification_1}} |

## 6. 目标技术设计

### 6.1 目标调用链

```text
{{target_input}}
  -> {{target_entry}}
  -> {{target_service}}
  -> {{target_adapter_or_storage}}
  -> {{target_output}}
```

### 6.2 分层职责

| 层或组件 | 唯一职责 | 输入 | 输出 | 不负责 |
| --- | --- | --- | --- | --- |
| {{component_1}} | {{responsibility_1}} | {{component_input_1}} | {{component_output_1}} | {{component_non_responsibility_1}} |

### 6.3 接口、事件和数据模型

- API 或事件变化：{{api_or_event_changes_or_none}}
- 数据结构变化：{{schema_changes_or_none}}
- 配置变化：{{configuration_changes_or_none}}
- 依赖变化：{{dependency_changes_or_none}}
- 兼容和版本策略：{{versioning_strategy_or_none}}

具体 DDL、迁移和执行命令只放 `DEV_WORKFLOW.md` 或经批准的稳定迁移入口；本文记录业务目的、字段合同和影响。

### 6.4 事务、幂等与外部失败保护

- 事务边界：{{transaction_boundary}}
- 幂等实现：{{idempotency_implementation}}
- 外部调用超时与重试：{{external_failure_policy}}
- 部分成功语义：{{partial_success_semantics}}
- 批量和性能边界：{{batch_and_performance_boundary}}

### 6.5 可观测性与安全

- 链路标识：{{trace_identity}}
- 日志和审计事件：{{logs_and_audit_events}}
- 敏感数据处理：{{sensitive_data_handling}}
- 权限与鉴权：{{authorization_and_authentication}}

### 6.6 运行时与基础设施生命周期

- 常驻进程、监听器或后台线程的生命周期所有者：{{resident_process_lifecycle_owner_or_none}}
- 启动、停止、恢复和重复启动语义：{{runtime_start_stop_recovery_semantics}}
- 状态、健康或自检入口是只读观测还是运行操作：{{status_health_endpoint_semantics}}
- 数据库、消息系统、缓存或对象存储的生命周期与标准发布边界：{{external_infrastructure_lifecycle_boundary}}

没有常驻进程或外部基础设施时删除不适用项，不为模板完整性虚构运行时能力。

## 7. 影响清单

只列当前需求直接影响项；没有则写“无”。

| 类型 | 新增、修改或删除 | 文件、对象或系统 | 目标职责或行为 | 对应验收 |
| --- | --- | --- | --- | --- |
| 入口 | {{entry_change_type}} | `{{entry_file_or_api}}` | {{entry_change}} | {{entry_acceptance}} |
| 服务 | {{service_change_type}} | `{{service_file}}` | {{service_change}} | {{service_acceptance}} |
| client/adapter | {{client_change_type}} | `{{client_file}}` | {{client_change}} | {{client_acceptance}} |
| 模型或数据 | {{data_change_type}} | `{{model_table_or_event}}` | {{data_change}} | {{data_acceptance}} |
| 运行或基础设施 | {{runtime_infrastructure_change_type}} | `{{runtime_process_or_resource}}` | {{runtime_infrastructure_change}} | {{runtime_infrastructure_acceptance}} |
| 测试 | {{test_change_type}} | `{{test_file}}` | {{test_change}} | {{test_acceptance}} |
| 文档或发布 | {{doc_change_type}} | `{{doc_or_workflow_file}}` | {{doc_change}} | {{doc_acceptance}} |

## 8. 实施拆分

按可独立验收的业务闭环拆分，不为追求编号制造长期半成品。每个实施单元复制以下模板。

### {{unit_id}} {{unit_name}}

- 目标：{{unit_goal}}
- 前置依赖：{{unit_dependencies}}
- 进入条件：{{unit_entry_criteria}}
- 固定基线：{{unit_baseline_identity}}
- 交付内容：{{unit_deliverables}}
- 不交付内容：{{unit_non_deliverables}}
- 修改文件、方法、字段和调用关系：{{unit_change_locations}}
- 废弃和删除范围：{{unit_removal_scope_or_none}}
- 授权等级：{{unit_authorization_level}}
- 定向测试：{{unit_targeted_tests}}
- 回归范围：{{unit_regression_scope}}
- 完成条件：{{unit_completion_criteria}}
- 当前状态：{{unit_status}}

如用户明确允许某个实施单元跳过默认开发前同步，必须额外记录：

- 例外只适用的单元：{{sync_exception_unit}}
- 固定源基线：{{sync_exception_baseline}}
- 禁止合并或同步的来源：{{sync_exception_forbidden_sources}}
- 替代只读检查：{{sync_exception_readonly_checks}}
- 例外失效条件：{{sync_exception_expiration}}

例外不得自动延续到后续单元或发布门禁。

## 9. 测试与验收

### 9.1 自动化测试矩阵

| 层级 | 场景 | 输入或前置 | 期望结果 | 命令入口 | 当前结果 |
| --- | --- | --- | --- | --- | --- |
| 定向 | {{targeted_scenario}} | {{targeted_precondition}} | {{targeted_expected}} | `DEV_WORKFLOW.md: {{targeted_section}}` | {{targeted_result}} |
| 回归 | {{regression_scenario}} | {{regression_precondition}} | {{regression_expected}} | `DEV_WORKFLOW.md: {{regression_section}}` | {{regression_result}} |
| 全量 | {{full_suite_scope}} | {{full_suite_precondition}} | {{full_suite_expected}} | `DEV_WORKFLOW.md: {{full_test_section}}` | {{full_test_result}} |
| 静态/构建 | {{static_build_scope}} | {{static_build_precondition}} | {{static_build_expected}} | `DEV_WORKFLOW.md: {{static_build_section}}` | {{static_build_result}} |

至少按风险覆盖：正常流程、重复或幂等、边界、失败保护、事务、旧链路回归和安全边界。

自动化测试应隔离真实数据库、消息 Broker、缓存、对象存储和外部网络；确需使用隔离集成环境时，在 9.2 节按真实联调记录资源身份、授权和影响。

### 9.2 真实联调计划

- 是否需要：{{real_integration_required}}
- 环境和实际身份：{{real_integration_environment_identity}}
- 数据库、存储和业务对象：{{real_integration_data_scope}}
- 外部系统：{{real_integration_external_systems}}
- 读写影响和预计数量：{{real_integration_write_impact}}
- 执行顺序：{{real_integration_sequence}}
- 立即停止条件：{{real_integration_stop_conditions}}
- 已获授权：{{real_integration_authorization}}

### 9.3 证据要求

按需求风险裁剪，不机械要求每项都适用：

- 页面或正式入口动作：{{entry_action_evidence}}
- Network、API、消息或命令结果：{{interface_evidence}}
- 数据库或存储只读回查：{{data_readback_evidence}}
- 日志或审计事件：{{log_or_audit_evidence}}
- 关联标识：{{request_event_business_identity}}
- 环境、日期、源代码或制品身份：{{environment_date_source_identity}}

必须分别写明 Mock、真实只读、真实写链路和未实测项，不能相互替代。

## 10. 环境、数据和外部影响授权

| 动作 | 环境 | 读/写/状态变化 | 影响范围 | 所需授权 | 当前授权状态 |
| --- | --- | --- | --- | --- | --- |
| 文件修改 | {{file_change_environment}} | 写 | {{file_scope}} | 小改动 | {{file_change_authorization_status}} |
| 依赖或配置 | {{dependency_config_environment}} | 状态变化 | {{dependency_config_scope}} | {{dependency_config_authorization_model}} | {{dependency_config_authorization_status}} |
| 数据库或迁移 | {{database_change_environment}} | 写 | {{database_scope}} | {{database_change_authorization_model}} | {{database_authorization_status}} |
| 真实接口或后台任务 | {{real_write_environment}} | 写/状态变化 | {{business_scope}} | {{real_write_authorization_model}} | {{real_write_authorization_status}} |
| 服务启停或部署 | {{service_operation_environment}} | 状态变化 | {{service_scope}} | {{service_operation_authorization_model}} | {{service_operation_authorization_status}} |
| 最终环境直接修复（如允许） | {{direct_final_edit_environment}} | 写/状态变化 | {{direct_final_edit_scope}} | 逐次明确授权并引用 `DEV_WORKFLOW.md` 的可选流程 | {{direct_final_edit_authorization_status}} |

没有对应能力时删除整行，不保留误导性授权项。

受保护 CI/CD 可以承接经审核的正式迁移或发布预授权，但必须记录触发条件、保护规则和审计身份；临时 DDL/DML、破坏性变更、数据修复和范围外写入仍逐次授权。

## 11. 发布与门禁

没有远端发布时写“不适用”并删除子项。

- 开发前基线检查：`DEV_WORKFLOW.md` 的 `{{pre_development_gate_section}}`。
- 开发环境身份门禁：`DEV_WORKFLOW.md` 的 `{{development_identity_gate_section}}`。
- 发布前完整验证：`DEV_WORKFLOW.md` 的 `{{pre_release_gate_section}}`。
- `validated_source_identity`：{{validated_source_identity}}
- 前置验证环境：{{verification_environment_or_none}}
- `tested_source_identity`：{{tested_source_identity}}
- 后续环境必须使用同一身份：{{identity_consistency_rule}}
- 发布后只读可用性检查：`DEV_WORKFLOW.md` 的 `{{post_release_check_section}}`。
- 后台任务、真实写接口和线上数据操作：{{separate_authorization_requirements}}

发布命令超时、中断或结果不明时，按 `DEV_WORKFLOW.md` 的“超时、中断和未知现场”先只读核对，不直接重跑。

## 12. 实施完成记录

每个实施单元完成后只更新稳定结果，不粘贴大段日志。

### {{unit_id}} 完成汇报

- 结果：{{completed_partial_or_blocked}}
- 实际修改：{{actual_changes}}
- 与计划偏差：{{plan_deviation_or_none}}
- 业务代码配套核对：审计或可观测性={{audit_observability_check}}；职责注释或稳定说明={{responsibility_documentation_check}}；匹配测试={{matching_test_check}}；没有业务代码改动时写“不适用”
- 定向测试：{{targeted_test_command_identity_date_and_result}}
- 回归、全量和静态检查：{{regression_full_static_results}}
- 真实联调：{{real_integration_result_or_not_run}}
- 外部和环境操作：{{external_environment_operations_or_none}}
- 未执行：{{not_executed_items}}
- 剩余风险：{{remaining_risks_or_none}}
- Git 或版本身份：{{git_or_source_identity}}
- 提交、推送和发布状态：{{commit_push_release_status}}

## 13. 当前最终结论

- 需求状态：{{final_requirement_status}}
- 实施状态：{{final_implementation_status}}
- 验证状态：{{final_verification_status}}
- 发布状态（如适用）：{{final_release_status}}
- 已满足完成条件：{{satisfied_completion_criteria}}
- 尚未满足完成条件：{{unsatisfied_completion_criteria_or_none}}
- 未验证项：{{unverified_items_or_none}}
- 剩余风险：{{final_remaining_risks_or_none}}
- 下一项允许动作：{{final_next_allowed_action}}
- 是否可以关闭需求：{{can_close_requirement_yes_or_no}}

只有目标行为实现、匹配验证完成、状态证据一致且无直接阻塞问题时，才可关闭需求。优化、清理和旁支建议应拆成独立需求，不延长当前需求。

# {{project_name}}

{{project_one_line}}

## 项目负责

- 填写本项目负责的核心职责。

## 项目不负责

- 填写本项目明确不承担的边界。

## 最小启动

> 按实际技术栈替换命令。

初始化：

```powershell
# 依赖安装命令，例如：
# python -m venv .venv
# .\.venv\Scripts\python.exe -m pip install -e .[dev]
# 或 npm install
```

启动：

```powershell
# {{start_cmd}}
```

健康检查：

```powershell
# curl {{health_check_url}}
```

测试：

```powershell
# {{test_cmd}}
```

## 目录说明

- `src/`：主工程源码。
- `tests/`：测试目录。
- `docs/`：项目说明和专题材料目录；不保存临时 AI 协作过程材料或历史过程归档。
- 其他目录按项目实际补充。

## 文档索引

- `AGENTS.md`：AI 协作约束（强约束 + 任务分级 + 工程风格 + 架构红线填写位 + 证据收口）。

## 环境口径

> 按实际环境数量填写，删除不适用的环境。

- 开发环境：`{{dev_branch}}` + `{{dev_config}}`，工作区 `{{dev_workspace}}`。
- 测试环境（如有）：`{{test_branch}}` + `{{test_config}}`，工作区 `{{test_workspace}}`。
- 生产环境（如有）：`{{prod_branch}}` + `{{prod_config}}`，工作区 `{{prod_workspace}}`。
- Git 合并只允许 `主开发分支 -> 测试分支` 和 `主开发分支 -> 生产分支`，禁止 `测试分支 -> 生产分支`。
- 本地端到端只在主开发分支和开发环境配置下执行。

## 落地清单

新项目接入时：

1. 全局搜索 `{{` 替换占位符（路径、端口、包名、分支、命令）。
2. 重写 `AGENTS.md` 的"架构红线"章节为项目特有红线。
3. 调整"工程风格"章节的 commit 前缀和命名禁忌为团队习惯。
4. 按实际环境数量调整"环境口径"。
5. 全局搜索 `{{` 确认无残留占位符。

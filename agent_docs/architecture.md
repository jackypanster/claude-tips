# agent_docs/architecture.md

## 目的
给 Agent 一张“系统地图”：组件边界、数据流、关键入口与约束。
这里写结构与原则；实现细节用 file:line 指向源码。

## 系统概览（请维护为权威）
- 项目名称：`{{PROJECT_NAME}}`
- 主要目标：`{{PROJECT_GOAL}}`
- 主要用户/调用方：`{{PRIMARY_USERS_OR_SYSTEMS}}`

## 顶层组件与职责
用“组件 -> 职责 -> 主要输入/输出”描述（越少越清楚）：

- `{{COMPONENT_A}}`
  - 职责：`{{A_RESPONSIBILITY}}`
  - 输入：`{{A_INPUTS}}`
  - 输出：`{{A_OUTPUTS}}`

- `{{COMPONENT_B}}`
  - 职责：`{{B_RESPONSIBILITY}}`
  - 输入：`{{B_INPUTS}}`
  - 输出：`{{B_OUTPUTS}}`

## 关键数据流（从入口到出口）
用 3~7 步描述主链路：
1) `{{STEP_1}}`
2) `{{STEP_2}}`
3) `{{STEP_3}}`
...

## 关键入口点（entrypoints）
- CLI 入口：`{{CLI_ENTRY}}`（file:line）
- 服务入口：`{{SERVICE_ENTRY}}`（file:line）
- 任务/Worker：`{{WORKER_ENTRY}}`（file:line）
- API 路由：`{{API_ROUTER_ENTRY}}`（file:line）

## 依赖与集成点
- 内部依赖：`{{INTERNAL_DEPS}}`
- 外部依赖：`{{EXTERNAL_DEPS}}`
- 存储：`{{STORAGE}}`
- 消息/事件：`{{MQ_OR_EVENTING}}`

## 配置与环境变量
- 配置文件：`{{CONFIG_FILES}}`
- 环境变量：`{{ENV_VARS}}`
- 约束：哪些配置在 CI/生产必须显式提供：`{{CONFIG_CONSTRAINTS}}`

## 非功能性约束（必须明确）
- 安全/权限边界：`{{SECURITY_BOUNDARIES}}`
- 性能/延迟目标：`{{SLO_OR_PERF_TARGETS}}`
- 可观测性：日志/指标/追踪的权威来源：`{{OBSERVABILITY_NOTES}}`

## 变更原则（架构层）
- 改动优先局部化，避免跨边界耦合。
- 若必须跨组件改动，先更新本文件中的“数据流与边界”，再改代码。

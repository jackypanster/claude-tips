# agent_docs/build.md

## 目的
说明如何把项目“跑起来”，并能稳定复现构建结果。
本文件存放具体命令与环境约束，避免污染全局 CLAUDE.md。

## 快速开始（优先级从高到低）
按以下顺序尝试（只需命中一种即可）：

1) `make help` / `make`
2) `task -l`（如使用 Taskfile）
3) `just -l`（如使用 justfile）
4) 包管理脚本（如 `npm run` / `pnpm` / `poetry` / `pip` / `go` / `mvn` / `gradle` 等）
5) `README.md` 的 Quickstart 章节

如果项目已有“标准入口命令”，请把它写在下面“项目入口”里，作为唯一权威来源。

## 项目入口（请维护为权威）
- 启动开发环境：
  - `{{DEV_START_COMMAND}}`
- 构建：
  - `{{BUILD_COMMAND}}`
- 运行：
  - `{{RUN_COMMAND}}`
- 停止/清理：
  - `{{STOP_CLEAN_COMMAND}}`

## 环境前置（最小集合）
- Shell：bash/zsh 任一
- Git：可用（用于查看变更、回滚、定位问题）
- 网络：能访问依赖源（如存在内网镜像/代理需注明）

### 运行时与工具版本（建议记录）
- 语言运行时版本：`{{RUNTIME_VERSIONS}}`（node/python/go/java 等）
- 包管理器版本：`{{PKG_MANAGERS}}`
- 关键 CLI（如有）：`{{REQUIRED_CLIS}}`

提示：需要确认某工具是否可用时，用 `command -v <tool>` 或 `which <tool>`。

## 构建产物与目录约定
- 主要构建产物目录：`{{ARTIFACT_DIR}}`（如 `dist/`、`build/`、`target/` 等）
- 缓存目录（可安全删除）：`{{CACHE_DIRS}}`（如 `node_modules/`、`.venv/`、`~/.cache/...` 等）
- 生成文件是否纳入版本控制：`{{GENERATED_FILES_POLICY}}`

## 可复现性与版本钉住
- 版本策略：`{{RUNTIME_VERSION_POLICY}}`（例如固定版本/允许范围）
- 依赖锁文件：
  - 锁文件清单：`{{LOCKFILES}}`
  - CI 是否强校验 lock：`{{CI_LOCK_POLICY}}`

## 常见问题（按“先证据后结论”）
### 依赖安装失败
- 先记录错误全文（关键堆栈/退出码）
- 检查：
  - 网络/代理/镜像源
  - 版本是否匹配（运行时、包管理器、关键 CLI）
  - 缓存/锁文件是否一致

### 构建慢或卡住
- 先确认正在做什么（输出/日志/进程）
- 再观察资源：CPU/内存/磁盘（见 debugging.md 的“资源压力”）
- 最后考虑：降低并行度、清理缓存、增量/全量构建切换

## 约束与禁止项（只写确实会出事故的）
- 禁止在本机执行：`{{DANGEROUS_COMMANDS_OR_ENV}}`
- 需要额外审批/权限：`{{PRIVILEGE_NOTES}}`

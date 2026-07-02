# AGENTS.project.md｜<project-name> 项目定制检查清单

本文件只承载本项目定制规则。每日治理同步任务不得自动覆盖本文件；只有用户在当前会话中明确授权时才可以修改。

## B0. 项目身份

- [ ] 项目名称已确认：`<project-name>`。
- [ ] 仓库已确认：`<owner>/<repo>`。
- [ ] 产品定位已确认：`<product-positioning>`。
- [ ] 核心用户场景已确认：`<main-user-scenarios>`。
- [ ] 技术栈已确认：`<tech-stack>`。

## B1. 当前开发基线检查

- [ ] 默认分支已确认：`<default-branch>`。
- [ ] 当前 source-of-truth 开发分支已确认：`<dev-branch>`。
- [ ] 修改前已从目标分支读取最新目标文件。
- [ ] 常规任务分支命名已使用：`chatgpt/task-xxx`。
- [ ] Codex 任务分支命名已使用：`codex/task-xxx`。
- [ ] PR 目标分支已确认：`<pr-target-branch>`。
- [ ] 只有用户明确要求直接修改目标分支时，才允许跳过任务分支。

## B2. 本项目必读文件检查

开始任何需求设计、代码修改、UI 调整或 PR 验收前，必须读取：

- [ ] `AGENTS.md`
- [ ] `AGENTS.common.md`
- [ ] `AGENTS.project.md`
- [ ] `README.md`
- [ ] `docs/handoff/latest-handoff.md`，如存在。
- [ ] `docs/design/current-core-design.md`，如存在。
- [ ] `docs/requirements/current-requirements.md`，如存在。
- [ ] `docs/changes/CHANGELOG-dev.md`，如存在。

按任务类型追加读取：

- [ ] 涉及 ChatGPT GitHub connector 操作时，已读取项目内 connector guide 和 feedback loop。
- [ ] 涉及版本时，已读取所有项目版本文件。
- [ ] 涉及依赖时，已读取 package / lock / dependency manifest。
- [ ] 涉及后端、数据库、ETL、UI、构建或发布时，已读取对应模块文件。

## B3. 本项目方向一致性检查

- [ ] 是否保持项目当前产品方向。
- [ ] 是否保持项目当前架构主线。
- [ ] 是否避免破坏已确认业务口径。
- [ ] 是否避免无关重构。
- [ ] 是否避免新增多个治理入口。

## B4. 本项目版本检查

- [ ] 当前版本已确认：`<version>`。
- [ ] 项目真实版本文件已同步：`<version-files>`。
- [ ] README 当前版本已同步。
- [ ] handoff 当前版本已同步，如存在。
- [ ] changelog 当前版本已同步，如存在。
- [ ] 不改依赖时，未修改 lock 文件。
- [ ] 版本体系未确认时，未强行新增版本机制。

## B5. 本项目构建与 CI 检查

- [ ] 构建命令已确认：`<build-command>`。
- [ ] 测试命令已确认：`<test-command>`。
- [ ] 类型检查 / 后端检查命令已确认：`<check-command>`。
- [ ] CI 文件已检查：`<ci-files>`。
- [ ] 未发现 CI 时，未声称 CI 通过。

## B6. 本项目禁止事项检查

- [ ] 不提交凭据、运行数据、缓存、数据库导出、安装包或构建产物。
- [ ] 不做无关 UI 风格重写。
- [ ] 不删除用途未确认的旧模块。
- [ ] 不修改用户未授权的发布、依赖或数据库结构。

## B7. 本项目交付附加要求

每次修改完成后必须汇报：

- [ ] 目标分支。
- [ ] 任务分支；若直接修改目标分支，说明用户已明确要求。
- [ ] commit hash。
- [ ] 最新版本号。
- [ ] 修改文件清单。
- [ ] 做了什么。
- [ ] 没做什么。
- [ ] 是否修改依赖 / lock 文件。
- [ ] 是否执行 build / test / check。
- [ ] 未验证项和原因。

## B8. ChatGPT GitHub Connector 操作检查

- [ ] 已读取项目内 connector guide 和 feedback loop。
- [ ] 使用 `compare_commits` 检查分支差异，未用 `update_ref` 做探测。
- [ ] 使用 `fetch_file` 获取文件内容和 sha。
- [ ] 使用 `update_file` 更新已有 UTF-8 文本文件。
- [ ] 使用 `create_file` 新增小型 UTF-8 文本文件。
- [ ] 每次写入后已回读关键文件确认。
- [ ] 遇到 safety block、not fast-forward、sha 冲突时，已停止说明或重新读取后再判断，未盲目重试。
- [ ] 操作结束前已复盘是否出现新的 connector 问题或更优流程。
- [ ] 如出现新经验，已更新项目内 guide、feedback loop 或公共治理仓。

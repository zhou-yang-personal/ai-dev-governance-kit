# <Project Name> 当前交接入口

## 1. 当前主线状态

```text
项目：<project-name>
仓库：<owner>/<repo>
当前分支：<branch>
当前版本：<version>
当前阶段：<current-stage>
最新有效提交：<commit-sha>
```

## 2. 本轮关键变更

```text
<summary-of-latest-changes>
```

## 3. 关键文件

```text
AGENTS.md
AGENTS.common.md
AGENTS.project.md
README.md
docs/handoff/latest-handoff.md
docs/design/current-core-design.md
docs/requirements/current-requirements.md
docs/changes/CHANGELOG-dev.md
docs/development/chatgpt-github-connector-guide.md
```

## 4. 后续执行入口

```text
每次需求设计、代码修改、UI 调整、PR 验收前，先读取根目录 AGENTS.md，并继续读取 AGENTS.common.md 和 AGENTS.project.md。
涉及 GitHub connector 操作时，先读取项目内 connector guide。
```

## 5. 当前风险

```text
<known-risks>
```

## 6. 新会话启动文本

```text
当前项目为 <project-name>，仓库为 <owner>/<repo>，当前 source-of-truth 分支为 <branch>，当前版本为 <version>。每次需求设计、代码修改、UI 调整、PR 验收前，必须先读取仓库根目录 AGENTS.md，并继续读取 AGENTS.common.md 和 AGENTS.project.md；若无法读取，必须先说明缺失情况，不得直接设计或改代码。
```

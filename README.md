# AI Dev Governance Kit

跨项目 AI 协作开发治理公共源仓，用于统一维护 ChatGPT / Codex / 人工开发共同使用的通用规则、模板、GitHub connector 操作手册和同步任务 prompt。

本仓不是业务项目仓，不存放任何单一项目的业务代码、数据库、UI 设计或项目专属规则。

## 1. 核心目标

1. 维护跨项目通用治理规则。
2. 统一项目仓三文件治理结构。
3. 沉淀 GitHub connector 的稳定操作流程和失败处理经验。
4. 提供新项目治理初始化模板。
5. 固化每日治理同步任务 prompt。

## 2. 三文件治理结构

项目仓统一采用：

```text
AGENTS.md                 # 固定入口，只负责引导读取和声明优先级
AGENTS.common.md          # 从本仓 AGENTS.base.md 同步
AGENTS.project.md         # 项目定制规则，不得被每日同步覆盖
```

公共治理仓自身采用：

```text
AGENTS.md                 # 公共仓固定入口
AGENTS.base.md            # 跨项目公共规则源文件
AGENTS.project.md         # 公共仓自身项目规则
```

## 3. 推荐目录结构

```text
.
├─ README.md
├─ AGENTS.md
├─ AGENTS.base.md
├─ AGENTS.project.md
├─ guides/
│  └─ chatgpt-github-connector-guide.md
├─ templates/
│  ├─ AGENTS.entry-template.md
│  ├─ AGENTS.project-template.md
│  ├─ pull_request_template.md
│  ├─ CHANGELOG-dev.template.md
│  └─ latest-handoff.template.md
└─ prompts/
   ├─ daily-governance-sync.prompt.md
   ├─ initialize-project-governance.prompt.md
   ├─ new-chat-handoff.prompt.md
   └─ codex-task-prompt.template.md
```

## 4. 文件职责

| 文件 | 职责 | 是否长期维护 |
|---|---|---|
| `AGENTS.md` | 公共仓入口 | 是 |
| `AGENTS.base.md` | 公共规则源文件，同步到项目仓 `AGENTS.common.md` | 是 |
| `AGENTS.project.md` | 公共仓自身规则 | 是 |
| `guides/chatgpt-github-connector-guide.md` | GitHub connector 操作手册和经验回写机制 | 是 |
| `templates/AGENTS.entry-template.md` | 项目根入口模板 | 是 |
| `templates/AGENTS.project-template.md` | 项目定制规则模板 | 是 |
| `templates/pull_request_template.md` | PR 检查模板 | 是，但不强制覆盖项目特有模板 |
| `templates/CHANGELOG-dev.template.md` | changelog 初始化模板 | 可选维护 |
| `templates/latest-handoff.template.md` | handoff 初始化模板 | 可选维护 |
| `prompts/daily-governance-sync.prompt.md` | 每日治理同步任务 prompt | 是 |
| `prompts/initialize-project-governance.prompt.md` | 新项目治理初始化 prompt | 是 |
| `prompts/new-chat-handoff.prompt.md` | 新会话启动模板 | 可选维护 |
| `prompts/codex-task-prompt.template.md` | Codex 单任务启动模板 | 可选维护 |

## 5. 同步范围

当前账户 `zhou-yang-personal` 下所有可访问开发仓默认纳入治理同步范围，不再维护人工 allowlist。

自动跳过条件：

```text
archived 仓库
fork 仓库，除非用户单独授权
无目标分支的仓库
存在 .governance-sync-ignore 的仓库
存在 .github/governance-sync-ignore 的仓库
权限不足的仓库
关键文件不可读或分界无法识别的仓库
```

## 6. 每日同步边界

默认允许同步：

```text
AGENTS.common.md
docs/development/chatgpt-github-connector-guide.md
.github/pull_request_template.md
```

默认不得自动覆盖：

```text
AGENTS.project.md
项目业务代码
项目业务文档
数据库 / ETL / UI / 构建逻辑
依赖文件和 lock 文件
```

## 7. 使用原则

- 公共仓只维护跨项目重复出现、且需要统一口径的内容。
- 项目特有规则必须留在项目仓 `AGENTS.project.md`。
- 已有项目模板不应被粗暴覆盖，应按公共规则合并。
- GitHub connector 操作出现新问题时，应判断是否具备跨项目复用价值；具备则回写本仓主 guide。

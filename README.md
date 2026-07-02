# AI Dev Governance Kit

跨项目 AI 协作开发治理模板仓，用于统一维护 ChatGPT / Codex / 人工开发共同使用的通用规则、模板、操作手册和启动 prompt。

## 1. 仓库定位

本仓库不是某一个业务项目的代码仓，而是所有 AI 辅助开发项目的治理资源上游仓。

目标：

1. 统一沉淀通用 `AGENTS.md` 检查规则。
2. 统一沉淀 ChatGPT GitHub connector / Codex / PR / 版本 / 交付等操作手册。
3. 为每个具体项目生成本地化治理文件。
4. 避免每个项目重复踩 GitHub、PR、版本号、handoff、构建验证等流程坑。

## 2. 使用原则

不建议项目仓只远程引用本仓文件。每个项目仍应保留自己的根目录 `AGENTS.md`。

推荐模式：

```text
公共仓：维护通用模板和最新经验。
项目仓：复制并本地化 AGENTS.md、connector guide、PR 模板等文件。
执行时：始终以当前项目根目录 AGENTS.md 为最高优先级入口。
```

## 3. 目录结构

```text
.
├─ README.md
├─ AGENTS.base.md
├─ guides/
│  ├─ chatgpt-github-connector-guide.md
│  └─ chatgpt-github-connector-feedback-loop.md
├─ templates/
│  ├─ AGENTS.project-template.md
│  ├─ pull_request_template.md
│  ├─ CHANGELOG-dev.template.md
│  └─ latest-handoff.template.md
└─ prompts/
   ├─ generate-project-agents.prompt.md
   ├─ new-chat-handoff.prompt.md
   └─ codex-task-prompt.template.md
```

## 4. 推荐同步流程

1. 在公共仓更新通用规则或 guide。
2. 在目标项目读取本仓最新版模板。
3. 对比目标项目的 `AGENTS.md`。
4. 只同步通用部分，不覆盖项目定制部分。
5. 将 connector guide / PR 模板复制到项目仓对应路径。
6. 按目标项目版本规则 bump 版本并记录 changelog。

## 5. 初始来源

本仓初始内容抽取自 `zhou-yang-personal/latam-fbb-desktop` 的治理规则、GitHub connector 操作手册、PR 模板和新会话启动词。

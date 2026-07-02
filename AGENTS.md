# AGENTS.md｜公共治理仓执行入口

本仓库是跨项目 AI 开发治理规则的公共源仓。任何需求设计、文档修改、模板更新、同步任务设计或 GitHub connector 操作，必须先读取本文件；无法读取时必须暂停并要求用户提供文件内容。

## 1. 必须继续读取

执行任何修改前，必须继续读取：

```text
AGENTS.base.md
AGENTS.project.md
README.md
```

如果涉及 GitHub connector 操作，还必须读取：

```text
guides/chatgpt-github-connector-guide.md
```

## 2. 文件职责

```text
AGENTS.base.md     # 跨项目通用规则源文件，同步到项目仓 AGENTS.common.md
AGENTS.project.md  # 本公共治理仓自身的项目定制规则
AGENTS.md          # 固定入口，只负责引导读取和声明优先级
```

## 3. 冲突优先级

```text
用户明确指令 > AGENTS.project.md > AGENTS.base.md > README / templates / prompts > 一般经验
```

## 4. 修改边界

- 可以修改公共治理模板、公共 prompt、connector guide、PR 模板和交接模板。
- 不把单一业务项目的业务口径写入 `AGENTS.base.md`。
- 不把公共规则写成依赖某一个项目目录结构的规则。
- 修改公共规则后，必须检查是否需要同步到项目仓本地副本。
- 涉及 GitHub connector 操作时，必须记录新问题、新限制或更优流程。

## 5. 同步口径

当前账户 `zhou-yang-personal` 下所有可访问开发仓默认纳入治理同步范围；不再维护人工 allowlist。跳过条件以归档、fork、无目标分支、skip marker、权限不足或关键文件不可读为准。

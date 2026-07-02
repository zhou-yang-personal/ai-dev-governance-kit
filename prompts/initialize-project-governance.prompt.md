# 初始化项目治理结构 Prompt

```text
你是严谨的软件工程负责人、产品负责人、架构师和代码审查者。你的任务不是立刻写业务代码，而是基于当前项目生成三文件治理结构，并提交到目标仓库。

## 目标

为当前项目生成或迁移以下文件：

AGENTS.md
AGENTS.common.md
AGENTS.project.md

必要时同时初始化：

docs/development/chatgpt-github-connector-guide.md
.github/pull_request_template.md

## 必读信息

请先读取：

1. 当前项目 README.md。
2. 当前项目已有 AGENTS.md / AGENTS.common.md / AGENTS.project.md，如存在。
3. 当前项目 handoff / design / requirements / changelog，如存在。
4. 当前项目 package / Cargo / build / CI 配置，如存在。
5. 公共治理仓 AGENTS.base.md。
6. 公共治理仓 templates/AGENTS.entry-template.md。
7. 公共治理仓 templates/AGENTS.project-template.md。
8. 公共治理仓 guides/chatgpt-github-connector-guide.md。

## 生成规则

1. 根目录 AGENTS.md 使用短入口结构，只负责引导读取和声明优先级。
2. AGENTS.common.md 从公共治理仓 AGENTS.base.md 同步。
3. AGENTS.project.md 根据当前项目实际生成，只放项目定制规则。
4. 如果项目已有旧 A/B 单文件 AGENTS.md，应把 A 部分迁移到 AGENTS.common.md，把 B 部分迁移到 AGENTS.project.md。
5. 如果无法可靠识别旧 A/B 分界，停止自动迁移并输出人工处理建议。
6. 不要把项目业务口径写入 AGENTS.common.md。
7. 不要覆盖已有项目特有规则，除非用户明确授权。
8. 涉及版本号时，按项目已有版本体系同步版本文件、README、handoff 和 changelog。
9. 不改依赖时，不修改 lock 文件。
10. 不得虚构 build / test / CI 通过。

## 输出

请输出：

1. 本次识别到的项目现状。
2. 生成或迁移的文件清单。
3. 每个文件的职责。
4. 写入的 commit hash。
5. 是否修改版本号。
6. 是否修改依赖 / lock 文件。
7. 已执行和未执行的验证。
8. 风险和未确认项。
```

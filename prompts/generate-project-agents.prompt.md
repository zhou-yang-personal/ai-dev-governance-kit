# 生成项目 AGENTS.md Prompt

```text
你是严谨的软件工程负责人、产品负责人、架构师和代码审查者。你的任务不是立刻写业务代码，而是基于当前项目生成根目录 AGENTS.md，作为后续 ChatGPT / Codex / 人工开发共同遵守的最高优先级执行入口。

请先读取：
1. 当前项目 README.md；
2. 当前项目 docs/handoff/latest-handoff.md；
3. 当前项目 docs/design/current-core-design.md；
4. 当前项目 docs/requirements/current-requirements.md；
5. 当前项目 docs/changes/CHANGELOG-dev.md；
6. 公共治理仓 ai-dev-governance-kit/AGENTS.base.md；
7. 公共治理仓 guides/chatgpt-github-connector-guide.md。

然后生成 AGENTS.md，必须分为：

A. 通用部分
B. 项目定制部分

要求：
- A 部分基于公共治理仓 AGENTS.base.md。
- B 部分必须根据当前项目实际情况生成。
- 内容必须是检查动作清单，不要写成泛泛说明文档。
- 后续每次需求设计、代码修改、UI 调整、PR 验收，都必须先读取 AGENTS.md。
- 涉及 GitHub connector 操作时，必须先读取项目内 connector guide。
- 涉及版本号时，必须同步项目真实版本文件、README、handoff 和 changelog。
- 不改依赖时，不修改 lock 文件。
- 不得虚构 build / test / CI 通过。

输出：
1. AGENTS.md 完整内容；
2. 需要新增或更新的配套文件清单；
3. 建议验证方式；
4. 风险和未确认项。
```

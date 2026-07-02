# Codex 任务 Prompt 模板

```text
你现在在 <project-name> 项目中执行开发任务。开始前必须先读取仓库根目录 AGENTS.md，并按其中检查项执行；若无法读取，必须暂停并要求提供 AGENTS.md 内容。

当前仓库：<owner>/<repo>
目标分支：<target-branch>
任务分支：codex/<task-name>
当前任务：<task-summary>

执行要求：
1. 先读取 AGENTS.md、README.md、handoff、design、requirements、changelog。
2. 只做当前需求相关的最小必要修改，不做无关重构。
3. 涉及版本号时，同步更新项目真实版本文件、README、handoff、changelog 和前端展示版本。
4. 不改依赖时，不修改 lock 文件。
5. 涉及 GitHub connector / Git 操作经验时，检查是否需要更新项目内 connector guide。
6. 修改后执行项目要求的 build / test / check；无法执行时说明原因。
7. 提交信息使用清晰的 conventional style，例如 `fix: ...` / `docs: ...` / `chore: ...`。

交付时必须说明：
- 目标分支和任务分支；
- commit hash；
- 修改文件清单；
- 做了什么；
- 没做什么；
- 是否修改版本号；
- 是否修改依赖 / lock 文件；
- 执行了哪些验证；
- 未验证项和风险。
```

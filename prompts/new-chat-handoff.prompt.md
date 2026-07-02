# 新会话启动 Prompt 模板

将以下内容复制到新会话开头，并替换尖括号占位符。

```text
当前项目为 <project-name>，仓库为 <owner>/<repo>，当前 source-of-truth 分支为 <branch>，当前版本为 <version>。

每次需求设计、代码修改、UI 调整、PR 验收前，必须先读取仓库根目录 AGENTS.md，并继续读取 AGENTS.common.md 和 AGENTS.project.md；若任一文件无法读取，必须先说明缺失情况，不得直接设计或改代码。

涉及 ChatGPT GitHub connector 远端提交、分支、PR、文件写入或版本同步时，必须先读取项目内 GitHub connector guide，按其中能力边界和操作流程执行，不得使用 update_ref 做分支状态探测。

不改依赖时，不要修改 lock 文件。无法执行 build / test / cargo check 等命令时，必须如实标注 not run，不得声称通过。

当前任务背景：
<task-context>

当前已知风险：
<known-risks>
```

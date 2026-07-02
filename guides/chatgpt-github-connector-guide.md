# ChatGPT GitHub Connector 操作手册

本文件记录 ChatGPT 使用 GitHub connector 处理远端仓库文件、分支、提交和 PR 的能力边界与推荐流程。涉及 GitHub 远端提交、分支、PR、文件写入、版本同步时，应先读取本文件。

## 1. 适用范围

- 适用于 ChatGPT 通过 GitHub connector 直接读取或修改 GitHub 仓库的任务。
- 适用于文档、源码、配置、PR 模板、版本文件等 UTF-8 文本文件操作。
- 不替代具体项目的 `AGENTS.md`、产品设计文档、代码规范和用户明确指令。
- 与具体项目 `AGENTS.md` 冲突时，以项目 `AGENTS.md` 和用户明确指令为准。

## 2. 可用能力总览

常用只读能力：

- `get_repo`：读取仓库元信息、默认分支、权限、可合并策略等。
- `fetch_file`：按仓库路径读取 UTF-8 文本文件，并获取当前文件 sha。
- `search`：在仓库内搜索文件、函数、错误文本或关键字。
- `compare_commits`：比较两个 ref / commit 的差异，用于检查分支 ahead / behind、变更文件清单。
- `fetch_commit`：读取单个 commit 的 diff、文件清单和链接。
- `fetch_pr` / `fetch_pr_patch` / `get_pr_diff`：读取 PR 元信息、patch 和 diff。

常用写入能力：

- `create_file`：新增小型 UTF-8 文本文件。
- `update_file`：基于当前 sha 替换已有 UTF-8 文本文件。
- `delete_file`：基于当前 sha 删除已有文件。
- `create_branch`：从指定 base ref 或 commit 创建任务分支。
- `create_pull_request`：创建 PR。

不适合作为常规手段的能力：

- `update_ref`：只用于明确移动分支指针；不得用于分支状态探测、noop 检查或试错。
- `create_blob` / `create_tree` / `create_commit`：仅在需要一次性组合多文件 commit 且已有完整 tree / parent 信息时使用；常规文件修改优先用 `create_file` / `update_file`。

## 3. 推荐流程

1. 用 `get_repo` 确认仓库、默认分支、权限。
2. 用 `compare_commits` 检查分支差异。
3. 用 `fetch_file` 读取 `AGENTS.md`、README、handoff、设计文档、目标文件和 sha。
4. 更新已有文本文件：先 `fetch_file` 获取 sha，再 `update_file`。
5. 新增小文本文件：使用 `create_file`。
6. 每次写入后，必须 `fetch_file` 回读关键片段。
7. 多文件修改必须串行执行，不并发写同一路径。
8. sha 冲突时，重新 `fetch_file` 获取最新内容，重新判断是否继续；不得盲目覆盖。
9. 创建 PR 后，不自动 merge，除非用户明确要求。

## 4. 文件类型规则

| 文件类型 | 推荐操作 | 注意事项 |
|---|---|---|
| Markdown | `fetch_file` + `update_file` / `create_file` | 适合 connector 直接操作 |
| TypeScript / TSX | `fetch_file` + `update_file` | 修改后提示运行前端构建 |
| Rust / TOML | `fetch_file` + `update_file` | 修改后提示运行 Rust 检查 |
| JSON 配置 | 优先最小修改 | 整文件写入可能触发平台拦截；失败后停止说明，不盲试 |
| PR 模板 | `create_file` / `update_file` | 只放确认清单，不复制 AGENTS 全文 |
| lock 文件 | 默认不改 | 只有新增、删除、升级依赖时才改 |
| 大文件 | 优先交给 Codex / 本地 | connector 不适合反复整文件重写 |
| 二进制、图片、DB、安装包、构建产物 | 默认不通过 connector 操作 | 不提交运行数据和构建产物 |

## 5. 常见失败与处理方式

| 失败现象 | 正确处理 |
|---|---|
| `fetch_file` 返回 404 | 记录文件未发现；如需新增，用 `create_file` |
| `create_file` 提示文件已存在 | 改用 `fetch_file` + `update_file` |
| `update_file` sha 冲突 | 重新读取文件和 sha 后再判断 |
| `update_ref` 返回 not fast-forward | 不 force；除非用户明确要求且已说明风险 |
| 平台 safety block | 停止说明被拦截的文件和操作类型；不得多轮盲试 |
| 构建命令无法执行 | 明确写 `not run in ChatGPT GitHub connector environment` |
| CI 未配置或无法读取 | 不声称 CI 通过 |

## 6. 已知踩坑记录

- 2026-07-02：不要使用 `update_ref` 做分支状态探测；使用 `compare_commits` 检查分支差异。
- 2026-07-02：配置类 JSON 整文件更新可能触发平台安全拦截；后续优先最小修改，失败后停止说明。
- 2026-07-02：README 长目录树整文件恢复可能触发拦截；如只是版本号修改，应避免重写整个 README。
- 2026-07-02：GitHub connector 不能运行本地构建命令；交付时必须如实标注未执行。
- 2026-07-02：治理长文整文件更新可能被平台拦截；遇到拦截后应停止盲试，改用更小补充文件、人工补丁、Codex 或本地编辑。

## 7. 交付前自检

- [ ] 已读取项目 `AGENTS.md`。
- [ ] 已读取本文件或项目内副本。
- [ ] 已用 `compare_commits` 检查分支差异，未用 `update_ref` 做探测。
- [ ] 已用 `fetch_file` 获取待更新文件和 sha。
- [ ] 已用 `update_file` 更新已有 UTF-8 文本文件，或用 `create_file` 新增小文本文件。
- [ ] 已逐个回读关键文件确认。
- [ ] 已说明是否创建任务分支 / PR。
- [ ] 已说明是否修改版本号。
- [ ] 已说明是否修改依赖 / lock 文件。
- [ ] 已说明 build / test / cargo check 是否执行。
- [ ] 已说明未验证项和风险。

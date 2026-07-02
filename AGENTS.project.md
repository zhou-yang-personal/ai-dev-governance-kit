# AGENTS.project.md｜AI Dev Governance Kit 项目定制规则

本文件只适用于公共治理仓 `zhou-yang-personal/ai-dev-governance-kit`。本仓是跨项目治理源仓，不承载任何单一业务项目的代码、数据库、UI 或业务口径。

## B0. 项目身份

- [ ] 项目名称已确认：`AI Dev Governance Kit`。
- [ ] 仓库已确认：`zhou-yang-personal/ai-dev-governance-kit`。
- [ ] 默认分支已确认：`main`。
- [ ] 仓库定位已确认：跨项目 AI 协作开发治理公共源仓。

## B1. 本仓核心职责

- [ ] 维护跨项目通用规则源文件：`AGENTS.base.md`。
- [ ] 维护 GitHub connector 操作手册和经验回写机制。
- [ ] 维护项目治理三文件结构模板。
- [ ] 维护 PR、handoff、changelog 和新会话 prompt 模板。
- [ ] 维护每日治理同步任务 prompt。

## B2. 三文件结构口径

项目仓统一采用：

```text
AGENTS.md                 # 固定入口
AGENTS.common.md          # 从本仓 AGENTS.base.md 同步
AGENTS.project.md         # 项目定制规则，不得被每日同步覆盖
```

公共治理仓自身采用：

```text
AGENTS.md                 # 固定入口
AGENTS.base.md            # 公共规则源文件
AGENTS.project.md         # 公共治理仓自身规则
```

## B3. 同步范围规则

- [ ] `zhou-yang-personal` 账户下所有可访问开发仓默认纳入治理同步范围。
- [ ] 不再使用人工 allowlist 作为写入前提。
- [ ] 必须跳过 archived 仓库。
- [ ] 必须跳过 fork 仓库，除非用户单独授权。
- [ ] 必须跳过无目标分支的项目仓。
- [ ] 必须跳过存在 `.governance-sync-ignore` 或 `.github/governance-sync-ignore` 的仓库。
- [ ] 权限不足、关键文件不可读、分界无法识别或 connector 异常时，只记录，不写入。

## B4. 公共规则保护

- [ ] 不把 LATAM FBB、FBB Snapshot、Task Pomodoro 等单项目业务规则写入 `AGENTS.base.md`。
- [ ] 跨项目通用经验可以写入 `AGENTS.base.md`、connector guide、PR 模板或 prompt。
- [ ] 项目特有踩坑只应保留在项目仓 `AGENTS.project.md` 或项目内 guide。
- [ ] 如果一条规则只适用于一个项目，不进入公共规则。

## B5. 交付要求

每次修改本仓后必须说明：

- [ ] 修改目标。
- [ ] 修改文件清单。
- [ ] 是否改变三文件同步口径。
- [ ] 是否改变项目仓写入范围。
- [ ] 是否需要重新同步各项目仓。
- [ ] 是否遇到 GitHub connector 新问题。
- [ ] 未执行 build / test 时如实说明。

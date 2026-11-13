# idea-to-plan

A small, focused collection of two workflow skills for AI coding agents:
**brainstorming** (clarify what to build before building it) and
**writing-plans** (turn an approved design into a bite-sized, test-driven
implementation plan).

## ⚠️ 来源与版权声明

This project is a **derivative work**, extracted and repackaged from
[**obra/superpowers**](https://github.com/obra/superpowers) by Jesse Vincent.

- **Original project:** https://github.com/obra/superpowers
- **Original author:** Jesse Vincent (obra)
- **Original license:** MIT License — see [LICENSE](./LICENSE) (unchanged,
  original copyright notice preserved as required by the MIT license)
- **What was extracted:** only the `brainstorming` and `writing-plans` skills
  from the upstream `skills/` directory. No other skill, script, or asset from
  the upstream project is included.
- **Project name:** renamed for this distribution; the rename does not affect
  the license or the attribution obligations described above.

See [NOTICE.md](./NOTICE.md) for the full attribution statement.

## 包含的两项技能

| 技能 | 用途 |
|------|------|
| `skills/brainstorming` | 在任何创造性工作（建功能、做组件、改行为、做规划）开始前，通过结构化对话澄清用户真正想要的东西，并产出可批准的设计文档 |
| `skills/writing-plans` | 在拿到规格/需求、动手写代码之前，把设计拆解为逐任务、带测试、可独立验证的实施计划 |

## 目录结构

```
idea-to-plan/
├── LICENSE              # 上游原始 MIT 许可证（版权归原作者，未做任何修改）
├── NOTICE.md            # 来源与归属声明
├── README.md
└── skills/
    ├── brainstorming/
    │   ├── SKILL.md
    │   ├── builder-check-prompt.md
    │   ├── visual-companion.md
    │   └── scripts/    # 可视化伴侣服务（frame-template.html、server.cjs 等）
    └── writing-plans/
        └── SKILL.md
```

## 使用方法

将 `skills/` 下的两个目录复制到对应 Agent 平台的 skills 目录（例如
`~/.workbuddy/skills/`），即可按技能名调用。

**注意：** 这两项技能在运行流程中会引用 superpowers 体系中的其他技能
（如 `subagent-driven-development`、`executing-plans`、
`using-git-worktrees`）。本仓库**不包含**这些技能；如需完整工作流，请
直接使用上游仓库 [obra/superpowers](https://github.com/obra/superpowers)。

## 许可证

MIT License，与上游项目一致。版权归原作者 Jesse Vincent 所有，详见
[LICENSE](./LICENSE)。

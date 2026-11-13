# idea-to-plan

一套面向 AI 编码代理的**轻量工作流技能**，只保留两件事，并把它们打磨成可直接落地的闭环：

- **brainstorming**：在动手前，通过结构化对话澄清"真正想要什么、为什么"，产出可批准的设计文档；
- **writing-plans**：把已批准的设计拆解为逐任务、带测试、可独立验证的实施计划，并内置两种执行方式。

本仓库基于对 [obra/superpowers](https://github.com/obra/superpowers) 两项技能的研习与吸收，做了**精选提取 + 优化与个性化**：只保留上述两项技能，并完成自包含化、结构与效率优化，形成可直接使用的版本。优化详情见 [OPTIMIZATIONS.md](./OPTIMIZATIONS.md)。

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

## 优化亮点（相对上游的差异）

本项目在提取的基础上做了以下优化与个性化，使其**自包含、可直接使用**：

| 优化项 | 说明 |
|--------|------|
| **自包含，无外部技能依赖** | 上游 `writing-plans` 的执行交接依赖未包含的 `subagent-driven-development` / `executing-plans` 等技能；本版将两种执行方法**内联**进技能，单独安装即可完整跑通 |
| **命名统一** | 技能内部引用统一改为 `idea-to-plan:` 前缀，文档路径统一为 `docs/idea-to-plan/`，与仓库名自洽 |
| **快速参考入口** | 两个 SKILL.md 顶部新增"快速参考"：核心循环、动工前检查清单，代理与人类都能一眼抓住要点 |
| **设计文档骨架** | brainstorming 内置设计文档模板骨架，产出结构一致、可直接审批的设计文档 |
| **品牌自洽** | 可视化伴侣（浏览器服务）的页脚、标题、会话目录、环境变量全部改为 idea-to-plan，去除上游与第三方品牌残留 |
| **变更可追溯** | 新增 [OPTIMIZATIONS.md](./OPTIMIZATIONS.md)，逐项记录优化内容与理由，便于讲解与评审 |

## 包含的两项技能

| 技能 | 用途 |
|------|------|
| `skills/brainstorming` | 在任何创造性工作（建功能、做组件、改行为、做规划）开始前，通过结构化对话澄清用户真正想要的东西，并产出可批准的设计文档 |
| `skills/writing-plans` | 在拿到规格/需求、动手写代码之前，把设计拆解为逐任务、带测试、可独立验证的实施计划，并内置子代理驱动 / 原生两种执行方式 |

## 目录结构

```
idea-to-plan/
├── LICENSE              # 上游原始 MIT 许可证（版权归原作者，未做任何修改）
├── NOTICE.md            # 来源与归属声明
├── OPTIMIZATIONS.md     # 相对上游的优化变更说明（逐项对照）
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
`~/.workbuddy/skills/`），即可按技能名调用。两项技能**自包含**，无需
额外安装其他技能。

标准工作流：

```
需求/想法
   │  brainstorming（澄清 → 方案 → 设计文档 → 批准）
   ▼
设计文档
   │  writing-plans（拆解任务 → 自检 → 用户审阅 → 执行）
   ▼
实施计划 → 按任务实现
```

## 许可证

MIT License，与上游项目一致。版权归原作者 Jesse Vincent 所有，详见
[LICENSE](./LICENSE)。

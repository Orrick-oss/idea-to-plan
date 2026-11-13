# 优化说明（OPTIMIZATIONS）

本文档记录 **idea-to-plan** 在研习上游项目
[obra/superpowers](https://github.com/obra/superpowers)（Jesse Vincent，MIT License）
两项技能的基础上，所做的优化与个性化修改。目标是在保留上游方法论核心的前提下，
形成**自包含、结构清晰、易于使用与讲解**的个性化版本。

所有修改均在上游 MIT 许可证允许的范围内进行，上游版权与许可声明原样保留。

## 1. 技能引用与命名统一

**上游状态：** 技能内部通过 `superpowers:xxx` 前缀引用其他技能，文档路径
使用 `docs/superpowers/...`。

**优化：** 统一为本项目命名空间——

| 上游引用 | 本版引用 |
|----------|----------|
| `superpowers:writing-plans` | `idea-to-plan:writing-plans` |
| `docs/superpowers/specs/...` | `docs/idea-to-plan/specs/...` |
| `docs/superpowers/plans/...` | `docs/idea-to-plan/plans/...` |

**理由：** 仓库改名后，内部引用与路径应与项目自洽，避免使用方产生
"是否还需要安装 superpowers"的困惑。

## 2. 消除外部技能依赖（自包含化）

**上游状态：** `writing-plans` 的执行交接强制依赖两个未包含在本仓库中的
技能——`superpowers:subagent-driven-development`（子代理驱动执行）与
`superpowers:executing-plans`（原生执行）；并提到 `superpowers:using-git-worktrees`。
单独使用本仓库时，这一交接会断裂。

**优化：**

- 将两种执行方法（**子代理驱动** / **原生执行**）的核心操作要点**内联**
  到 `writing-plans/SKILL.md` 的"Execution Methods"章节，含选择建议与
  通用执行规则；计划文档模板中的"REQUIRED SUB-SKILL"提示改为指向该章节；
- worktree 相关说明改为通用表述（按平台机制创建隔离工作树），不绑定
  特定技能。

**理由：** 本仓库只包含两项技能，使用者无需再安装整套 superpowers 即可
完整跑通"澄清 → 设计 → 计划 → 执行"闭环。这是本版个性化优化的核心价值。

## 3. 快速参考与检查清单

**上游状态：** 两个 SKILL.md 为长文档，无速查入口。

**优化：**

- `brainstorming` 顶部新增"快速参考"：核心循环五步、硬性门禁、对话纪律、
  交棒检查清单；
- `writing-plans` 顶部新增"快速参考"：计划文档解剖、核心原则、动工前
  检查清单。

**理由：** 代理加载技能后可先执行清单再深入细节，减少遗漏；人类评审时
也能快速核对关键门禁是否满足。

## 4. 内置设计文档骨架

**上游状态：** `brainstorming` 仅以要点列表描述设计文档应覆盖的内容。

**优化：** 将要点固化为可直接填写的 Markdown 骨架（Intent & Why /
Goals / Constraints / Approaches / How / Left to the builder），内嵌在
SKILL.md 中。

**理由：** 产出的设计文档结构一致，便于审批与后续计划引用，降低每次
从零组织的成本。

## 5. 可视化伴侣品牌与路径自洽

**上游状态：** 浏览器伴侣服务（`scripts/`）页脚显示 "Superpowers" 品牌
与第三方（Prime Radiant）logo，链接指向上游仓库；会话目录使用
`.superpowers/brainstorm/`；环境变量为 `SUPERPOWERS_DISABLE_TELEMETRY`。

**优化：**

- 页脚改为 "idea-to-plan · Brainstorm Companion"，链接指向本仓库，
  移除第三方 logo；
- 会话目录统一改为 `.idea-to-plan/brainstorm/`（start-server.sh、
  stop-server.sh、visual-companion.md 三处同步）；
- 环境变量改为 `IDEA_TO_PLAN_DISABLE_TELEMETRY`；
- 页面标题改为 "idea-to-plan · Brainstorm Companion"。

**理由：** 避免在分发与使用时出现上游/第三方品牌残留，保持项目整体
品牌一致性。服务功能逻辑未做改动（已通过 Node 语法校验）。

## 6. 文档体系

**优化：**

- `README.md` 新增"优化亮点"总览与标准工作流示意；
- 新增本 `OPTIMIZATIONS.md`，逐项记录优化内容、理由与对照；
- `NOTICE.md` 补充"优化与修改说明"，明确修改的合规边界。

**理由：** 使用方（同事/同学）可以清楚看到"做了什么优化、为什么做、
与上游的关系"，便于讲解与评审。

## 未改动的内容（刻意保留）

以下上游内容**未做修改**，以保证方法论的完整性与有效性：

- 两个技能的核心方法论：对话纪律、硬性门禁、红旗清单、计划结构、
  自检流程、执行交接话术；
- `builder-check-prompt.md` 的构建者检查提示词；
- `visual-companion.md` 的全部操作指南与脚本行为；
- `scripts/` 中服务的全部功能逻辑（仅做品牌字符串替换）。

## 版本

- 优化版本：**1.0.0**（可视化伴侣页脚版本号同步标注）
- 基线：obra/superpowers 的 brainstorming 与 writing-plans 技能

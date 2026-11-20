# idea-to-plan

一套面向 AI 编码代理的**轻量工作流技能**，覆盖"做什么、按什么顺序、怎么做"三个层面，打磨成可直接落地的闭环：

- **brainstorming**：在动手前，通过结构化对话澄清"真正想要什么、为什么"，产出可批准的设计文档；
- **writing-plans**：把已批准的设计拆解为逐任务、带测试、可独立验证的实施计划，并内置两种执行方式；
- **karpathy-guidelines**：贯穿全工作流的行为纪律，四条原则约束"怎么做"，让工作流每一步都有行为约束兜底。

本仓库在**学习**上游项目的基础上做了精选提取 + 优化与个性化：

- 工作流技能（brainstorming、writing-plans）源自 [obra/superpowers](https://github.com/obra/superpowers)（Jesse Vincent，MIT License）；
- 行为纪律技能（karpathy-guidelines）源自 [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills)（MIT License，内容源自 Andrej Karpathy 的观察）。

完成自包含化、结构与效率优化，形成可直接使用的版本。优化详情见 [OPTIMIZATIONS.md](./OPTIMIZATIONS.md)。

## ⚠️ 来源与版权声明

本仓库为**派生作品（derivative work）**，由以下两个上游开源项目提取、整合而来：

**一、工作流技能来源**

提取并再分发自 [**obra/superpowers**](https://github.com/obra/superpowers)，作者 Jesse Vincent。

- **Original project:** https://github.com/obra/superpowers
- **Original author:** Jesse Vincent (obra)
- **Original license:** MIT License — see [LICENSE](./LICENSE) (unchanged,
  original copyright notice preserved as required by the MIT license)
- **What was extracted:** the `brainstorming` and `writing-plans` skills
  from the upstream `skills/` directory. No other skill, script, or asset from
  the upstream project is included.

**二、行为纪律技能来源**

整合自 [**multica-ai/andrej-karpathy-skills**](https://github.com/multica-ai/andrej-karpathy-skills)，
MIT License；其中 `karpathy-guidelines` 的内容源自 Andrej Karpathy 对 LLM 编码误区的观察。

- **Upstream project:** https://github.com/multica-ai/andrej-karpathy-skills
- **Upstream license:** MIT License
- **What was integrated:** the `karpathy-guidelines` skill (four behavioral
  principles), retained as a self-contained third skill.
- **Underlying source:** derived from Andrej Karpathy's observations on LLM
  coding pitfalls.

**命名说明：** 本仓库名称（idea-to-plan）为本分发版本所取的新名称。改名行为不构成对
上游项目主张任何所有权，上述署名要求不受影响。

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
| **行为纪律整合** | 引入第三技能 `karpathy-guidelines`，以四条原则为全工作流提供"怎么做"的行为约束，并在 brainstorming / writing-plans 对应环节加交叉引用，形成工作流骨架与行为纪律互补的整体 |
| **变更可追溯** | 新增 [OPTIMIZATIONS.md](./OPTIMIZATIONS.md)，逐项记录优化内容与理由，便于讲解与评审 |

## 包含的技能

| 技能 | 用途 |
|------|------|
| `skills/brainstorming` | 在任何创造性工作（建功能、做组件、改行为、做规划）开始前，通过结构化对话澄清用户真正想要的东西，并产出可批准的设计文档 |
| `skills/writing-plans` | 在拿到规格/需求、动手写代码之前，把设计拆解为逐任务、带测试、可独立验证的实施计划，并内置子代理驱动 / 原生两种执行方式 |
| `skills/karpathy-guidelines` | 贯穿全工作流的行为纪律：编码前思考、简洁优先、精准修改、目标驱动执行，约束"怎么做"，让工作流每一步都有行为约束兜底 |

三项技能**自包含**，其中 `karpathy-guidelines` 作为行为纪律被前两项技能在对应环节交叉引用，形成有机整体。

## karpathy-guidelines：要解决的问题与原理

`karpathy-guidelines` 并非凭空订立的规则，而是直接针对 LLM 编码中最常见、也最昂贵的几类误区。这些误区由 Andrej Karpathy 系统指出，本技能据此提炼出四条行为原则，让工作流的每一步都有行为约束兜底。

### 要解决的问题

Karpathy 指出，LLM 在编码时普遍存在三类典型误区：

> "模型会替你做出错误假设，然后顺着这个假设一路做下去而不去核对。它们不管理自己的困惑、不寻求澄清、不暴露不一致、不呈现取舍、在该坚持时也不据理力争。"

> "它们特别偏爱把代码和 API 过度复杂化，堆砌臃肿的抽象、不清理死代码……本可 100 行完成的事，却用 1000 行去搭建。"

> "它们有时还会顺带改动或删除自己并未充分理解的注释和代码，哪怕这些内容与当前任务并无关系。"

### 四条原则如何逐一对症

针对上述问题，四条原则各自对症，形成一套直接回应这些误区的行为纪律：

| 原则 | 对症解决的问题 |
|------|----------------|
| **编码前思考（Think Before Coding）** | 错误假设、隐藏困惑、缺少取舍呈现 |
| **简洁优先（Simplicity First）** | 过度复杂、臃肿的抽象 |
| **精准修改（Surgical Changes）** | 越界编辑、碰了不该碰的代码 |
| **目标驱动执行（Goal-Driven Execution）** | 以测试优先、可验证的成功标准获得杠杆 |

**核心洞察：** Karpathy 观察到——

> "LLM 非常擅长循环执行，直到达成特定目标……不要只告诉它做什么，而是给它成功标准，然后看着它完成。"

「目标驱动执行」正是抓住这一点：把指令式的任务，转化为带验证循环的、可验证的目标，让代理能独立循环推进，而无需反复澄清。

### 权衡说明

这套原则**偏向谨慎而非速度**。对于琐碎任务（改个笔误、显而易见的一行改动），运用判断力即可——并非每次改动都需要全套严谨流程。其目标是**降低非平凡工作中代价高昂的错误**，而不是拖慢简单任务。

上述原理与四条原则的完整表述，见 [`skills/karpathy-guidelines/SKILL.md`](./skills/karpathy-guidelines/SKILL.md)。

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
    ├── writing-plans/
    │   └── SKILL.md
    └── karpathy-guidelines/
        └── SKILL.md     # 贯穿全工作流的行为纪律（四条原则）
```

## 使用方法

将 `skills/` 下的三个目录复制到对应 Agent 平台的 skills 目录（例如
`~/.workbuddy/skills/`），即可按技能名调用。三项技能**自包含**，无需
额外安装其他技能。

标准工作流（`karpathy-guidelines` 作为行为纪律贯穿全程）：

```
需求/想法
   │  brainstorming（澄清 → 方案 → 设计文档 → 批准）
   ▼
设计文档
   │  writing-plans（拆解任务 → 自检 → 用户审阅 → 执行）
   ▼
实施计划 → 按任务实现

────────────────────────────────────────────
karpathy-guidelines（编码前思考 · 简洁优先 · 精准修改 · 目标驱动执行）
贯穿上述每一步，约束"怎么做"
```

## 许可证

MIT License，与各上游项目一致。工作流技能版权归原作者 Jesse Vincent 所有；
行为纪律技能源自 multica-ai/andrej-karpathy-skills（MIT License），内容基于
Andrej Karpathy 的观察。详见 [LICENSE](./LICENSE) 与 [NOTICE.md](./NOTICE.md)。

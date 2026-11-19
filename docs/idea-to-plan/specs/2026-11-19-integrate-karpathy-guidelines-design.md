# 整合 karpathy-guidelines 到 idea-to-plan — 设计文档

**日期**：2026-11-19
**状态**：待审阅

## Intent & Why

将 [multica-ai/andrej-karpathy-skills](https://github.com/multica-ai/andrej-karpathy-skills) 中的
`karpathy-guidelines` 技能与现有 idea-to-plan 项目结合，使项目更完善。

该技能提供四条行为原则（编码前思考、简洁优先、精准修改、目标驱动执行），解决"**怎么做**"的行为纪律；
idea-to-plan 现有两个技能解决"**做什么、按什么顺序**"的工作流骨架。两者互补——结合后，
工作流的每一步都有行为约束兜底。采用**方案 A**：作为第三个技能引入，保持自包含，并在现有技能中加交叉引用。

## Goals

- 新增第三个技能 `skills/karpathy-guidelines/SKILL.md`，四条原则原样保留、自包含。
- 在 brainstorming 与 writing-plans 的对应环节加入指向 karpathy-guidelines 的交叉引用，形成有机整体。
- 更新 README、NOTICE、OPTIMIZATIONS，标注新来源与署名。
- 保留上游 MIT 许可与版权归属，合规再分发。

## Non-goals

- 不拆解、不改写四条原则的实质内容。
- 不改变现有两个技能的核心方法论。
- 不引入该仓库其他形态的内容（CLAUDE.md / CURSOR.md / .claude-plugin / .cursor 等面向其他 agent 的配置不纳入——本仓库面向通用 skills 目录，只取 SKILL.md 形态）。

## Anti-goals

- 不要把四条原则拆散塞入现有技能，导致难以同步。
- 不要丢失上游署名或许可。
- 不要让新技能依赖未包含的外部资源。

## Constraints

- **署名合规**：保留 MIT 许可；NOTICE / README 标注来源 `multica-ai/andrej-karpathy-skills`；指南源自 Andrej Karpathy 的观察。
- **命名统一**：技能目录名 `karpathy-guidelines`；交叉引用使用 `idea-to-plan:karpathy-guidelines` 前缀。
- **内容自包含**：新技能不引用未包含的外部技能。

## Approaches

- **方案 A（已选）：作为第三个技能引入 + 交叉引用。**
  取舍：技能自包含、结构清晰、四条原则整体保留、后续好同步；代价是技能从 2 个变 3 个。
- **方案 B（未选）：拆解并入现有两个技能。**
  取舍：集成度最高、维持两技能闭环；代价是改动上游内容多、原则被拆散、难同步。
- **方案 C（未选）：仅作全局说明写进 README。**
  取舍：最轻；代价是不具备技能形态、无法被代理加载，整合最浅。

## How（已定部分）

1. **新增技能文件** `skills/karpathy-guidelines/SKILL.md`：
   - frontmatter：`name: karpathy-guidelines`，`description` 保留原意，`license: MIT`。
   - 正文：四条原则原样保留（编码前思考、简洁优先、精准修改、目标驱动执行），保留 Karpathy 观察的出处链接。
   - 顶部加一行定位说明：本技能属于 idea-to-plan，作为贯穿全工作流的行为纪律。

2. **交叉引用**：
   - `brainstorming/SKILL.md`：在澄清 / 设计环节（对应"编码前思考"）加引用，指向 `idea-to-plan:karpathy-guidelines`，强调不假设、呈现权衡、主动提问。
   - `writing-plans/SKILL.md`：在计划与执行环节（对应"简洁优先""精准修改""目标驱动执行"）加引用，强调可验证成功标准、最小实现、精准改动。

3. **文档更新**：
   - `README.md`：技能列表增加第三项；目录结构增加 `karpathy-guidelines`；标准工作流体现行为纪律贯穿；来源章节标注新来源。
   - `NOTICE.md`：新增 karpathy-guidelines 的归属声明（来源仓库、作者、MIT 许可、源自 Karpathy 观察）。
   - `OPTIMIZATIONS.md`：新增一节记录本次整合（整合内容、理由、交叉引用设计）。

## Left to the builder

- 交叉引用插入的具体章节位置，由实现时对齐现有文档结构确定。
- 新技能文件顶部定位说明的具体措辞可微调。

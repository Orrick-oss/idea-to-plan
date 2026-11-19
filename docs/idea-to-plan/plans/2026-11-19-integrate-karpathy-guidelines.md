# 整合 karpathy-guidelines 到 idea-to-plan 实施计划

> **For agentic workers:** Implement this plan task-by-task, tracking steps with checkbox (`- [ ]`) syntax. Choose the execution method with the user before starting: subagent-driven (fresh worker + reviewer per task) or native (in-session, final review).

**Goal:** 将 `multica-ai/andrej-karpathy-skills` 的 `karpathy-guidelines` 作为第三个技能引入 idea-to-plan，并加交叉引用与文档署名，形成"工作流骨架 + 行为纪律"互补的整体。

**Architecture:** 新增独立技能文件保持四条原则自包含、原样保留；在现有两个 SKILL.md 的对应环节加 `idea-to-plan:karpathy-guidelines` 交叉引用；README / NOTICE / OPTIMIZATIONS 三处文档同步更新来源与署名。

**Tech Stack:** 纯 Markdown 文档（技能文件 + 项目文档），无代码依赖。

**Spec:** [docs/idea-to-plan/specs/2026-11-19-integrate-karpathy-guidelines-design.md](../specs/2026-11-19-integrate-karpathy-guidelines-design.md)

## 全局约束

- **署名合规**：保留 MIT 许可；README / NOTICE 标注来源仓库 `multica-ai/andrej-karpathy-skills`；指南源自 Andrej Karpathy 的观察（含其 X 推文链接）。
- **命名统一**：技能目录名 `karpathy-guidelines`；所有交叉引用使用 `idea-to-plan:karpathy-guidelines` 前缀。
- **内容自包含**：新技能不引用任何未包含在本仓库的外部技能。
- **原样保留**：四条原则（Think Before Coding / Simplicity First / Surgical Changes / Goal-Driven Execution）的实质内容不拆解、不改写。
- **提交方式**：本机 `github.com:443` 不可直连，无法 `git push`；全部任务完成后用 `node D:/Tools/publish-idea-to-plan.js` 统一推送一次，保持 Commits 历史干净（单个整合提交）。

## 文件结构

| 文件 | 操作 | 职责 |
|------|------|------|
| `skills/karpathy-guidelines/SKILL.md` | 创建 | 第三条行为纪律技能，四条原则原样保留 |
| `skills/brainstorming/SKILL.md` | 修改 | 澄清/设计环节加交叉引用（对应"编码前思考"） |
| `skills/writing-plans/SKILL.md` | 修改 | 计划/执行环节加交叉引用（对应简洁/精准/目标驱动） |
| `README.md` | 修改 | 技能列表、目录结构、工作流、来源章节 |
| `NOTICE.md` | 修改 | 新增 karpathy-guidelines 归属声明 |
| `OPTIMIZATIONS.md` | 修改 | 新增整合记录一节 |

## Review Focus

文档类任务无单元测试，以下为最可能出问题的五个失败模式，各自对应任务的验证步骤：

1. **四条原则被改写或遗漏** → Task 1 逐条核对四条原则标题与核心要点完整、未被改写。
2. **交叉引用前缀写错**（误用 `superpowers:` 或漏 `idea-to-plan:`）→ Task 2、Task 3 用 grep 校验引用字符串精确为 `idea-to-plan:karpathy-guidelines`。
3. **署名遗漏**（README/NOTICE 未标注新来源或 MIT）→ Task 4 grep 校验三处文档均出现来源与许可。
4. **frontmatter 字段不全**（缺 `name`/`description`/`license`）→ Task 1 校验三个字段齐全且值正确。
5. **引入外部依赖**（新技能引用未包含技能）→ Task 1 校验新技能正文不引用任何外部技能名。

---

### Task 1: 新增 karpathy-guidelines 技能文件

**Files:**
- Create: `skills/karpathy-guidelines/SKILL.md`

**Interfaces:**
- Consumes: 上游原文（四条原则，已取得，内容见下）；设计文档 Constraints。
- Produces: 可供 Task 2、Task 3 交叉引用的技能 `idea-to-plan:karpathy-guidelines`。

**上游原文要点（原样保留，实现时以此为准）：**

frontmatter：
```
name: karpathy-guidelines
description: Behavioral guidelines to reduce common LLM coding mistakes. Use when writing, reviewing, or refactoring code to avoid overcomplication, make surgical changes, surface assumptions, and define verifiable success criteria.
license: MIT
```

正文四条原则（标题与核心要点原样保留，不改写）：
1. **Think Before Coding** — Don't assume. Don't hide confusion. Surface tradeoffs.
2. **Simplicity First** — Minimum code that solves the problem. Nothing speculative.
3. **Surgical Changes** — Touch only what you must. Clean up only your own mess.
4. **Goal-Driven Execution** — Define success criteria. Loop until verified.

开头保留出处说明（derived from Andrej Karpathy's observations，附 X 链接
`https://x.com/karpathy/status/2015883857489522876`），保留 **Tradeoff** 提示（bias toward caution over speed）。

- [ ] **Step 1: 创建 `skills/karpathy-guidelines/SKILL.md`**

frontmatter 三个字段（`name: karpathy-guidelines`、`description` 用上文原文、`license: MIT`）原样写入。正文四条原则原样保留（标题、加粗要点、列表要点均照上游原文），开头保留出处与 Tradeoff 说明。在正文顶部（`# Karpathy Guidelines` 标题之后、出处说明之前）加一行定位说明，标明本技能属于 idea-to-plan、作为贯穿全工作流的行为纪律。**定位说明措辞可由实现者微调，但必须明确"属于 idea-to-plan"且"贯穿全工作流"。**

- [ ] **Step 2: 验证 frontmatter 字段齐全**

Run: `grep -nE '^(name|description|license):' skills/karpathy-guidelines/SKILL.md`
Expected: 输出三行，分别为 `name: karpathy-guidelines`、`description: ...`、`license: MIT`。

- [ ] **Step 3: 验证四条原则原样保留且未被改写**

Run: `grep -nE 'Think Before Coding|Simplicity First|Surgical Changes|Goal-Driven Execution' skills/karpathy-guidelines/SKILL.md`
Expected: 输出四行，四条原则标题均在，顺序与上游一致。

- [ ] **Step 4: 验证出处链接与自包含性**

Run: `grep -n 'x.com/karpathy' skills/karpathy-guidelines/SKILL.md`
Expected: 命中出处链接。再通读全文，确认正文未引用任何本仓库未包含的外部技能（无 `idea-to-plan:` 前缀之外的技能引用）。

- [ ] **Step 5: 记录任务完成**

确认本任务全部验证通过，标记 Task 1 完成，进入 Task 2。

---

### Task 2: brainstorming 交叉引用

**Files:**
- Modify: `skills/brainstorming/SKILL.md`

**Interfaces:**
- Consumes: Task 1 产出的技能 `idea-to-plan:karpathy-guidelines`。
- Produces: 澄清/设计环节对行为纪律的引用，供使用方理解"编码前思考"贯穿 brainstorming。

- [ ] **Step 1: 在澄清/设计环节加交叉引用**

在 `skills/brainstorming/SKILL.md` 正文的 **"Lay out the approaches"** 段落之后（该段讲呈现方案与取舍，对应"编码前思考"的"呈现权衡"），加一句引用，指向 `idea-to-plan:karpathy-guidelines`，强调 brainstorming 全程遵循"不假设、呈现权衡、主动提问"的纪律。**具体位置可在"快速参考"的"交棒检查清单"或正文该段二者中择一，以贴合现有结构、不破坏阅读节奏为准。**

- [ ] **Step 2: 验证引用字符串精确**

Run: `grep -n 'idea-to-plan:karpathy-guidelines' skills/brainstorming/SKILL.md`
Expected: 至少命中一处，且引用前缀精确为 `idea-to-plan:karpathy-guidelines`（无 `superpowers:` 等错误前缀）。

- [ ] **Step 3: 记录任务完成**

确认引用位置合理、前缀正确，标记 Task 2 完成，进入 Task 3。

---

### Task 3: writing-plans 交叉引用

**Files:**
- Modify: `skills/writing-plans/SKILL.md`

**Interfaces:**
- Consumes: Task 1 产出的技能 `idea-to-plan:karpathy-guidelines`。
- Produces: 计划与执行环节对行为纪律的引用，对应"简洁优先 / 精准修改 / 目标驱动执行"。

- [ ] **Step 1: 在计划与执行环节加交叉引用**

在 `skills/writing-plans/SKILL.md` 的 **"快速参考"** 部分，紧接"核心原则：DRY · YAGNI · TDD · 频繁提交"那条之后，加一句引用，指向 `idea-to-plan:karpathy-guidelines`，强调写计划与执行时遵循"简洁优先、精准修改、目标驱动执行"——最小实现、只碰必须碰的、定义可验证成功标准。

- [ ] **Step 2: 验证引用字符串精确**

Run: `grep -n 'idea-to-plan:karpathy-guidelines' skills/writing-plans/SKILL.md`
Expected: 至少命中一处，前缀精确为 `idea-to-plan:karpathy-guidelines`。

- [ ] **Step 3: 记录任务完成**

确认引用位置合理、前缀正确，标记 Task 3 完成，进入 Task 4。

---

### Task 4: 文档更新（README + NOTICE + OPTIMIZATIONS）

**Files:**
- Modify: `README.md`
- Modify: `NOTICE.md`
- Modify: `OPTIMIZATIONS.md`

**Interfaces:**
- Consumes: Task 1 产出的技能；设计文档 Goals 中"更新 README、NOTICE、OPTIMIZATIONS，标注新来源与署名"。
- Produces: 三处文档完整标注 karpathy-guidelines 来源与整合记录。

- [ ] **Step 1: 更新 `README.md`**

四处改动：
1. **技能列表**（"包含的两项技能"一节）：标题改为"包含的技能"，表格新增第三行 `skills/karpathy-guidelines`，说明其为贯穿全工作流的行为纪律（四条原则）。
2. **目录结构**：`skills/` 下新增 `karpathy-guidelines/`（含 `SKILL.md`）。
3. **标准工作流**：在工作流示意或其说明中，体现行为纪律贯穿全程（指向 karpathy-guidelines）。
4. **来源章节**：在"来源与版权声明"一节补充 karpathy-guidelines 的来源（`multica-ai/andrej-karpathy-skills`，MIT，源自 Karpathy 观察）。

- [ ] **Step 2: 更新 `NOTICE.md`**

在"来源与归属声明"中新增 karpathy-guidelines 的归属条目：上游仓库 `multica-ai/andrej-karpathy-skills`、MIT 许可、指南源自 Andrej Karpathy 的观察；并同步更新"提取范围"说明本仓库纳入了第三个技能。

- [ ] **Step 3: 更新 `OPTIMIZATIONS.md`**

新增一节（编号顺延为第 7 节，或置于"未改动的内容"之前），记录本次整合：整合内容（引入第三技能 + 交叉引用）、理由（工作流骨架与行为纪律互补）、交叉引用设计。更新末尾"版本"信息，体现本次整合。

- [ ] **Step 4: 验证三处文档均标注来源与许可**

Run: `grep -nE 'karpathy-guidelines|multica-ai/andrej-karpathy-skills' README.md NOTICE.md OPTIMIZATIONS.md`
Expected: 三个文件各自命中，README 与 NOTICE 命中来源仓库 `multica-ai/andrej-karpathy-skills`，OPTIMIZATIONS 命中整合记录。

- [ ] **Step 5: 记录任务完成**

确认三处文档更新完整、来源与署名无遗漏，标记 Task 4 完成。

---

### 统一推送与验证

所有任务完成后执行一次：

- [ ] **Step 1: 推送到远程**

Run: `node D:/Tools/publish-idea-to-plan.js`
Expected: 脚本计算本地与远程树差异，生成提交并更新 `main`，输出成功且树校验通过。

- [ ] **Step 2: 验证远程结果**

通过 GitHub 连接器或 API 核对远程 `skills/karpathy-guidelines/SKILL.md` 存在、README/NOTICE/OPTIMIZATIONS 更新到位、Commits 历史为单个整合提交。

## Self-Review

- **Spec coverage**：设计文档 Goals 四项（新增技能 / 交叉引用 / 文档更新 / 合规署名）分别由 Task 1、Task 2+3、Task 4、全局约束 + Task 4 覆盖，无遗漏。
- **Step scan**：每个步骤给出唯一合理做法与可检查的验证命令，无"TBD"式空话。
- **Type consistency**：交叉引用前缀统一为 `idea-to-plan:karpathy-guidelines`，Task 2/3/4 一致。
- **Review Focus**：五个失败模式均对应到 Task 1/2/3/4 的验证步骤。
- **Proportion**：计划聚焦决策与验证，未转录上游全文，篇幅与设计文档相称。

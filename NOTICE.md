# 来源与归属声明 (Notice of Attribution)

本仓库（**idea-to-plan**）是基于以下上游开源项目派生（derivative work）与整合的：

## 一、工作流技能来源

- **上游项目名称：** superpowers
- **上游仓库地址：** https://github.com/obra/superpowers
- **原作者：** Jesse Vincent（GitHub: [obra](https://github.com/obra)）
- **上游许可证：** MIT License

## 二、行为纪律技能来源

- **上游项目名称：** andrej-karpathy-skills
- **上游仓库地址：** https://github.com/multica-ai/andrej-karpathy-skills
- **上游许可证：** MIT License
- **内容来源：** 其中的 `karpathy-guidelines` 技能源自 Andrej Karpathy 对 LLM
  编码误区的观察

## 提取与整合范围

本仓库从上述上游项目中取得以下技能作为内容基础：

1. `skills/brainstorming`（含 `SKILL.md`、`builder-check-prompt.md`、
   `visual-companion.md` 及其 `scripts/` 目录）——提取自 superpowers
2. `skills/writing-plans`（含 `SKILL.md`）——提取自 superpowers
3. `skills/karpathy-guidelines`（含 `SKILL.md`，四条行为原则）——整合自
   andrej-karpathy-skills

上游的其他技能、脚本与资产均未包含在本仓库中。

## 优化与修改说明

本仓库并非对上游内容的简单复制，而是在提取与整合的基础上进行了优化修改，
包括：统一内部引用与文档路径命名、将执行方法内联以消除对未包含技能的
外部依赖、增加快速参考与检查清单、内置设计文档骨架、统一可视化伴侣的
品牌与目录命名、引入 `karpathy-guidelines` 作为贯穿全工作流的行为纪律并在
两个工作流技能对应环节加交叉引用等。优化的逐项内容与理由记录于
[OPTIMIZATIONS.md](./OPTIMIZATIONS.md)。

上述修改均在原作者 MIT 许可证允许的"复制、修改、合并、发布"权利范围内
进行，不改变原作品的版权归属。

## 命名说明

本仓库名称（idea-to-plan）为本分发版本所取的新名称。改名行为不构成对
上游项目主张任何所有权，本声明及原始许可证中的署名要求不受影响。

## 许可证义务

各上游项目均采用 MIT License。按该许可证要求，本仓库完整保留了上游原始的
[LICENSE](./LICENSE) 文件（含原作者版权信息），且本声明随全部副本分发。

MIT License 原文规定：上述版权声明与许可声明须包含于本软件所有副本或实质
性部分中。

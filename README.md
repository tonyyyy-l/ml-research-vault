# ML Research Vault Agent

## 致谢

> 本项目基于 [juliye2025/evil-read-arxiv](https://github.com/juliye2025/evil-read-arxiv) 构建，并根据个人的 ML 论文阅读流程，对工作流、知识库结构和 agent 指令做了一些个性化调整。

这是一个基于 Obsidian 笔记库的 ML 论文学习工作区。它把论文笔记、每日论文推荐、知识图谱数据，以及面向 Claude Code/Codex 的学习助手规则放在同一个仓库里，方便持续积累和迁移。

## 目录结构

```text
.
├── CLAUDE.md                 # Claude Code/Codex 的主工作流说明
├── AGENTS.md                 # Codex 入口说明，指向 CLAUDE.md
├── skills/                   # 论文阅读工作流技能和脚本
│   ├── start-my-day/         # 每日论文推荐
│   ├── paper-analyze/        # 单篇论文深度分析
│   ├── paper-search/         # 笔记内论文搜索
│   ├── extract-paper-images/ # 从论文源码/PDF 提取图片
│   ├── ml-tutor/             # 基于 vault 的 ML 问答
│   ├── ml-note/              # 把新理解追加到论文笔记
│   └── ml-roadmap/           # 基于现有笔记规划阅读路线
└── Research Vault/           # Obsidian vault
    ├── 5_Daily/              # 每日论文推荐
    ├── 20_Research/
    │   ├── Papers/           # 按领域分类的论文深度笔记
    │   └── PaperGraph/       # 论文关系图谱数据
    ├── 30_QA/                # 半自动沉淀的 ML 问答笔记
    └── 99_System/Config/     # 研究兴趣和工作流配置
```

## 快速开始

1. 用 Obsidian 打开 `Research Vault/`。
2. 在 Claude Code 或 Codex 中打开本仓库根目录。
3. 如需显式指定 vault 路径，可设置：

```bash
export OBSIDIAN_VAULT_PATH="$PWD/Research Vault"
```

4. 直接用自然语言提问，例如：
   - `Transformer 的 QKV 是什么？`
   - `我发现 RLHF 的核心其实是 reward model + PPO`
   - `帮我规划 Attention 机制的学习路线`

## Agent 工作流

- `start-my-day`: 搜索 arXiv 并生成每日论文推荐。
- `paper-analyze`: 深度分析单篇论文，生成图文笔记并维护知识图谱。
- `paper-search`: 在已有论文笔记中搜索相关内容。
- `extract-paper-images`: 从 arXiv 源码包或 PDF 中提取论文图片。
- `ml-tutor`: 先搜索 `Research Vault`，基于你的论文笔记回答 ML 概念、方法和论文关系问题；笔记不够时再补充外部知识。
- `qa-capture`: 半自动沉淀高价值问答。回答后先询问是否保存，确认后再整理进 `Research Vault/30_QA/`。
- `ml-note`: 当你总结新理解时，自动寻找相关论文笔记，只追加到合适 section，不覆盖原文。
- `ml-roadmap`: 当你想系统学习一个方向时，扫描现有笔记，按时间和依赖关系规划不超过 10 篇论文的阅读路线，并标出缺失论文。

## 上传前检查

`.gitignore` 已排除 macOS 临时文件、Obsidian 本地工作区状态、环境变量文件、依赖缓存和 PDF 原文。公开上传前建议再人工确认：

- `Research Vault/` 中是否有不想公开的私人笔记。
- `Research Vault/99_System/Config/` 中是否包含私人偏好或账号信息。
- 图片是否适合随笔记一起公开。

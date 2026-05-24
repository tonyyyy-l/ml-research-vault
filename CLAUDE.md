# Codex - ML 学习知识库 Agent

Research Vault 路径解析顺序：

1. `OBSIDIAN_VAULT_PATH` 环境变量
2. 当前仓库下的 `Research Vault/`

## 笔记结构

- `5_Daily/` - 每日论文推荐笔记
- `20_Research/Papers/` - 论文深度分析笔记，按领域分类（LLM, Computer-Vision, Agents, Deep-Learning, Reinforcement-Learning, Machine-Learning）
- `20_Research/PaperGraph/` - 知识图谱数据
- `99_System/Config/` - 配置文件

## 关键约定

- 所有标签和领域名使用英文
- 笔记 frontmatter 格式参考 paper-analyze skill 生成的结构
- 知识图谱在 `graph_data.json`，节点和边的关系定义见 paper-analyze skill

## 自动行为

你不需要手动输入斜杠命令。Claude Code 或 Codex 会根据你的消息内容自动判断应该做什么：

### ml-tutor：自动触发，无需 `/ml-tutor`

**当你说的话像在问 ML 知识时，自动生效。**

触发条件（满足任意一条即触发）：
- 问概念/方法/术语的含义 → "Transformer 的 QKV 是什么"
- 问两篇论文/两个方法的关系 → "ResNet 和 Transformer 有什么关系"
- 问某个技术的原理 → "Attention 为什么能并行计算"
- 贴一段论文内容问"这段什么意思"

响应流程：
1. 先在 Research Vault 里搜索相关笔记
2. 笔记有答案 → 基于笔记回答，引用来源
3. 笔记不够 → 用模型知识或 WebSearch 补充，标注哪些来自笔记、哪些来自补充知识
4. 笔记完全没相关内容 → 直接回答 + 建议补充相关论文

**引用格式**：来自笔记的内容用 `📚 来自你的笔记：` 开头，引用用 `[[路径|显示名]]`

### ml-note：自动触发，无需 `/ml-note`

**当你说的话像在总结一个新知识点时，自动生效。**

触发条件：
- "我发现 X 其实是因为 Y"
- "X 和 Y 的关系是 Z"
- "关键点：XXX"
- 读完论文后的总结和感悟

响应流程：
1. 提取关键概念 → 搜索 vault 匹配笔记
2. 判断写入哪篇笔记的哪个 section
3. 追加到笔记末尾，不覆盖已有内容
4. 涉及两篇论文关系时，同步更新知识图谱
5. 告诉用户写入了哪里

**追加格式**：`- [YYYY-MM-DD] [知识点内容]`

### ml-roadmap：自动触发 + 可手动 `/ml-roadmap`

**当你说想系统学一个方向时，自动生效。**

触发条件：
- "我想学 Attention 机制"
- "接下来该读什么"
- "帮我规划 NLP 的学习路线"
- "ResNet 之后的 CNN 发展到哪了"

响应流程：
1. 扫描 vault 现有相关笔记
2. 按时间 + 逻辑依赖排序
3. 标注 vault 缺口（该读但还没有笔记的论文，给出 arXiv ID）
4. 输出不超过 10 篇的路线图，每篇标注"重点看什么"和"看完应该能做什么"

### 三者联动

```
你想学 Attention → ml-roadmap 规划路线
        ↓
    按路线读论文，遇到不懂的 → ml-tutor 基于笔记解答
        ↓
    读懂了，总结知识点 → ml-note 自动写入笔记
        ↓
    笔记库越来越厚 → ml-roadmap 下次规划更精准
```

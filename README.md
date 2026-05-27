# 📄 Paper Skill

学术论文总结工具，提供两种使用方式：作为 **Pi Skill** 自动触发，或作为 **Pi Prompt Template** 手动调用。

## 功能

将学术论文按研究思路拆解为以下模块，生成结构化的中文总结：

- 📄 基本信息（标题、作者、venue）
- 🌍 研究背景
- ❓ 研究问题
- 💡 核心思路与技术方案
- 🔬 实验设计与结果
- 📊 效果评估
- 🏆 主要贡献
- 🔗 与已有工作的关系
- 💬 个人评价
- 📌 一句话总结

## 支持的输入

| 输入类型 | 示例 |
|---------|------|
| 本地文件路径 | `~/papers/attention.pdf` |
| URL | `https://arxiv.org/abs/1706.03762` |
| 主题关键词 | `大语言模型` |

## 文件结构

```
paper-skill/
├── skills/
│   └── paper/
│       └── SKILL.md      # Skill 定义 — Pi 自动加载，含工具调用指令
├── prompts/
│   └── paper.md          # Prompt 模板 — 通过 /paper 手动调用
└── README.md
```

## 使用方式

### 方式一：作为 Skill（自动触发）

**安装 Skill**：

```bash
# 克隆后，将 skills/paper/ 目录复制到 Pi 的 skills 目录
git clone git@github.com:Youpen-y/paper-skill.git
cp -r paper-skill/skills/paper ~/.pi/agent/skills/paper
```

安装后，Pi 会根据 `SKILL.md` 中的 `description` 自动匹配用户意图：

```
总结一下这篇论文 ~/papers/attention.pdf
分析这篇 paper：https://arxiv.org/abs/1706.03762
论文综述 大语言模型
```

**Skill 特点**：
- 自动识别输入类型（文件 / URL / 关键词）并执行相应操作
- 包含完整的工具调用指令（`read` 读文件、`bash` + `curl` 下载 URL 等）
- 通过 `$@` 接收用户输入

### 方式二：作为 Prompt Template（手动调用）

**安装 Prompt Template**：

```bash
# 将 prompts/paper.md 复制到 Pi 的全局 prompts 目录
mkdir -p ~/.pi/agent/prompts
cp paper-skill/prompts/paper.md ~/.pi/agent/prompts/paper.md
```

安装后，在 Pi 编辑器中输入 `/paper` 加参数：

```
/paper ~/papers/attention.pdf
/paper https://arxiv.org/abs/1706.03762
```

**Template 特点**：
- 纯提示词，展开为结构化输出指令
- 无自动工具调用能力，需手动提供内容
- 适合在已有论文内容的场景下使用

> 两种方式使用相同的输出结构，区别在于 Skill 模式包含工具调用能力（自动读文件/下载），Template 模式仅展开为纯提示词。

## 两个文件的区别

| | `skills/paper/SKILL.md` | `prompts/paper.md` |
|---|---|---|
| **用途** | Pi Skill（自动触发） | Prompt Template（手动调用） |
| **触发方式** | Pi 根据描述自动匹配 | 编辑器中输入 `/paper` |
| **Frontmatter** | `name` + `description` | `description` + `argument-hint` |
| **工具调用** | ✅ 含 `read`/`bash` 指令 | ❌ 纯提示词 |
| **参数** | `$@` | `$@` |

## 输出要求

- 中文输出，关键术语保留英文
- 通俗易懂但不失严谨
- 篇幅控制在 1500-2500 字
- 如有开源代码/数据，指出链接

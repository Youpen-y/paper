# 📄 Paper Skill

学术论文总结工具，基于 [Pi Agent Skills](https://agentskills.io/specification) 标准。

## 功能

将学术论文按研究思路拆解为以下模块，生成结构化的中文总结：

- 基本信息（标题、作者、venue）
- 研究背景
- 研究问题
- 核心思路与技术方案
- 实验设计与结果
- 效果评估
- 主要贡献
- 与已有工作的关系
- 个人评价
- 一句话总结

## 支持的输入

| 输入类型 | 示例 |
|---------|------|
| 本地文件路径 | `~/papers/attention.pdf` |
| URL | `https://arxiv.org/abs/1706.03762` |
| 主题关键词 | `大语言模型` |

## 安装

克隆仓库到 Pi 的 skill 目录：

```bash
git clone git@github.com:Youpen-y/paper-skill.git ~/.pi/agent/skills/paper
```

## 使用

在 Pi 中直接说：

```
总结一下这篇论文 ~/papers/attention.pdf
```

或使用命令：

```
/skill:paper ~/papers/attention.pdf
```

## 文件结构

```
paper-skill/
├── SKILL.md    # Skill 定义（Pi 自动加载）
├── paper.md    # prompt 模板
└── README.md   # 本文件
```

## 输出要求

- 中文输出，关键术语保留英文
- 通俗易懂但不失严谨
- 篇幅控制在 1500-2500 字

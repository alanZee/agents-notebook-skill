# agents-notebook-skill

面向 LLM 代理的持久化知识笔记本。跨对话捕获重要事实、决策和发现，防止有价值的信息因上下文窗口满溢而丢失。

## 功能

- **主动记录**：用户提及偏好、约束、纠正或发现时自动触发
- **智能评估**：每条信息经过持久性、独特性、可操作性三重评估后才记录
- **自动维护**：写入前检查重复与冲突，保持笔记连贯无矛盾
- **项目注册**：首次使用时自动在项目的 `AGENTS.md` 和 `CLAUDE.md` 中注册

## 安装

将 `agents-notebook-skill/` 目录复制到你的 skills 文件夹，或通过 skill 管理器安装。

## 工作原理

LLM 获得新的事实性信息时：

1. **评估**：是否持久、独特、可操作？
2. **读取**：检查已有笔记是否重复或冲突
3. **写入**：记录到项目根目录的 `.agents-notebooks/<主题>.md`

触发方式：显式命令（"记住"、"记一下"）、隐式发现（API 限制、领域洞察）、纠正（"其实是 X"）。

## 文件结构

```
.agents-notebooks/
  INDEX.md              # 文件索引（笔记本增长后维护）
  user-preferences.md   # 按主题组织的笔记文件
  api-constraints.md
  ...
```

## 目录结构

```
agents-notebook-skill/
├── SKILL.md                    # 英文版技能定义
├── SKILL_CN.md                 # 中文版技能定义
├── README.md                   # 英文说明
├── README_CN.md                # 中文说明（本文件）
└── references/
    ├── evaluation-guide.md     # 详细评估标准
    └── registration-template.md # 项目注册模板
```

## 许可证

MIT

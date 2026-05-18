# File Structure & Naming / 文件结构与命名规范

## Directory Layout / 目录布局

```
.agents-notebooks/
  INDEX.md              # one-line summary per file (maintain when notebook grows beyond 10 files)
                        # 每个文件一行摘要（笔记本超过 10 个文件时维护）
  user-preferences.md   # topic-based files / 按主题组织的文件
  api-constraints.md
  fluid-sim/            # subdirectory for complex topics (use when 5+ notes on one topic)
                        # 复杂主题的子目录（一个主题 5+ 条笔记时使用）
    numerics.md
    boundary-conditions.md
```

## File Naming / 文件命名

- Pattern: `<topic-slug>.md` — lowercase, hyphens, descriptive
- 格式：`<主题词>.md` —— 小写、连字符、有描述性
- Examples / 示例：`user-preferences.md`, `api-constraints.md`, `key-decisions.md`

## Subdirectory Rules / 子目录规则

- **Default**: flat files in `.agents-notebooks/`
- **When to add subdirectories**: only when a single topic naturally splits into 5+ distinct notes
- **Don't over-organize early**: let structure emerge from need
- **默认**：平铺文件
- **何时加子目录**：仅当一个主题自然分为 5+ 个独立笔记时
- **不要过早组织**：让结构从需求中涌现

## INDEX.md Format / INDEX.md 格式

Maintain when notebook grows beyond 10 files. One line per entry:

当笔记本超过 10 个文件时维护。每个条目一行：

```markdown
# Notebook Index / 笔记本索引

- user-preferences.md — coding style, tool choices / 编码风格、工具选择
- api-constraints.md — external API limits / 外部 API 限制
- fluid-sim/ — numerical methods, boundary conditions / 数值方法、边界条件
```

## Note Format / 笔记格式

```markdown
# Topic Title / 主题标题

## YYYY-MM-DD — Brief heading / 简短描述性标题

Clear, concise statement of the fact or insight. 1-3 sentences max.

Source: [user / research / reasoning / synthesis]
来源：[用户告知 / 自行查阅 / 推理 / 归纳总结]
```

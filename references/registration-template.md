# Project Registration Template / 项目注册模板

When the notebook skill creates its first note in a project, it must register itself in the project's `AGENTS.md` and `CLAUDE.md` (create them if they don't exist). This makes the notebook discoverable by other sessions and agents.

当笔记本技能在项目中创建第一条笔记时，必须在项目的 `AGENTS.md` 和 `CLAUDE.md` 中注册自身（如文件不存在则先创建）。这使笔记本可被其他会话和代理发现。

---

## Registration Marker / 注册标记

Search for this exact marker to detect whether registration already exists:

用以下精确标记检测是否已注册：

```
<!-- notebook-skill-registered -->
```

If this marker exists anywhere in the file, **skip registration** — it's already done.

如果文件中任何位置存在此标记，**跳过注册** —— 已经注册过了。

---

## Template / 模板

Insert the following block into `AGENTS.md` and `CLAUDE.md`:

将以下内容块插入 `AGENTS.md` 和 `CLAUDE.md`：

```markdown
<!-- notebook-skill-registered -->

## Notebook

- **Skill**: `agents-notebook-skill` — 持久化知识笔记本，跨对话记录重要事实、决策和发现
- **笔记目录**: `.agents-notebooks/`（当前工作目录下）
- **用途**: 记录用户偏好、项目约束、外部事实、关键决策、领域洞察等
- **使用**: 当获得值得记住的新信息时自动触发；也可手动触发记录或回忆已有笔记
```

---

## Insertion Rules / 插入规则

1. **Detect existing**: Search file content for `<!-- notebook-skill-registered -->`. If found, do nothing.
2. **Create file if missing**: If `AGENTS.md` or `CLAUDE.md` doesn't exist, create it with just the template block.
3. **Insert position**:
   - If the file has a trailing `---` separator (common in CLAUDE.md), insert the template block **before** that separator, with a blank line before and after.
   - Otherwise, **append** the template block at the end of the file, with a blank line separator from existing content.
4. **Never modify existing content**: Only append/insert. Do not alter, reorder, or remove anything already in the file.

---

## Example: Before and After / 示例：插入前后

### Before / 插入前 (CLAUDE.md)

```markdown
# My Project

Some existing instructions here.

---

*Some footer content.*
```

### After / 插入后

```markdown
# My Project

Some existing instructions here.

<!-- notebook-skill-registered -->

## Notebook

- **Skill**: `agents-notebook-skill` — 持久化知识笔记本，跨对话记录重要事实、决策和发现
- **笔记目录**: `.agents-notebooks/`（当前工作目录下）
- **用途**: 记录用户偏好、项目约束、外部事实、关键决策、领域洞察等
- **使用**: 当获得值得记住的新信息时自动触发；也可手动触发记录或回忆已有笔记

---

*Some footer content.*
```

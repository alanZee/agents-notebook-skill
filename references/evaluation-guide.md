# Evaluation Guide — 评估指南

This reference provides detailed criteria and edge cases for deciding whether to record information. Read this when the core SKILL.md guidance feels insufficient for a specific situation.

本参考文件提供详细的评估标准和边界情况判断指南。当 SKILL.md 中的核心指导不足以应对具体情况时阅读此文件。

---

## Table of Contents / 目录

1. [Detailed Evaluation Criteria / 详细评估标准](#detailed-evaluation-criteria)
2. [Edge Cases / 边界情况](#edge-cases)
3. [Information Sources / 信息来源](#information-sources)
4. [Recording Quality Checklist / 记录质量清单](#recording-quality-checklist)

---

## Detailed Evaluation Criteria / 详细评估标准

### Durability Assessment / 持久性评估

Ask: "Will this information still matter in a week? A month? Across project milestones?"

问："这条信息一周后还重要吗？一个月后呢？跨越项目里程碑后呢？"

| Score | Meaning | Example |
|-------|---------|---------|
| **High** | Persistent constraint or preference | "The production server runs Python 3.9" |
| **Medium** | Relevant for current project phase | "We're using mock data until the DB migration finishes" |
| **Low** | Temporary or time-bound | "The CI pipeline is broken right now" |

Record **High** and **Medium**. Skip **Low** unless fixing it requires specific domain knowledge.

记录"高"和"中"。跳过"低"，除非修复它需要特定的领域知识。

### Uniqueness Assessment / 独特性评估

Ask: "Could I re-derive this in 5 minutes by reading code, docs, or running a command?"

问："我能通过阅读代码、文档或运行命令在 5 分钟内重新得到这个信息吗？"

| Score | Meaning | Example |
|-------|---------|---------|
| **High** | Implicit knowledge, not written anywhere | "The user's mental model: they think of X as Y" |
| **Medium** | Exists somewhere but hard to find | "The rate limit is buried in a 200-line config" |
| **Low** | Trivially derivable | "The function returns a string" |

Record **High** and **Medium**. Skip **Low**.

记录"高"和"中"。跳过"低"。

### Actionability Assessment / 可操作性评估

Ask: "Would knowing this change what I do or recommend?"

问："知道这个信息会改变我做什么或建议什么吗？"

| Score | Meaning | Example |
|-------|---------|---------|
| **High** | Directly affects code, architecture, or decisions | "The client requires all data at rest to be encrypted" |
| **Medium** | Influences approach or priorities | "The user prefers iterative over waterfall" |
| **Low** | Interesting but not decision-relevant | "The library was created by a former Google engineer" |

Record **High** and **Medium**. Skip **Low**.

记录"高"和"中"。跳过"低"。

---

## Edge Cases / 边界情况

### The User Corrects You / 用户纠正你

**Always record.** When a user says "that's wrong, actually it's X", this is high-value information. Record:
1. What you got wrong
2. The correct information
3. Why the distinction matters (if the user explains)

**始终记录。** 当用户说"不对，其实是 X"时，这是高价值信息。记录：（1）你搞错了什么；（2）正确信息；（3）为什么这个区别重要（如果用户解释了的话）。

### Information That Overlaps with CLAUDE.md / 与 CLAUDE.md 重叠的信息

If the information is already in CLAUDE.md or project docs, **skip it** — it's already captured. If the information adds nuance or context not in CLAUDE.md, **record it** with a note that the base rule is in CLAUDE.md.

如果信息已在 CLAUDE.md 或项目文档中，**跳过** —— 已经被捕获了。如果信息增加了 CLAUDE.md 中没有的细微差别或上下文，**记录它**并注明基本规则在 CLAUDE.md 中。

### Contradictory Information / 矛盾信息

If new information contradicts something already in the notebook:
1. Record the new information
2. Add a note explaining the contradiction
3. Mark the old entry as potentially outdated

如果新信息与笔记本中已有内容矛盾：（1）记录新信息；（2）添加说明矛盾的注释；（3）将旧条目标记为可能过时。

### Information Learned in Subagent Context / 在子代理上下文中获得的信息

If a subagent discovers something important, it should be surfaced and recorded in the main notebook. Information only trapped in a subagent's context is effectively lost.

如果子代理发现了重要信息，应在主笔记本中记录。仅困在子代理上下文中的信息等同于丢失。

---

## Information Sources / 信息来源

Different sources have different reliability profiles and recording needs:

不同来源有不同的可靠性特征和记录需求：

| Source / 来源 | Reliability / 可靠性 | Recording priority / 记录优先级 |
|---|---|---|
| **User explicitly states** / 用户明确说明 | Highest / 最高 | High — user preferences, constraints, decisions / 高 |
| **User implies through conversation** / 用户在对话中隐含 | High / 高 | Medium — watch for recurring themes / 中 |
| **Discovered via testing** / 通过测试发现 | High / 高 | High — empirical findings are hard to reproduce / 高 |
| **Found in official docs** / 在官方文档中发现 | Medium / 中 | Low unless hard to find / 除非很难找到否则低 |
| **Inferred from code patterns** / 从代码模式推断 | Medium / 中 | Low — read the code instead / 低 |
| **Synthesized/summarized** / 归纳总结 | Variable / 不确定 | Depends on the synthesis quality / 视综合质量而定 |

---

## Recording Quality Checklist / 记录质量清单

Before writing a note, verify:

写笔记前，确认：

- [ ] **Read first**: Checked existing notes in the relevant topic file / 先读取了相关主题文件中的已有笔记
- [ ] **Not duplicate**: Doesn't repeat something already recorded / 不重复已有内容
- [ ] **No conflict**: Doesn't contradict existing notes (if it does, update the old note) / 不与已有笔记矛盾（如矛盾则更新旧笔记）
- [ ] **Concise**: Can be read in under 10 seconds / 简洁：10 秒内可读完
- [ ] **Self-contained**: Future-you understands it without re-reading the conversation / 自包含：未来的自己无需重读对话就能理解
- [ ] **Dated**: Has a date tag for chronological context / 有日期标签便于时间排序
- [ ] **Source-tagged**: Know where this came from (user/research/reasoning/synthesis) / 标注来源
- [ ] **Sourced in the right file**: Goes into the correct topic file, not just a dump file / 放入正确的主题文件

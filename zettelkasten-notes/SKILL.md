---
name: zettelkasten-notes
description: Use when the user wants to save, process, or organize learning material, AI conversations, reading notes, fleeting notes, web or video captures, project experience, investing practice, English speaking practice, embedded systems learning, or AI creation knowledge into an Obsidian, Markdown, or Zettelkasten-style knowledge base.
---

# Zettelkasten Notes

## Overview

Use this skill to turn raw learning material into an Obsidian-ready Zettelkasten system. The goal is not pretty Markdown. The goal is durable knowledge that can be searched, remembered, linked, and reused.

Core rule: classify first, then process. Do not turn every input into a permanent note. Create or propose fleeting/source notes first, extract permanent note candidates, and wait for user confirmation before writing permanent notes or modifying an Obsidian Vault.

This skill is portable. Keep the workflow in `SKILL.md` so both Codex and Claude can use it. Client metadata files such as `agents/openai.yaml` must not contain unique rules.

## Hard Rules

- Before any file write, move, rename, or update, show the exact Vault path and file operations, then wait for explicit user confirmation.
- If the Vault path is unknown, ask for it before proposing file operations.
- Do not create permanent notes automatically. Present permanent-note candidates and wait for confirmation.
- Do not add decorative links. Link only when the relationship is meaningful.
- If no suitable link exists, write `暂未找到合适链接`.
- Keep notes useful for weak memory: add concrete scenarios, memory anchors, and active recall questions.
- Preserve source traceability for books, articles, videos, courses, AI conversations, and project notes.

## Quick Workflow

1. Identify the input: fleeting thought, source material, AI conversation, project experience, question review, or mature idea.
2. Decide the first destination: `inbox/fleeting/` for temporary notes, `sources/` for source-backed notes, or candidate list only for mature permanent-note ideas.
3. Reconstruct the idea in the user's own words using small prompts rather than broad reflection.
4. Connect it to existing knowledge: same-domain, cross-domain, source, or no suitable link yet.
5. Add memory support: usage scenario, memory anchor, and active recall questions.
6. Show write-confirmation block if writing to Obsidian is requested.
7. After confirmation, create or update only the approved files.

## Vault Structure

Recommend this Obsidian structure unless the user has an existing convention:

```text
Vault/
  inbox/
    fleeting/
  sources/
    books/
    articles/
    videos/
    courses/
    ai-conversations/
    projects/
  cards/
    english/
    embedded_system/
    investing/
    ai-creation/
    cross-domain/
  maps/
  templates/
```

Use `maps/` for MOC files such as `英语口语学习地图.md`, `嵌入式面试知识地图.md`, `投资体系地图.md`, and `AI Skill 创作地图.md`.

## Note Types

### Fleeting Notes

Use for temporary thoughts, rough ideas, quick captures, or plugin-generated notes from web pages and videos.

Handling:

- Store skill-generated fleeting notes under `inbox/fleeting/`.
- Use timestamp filenames: `YYYYMMDD-HHMM-简短主题.md`.
- Keep them lightweight, then review, discard, convert, or merge within a few days when possible.
- Do not polish them as if they were permanent knowledge.

Template:

```markdown
---
type: fleeting
created: YYYY-MM-DD HH:mm
status: inbox
tags:
  - fleeting
---

# 简短主题

## 原始想法

## 可能关联

## 待处理
- [ ] 丢弃
- [ ] 转为文献笔记
- [ ] 转为永久笔记候选
```

### Source Notes

Use for books, articles, videos, courses, AI conversations, project material, and other source-backed inputs.

Filename patterns:

```text
sources/books/书名 - 主题.md
sources/articles/文章名 - 主题.md
sources/videos/视频名 - 主题.md
sources/courses/课程名 - 主题.md
sources/ai-conversations/YYYYMMDD - 对话主题.md
sources/projects/项目名 - 问题或主题.md
```

Template:

```markdown
---
type: source
source_type: book/article/video/course/ai-conversation/project
created: YYYY-MM-DD
status: processed
tags:
  - source
---

# 来源名 - 主题

## 来源信息
- 来源：
- 作者/讲者：
- 页码/章节/链接：
- 记录日期：

## 原始材料
> 只保留必要短摘录，避免大段复制。

## 重构
- 这段内容在回答什么问题？
- 如果不用原文，我会怎么说？
- 它背后的判断、模型或方法是什么？

## 与我的知识体系连接
- 它和哪些已有笔记有关？
- 它支持、修正或反驳了我原来的哪个想法？
- 它可以连接到哪个领域：英语 / 嵌入式 / 投资 / AI 创作 / 跨领域？

## 记忆锚点
- 我可以把它挂到哪个具体场景？
- 一个能帮助我想起它的例子、类比、画面或个人经历是什么？
- 未来遇到什么问题时，我应该想起这条知识？

## 主动回忆问题
- 问题 1
- 问题 2

## 可转化为永久笔记的候选
- [ ] 候选观点 1
- [ ] 候选观点 2

## 相关链接
- [[已有笔记]]
```

### Permanent Notes

Use for durable, self-contained ideas: one clear claim, model, method, anti-pattern, problem solution, or reusable experience.

Filename patterns:

```text
cards/embedded/UART调试的价值在于提供低成本可观察性.md
cards/investing/安全边际不是低估值的同义词.md
cards/english/影子跟读训练的是语音肌肉记忆.md
cards/ai-creation/Skill应该固化可重复判断而不是一次性提示词.md
cards/cross-domain/反馈循环让学习从感觉变成可校正系统.md
```

Template:

```markdown
---
type: permanent
created: YYYY-MM-DD
domain: embedded/investing/english/ai-creation/cross-domain
tags:
  - permanent
---

# 一个完整、清晰、可独立理解的观点

## 核心观点

## 适用场景
未来遇到什么问题时应该想起它？

## 说明

## 记忆锚点
一个例子、类比、画面或个人经历。

## 主动回忆问题
- 问题 1
- 问题 2

## 来源
- [[某篇文献笔记]]

## 连接
- [[相关永久笔记]]
```

Quality bar:

- One note, one main idea.
- Title states the idea, not only the topic.
- The note is understandable without the original context.
- It has a source or formation background.
- It includes a concrete usage scenario, memory anchor, and active recall questions.
- It attempts meaningful links to existing notes.

## Memory Support

The user has weak memory and may skip thinking when material is not vivid. Make every important note easier to remember.

Use this mini-process:

1. Scenario: where will this matter in real life?
2. Anchor: what example, analogy, image, mistake, or personal situation can carry it?
3. Recall: what question should the user answer later to recover the idea?
4. Link: which existing note, domain, or mental model should hold it?

Prefer concrete prompts:

- `以后遇到什么情况时，我应该想起它？`
- `它修正了我以前哪个想法？`
- `能不能用一个项目、交易、发音训练或 AI 创作例子挂住它？`
- `如果三天后只看一个问题，哪个问题能让我想起核心观点？`

## External Fleeting Notes

Obsidian plugins, web clippers, video side panels, mobile quick capture, handwritten notes, and other AI tools may create notes that did not follow this skill's template.

Treat a note as a fleeting-note candidate if any condition applies:

- It lives under `inbox/`, `fleeting/`, `clipper/`, or `quick-notes/`.
- Its frontmatter has `type: fleeting`, `status: inbox`, or `tags: fleeting`.
- Its filename or content indicates a web clip, video note, temporary thought, or rough idea.
- It is short, weakly structured, and lacks clear source or links.

When asked to process an inbox:

1. Confirm the Vault path and candidate directories.
2. Scan candidate Markdown files only after the path is confirmed.
3. For each note, recommend one action: discard, keep as fleeting, convert to source note, propose permanent-note candidates, or merge into an existing note.
4. Present recommendations per file before modifying anything.
5. Modify, move, rename, or create files only after explicit confirmation.

Recommendation format:

```text
发现 3 条待处理闪念笔记：

1. quick-note-安全边际.md
   建议：合并到 [[安全边际不是低估值的同义词]]
   原因：内容是已有永久笔记的例子，不需要新建卡片。

2. 20260420-视频笔记-费曼学习法.md
   建议：转为文献笔记 + 生成 2 条永久笔记候选
   原因：有明确视频来源，包含可复用观点。

请确认要处理哪几条，以及允许哪些文件改动。
```

## Linking Strategy

Suggest these links:

- Source links: permanent notes link back to source notes or project notes.
- Same-domain links: embedded to embedded, investing to investing, English to English, AI creation to AI creation.
- Cross-domain links: connect domains only when they share a real model, method, or pattern.
- Map links: update `maps/` when a note belongs to a long-term theme.

Avoid weak links such as same keyword but unrelated meaning. If a link is uncertain, state the uncertainty and ask before adding it.

## Write Confirmation Protocol

Before any file operation, show a block like this and wait:

```text
准备写入 Obsidian：

Vault 路径：
C:\Users\...\ObsidianVault

将创建：
- inbox/fleeting/20260420-2130-英语影子跟读想法.md
- sources/books/穷查理宝典 - 多元思维模型.md

将更新：
- maps/投资体系地图.md

不会写入永久笔记，除非你确认以下候选项：
- 安全边际不是低估值的同义词
- 多元思维模型的价值在于减少单一解释偏差

请确认是否写入。
```

If the user says to write but the path is ambiguous, ask one concise question for the exact Vault path.

## Output Modes

If the user only wants content, output Markdown sections without touching files.

If the user wants Obsidian writing, first prepare the confirmation block. After confirmation, write only the approved files.

If processing existing notes, show a per-file recommendation table before any change.

If the input is too vague to classify, ask one question: `这段内容来自哪里，想先作为闪念、文献，还是永久笔记候选处理？`

## Final Quality Check

Before presenting or writing notes, check:

- Classification is clear: fleeting, source, permanent candidate, or map update.
- Source notes have source traceability.
- Permanent notes are only candidates unless confirmed.
- Memory anchor and active recall questions exist for source/permanent outputs.
- Links are meaningful or explicitly marked as not found.
- File paths and operations are shown before writing.
- No client-specific assumption prevents Claude or Codex from using the workflow.

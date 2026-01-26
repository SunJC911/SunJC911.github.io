---
title: 用 Claude Code 创建 blog-writer Skill：让 AI 自动帮你写博客
date: 2026-01-26 22:30:00 +0800
categories: [Claude Code, Skill]
tags: [Claude Code, Skill, 自动化, 博客, Jekyll]
author: sjc
description: 记录如何创建一个 Claude Code Skill，实现对话完成后自动生成博客文章的功能。
---

## 背景

在使用 Claude Code 完成各种任务后，经常想把解决问题的过程记录下来，分享到博客。但每次手动整理对话内容、格式化成博客文章，还是有些繁琐。

于是萌生了一个想法：能不能让 Claude Code 自动帮我把对话总结成博客文章？

## 什么是 Claude Code Skill

Skill 是 Claude Code 的扩展能力模块，可以让 Claude 具备特定领域的专业知识和工作流程。每个 Skill 包含：

- `SKILL.md`：核心文件，定义 Skill 的触发条件和工作流程
- 可选的脚本、参考资料、资产文件

Skill 分为两种级别：
- **项目级别**：放在项目的 `.claude/skills/` 目录，仅对当前项目生效
- **用户级别**：放在 `~/.claude/skills/` 目录，对所有项目生效

## 创建 blog-writer Skill

### 需求确认

首先明确需求：
- 触发方式：`/blog` 或 "帮我总结写成一篇文章"
- 输出格式：符合 Jekyll/Chirpy 主题的 Markdown 文章
- 语言：中文
- 保存位置：博客的 `_posts` 目录

### 创建 SKILL.md

在 `~/.claude/skills/blog-writer/` 目录下创建 `SKILL.md`：

```yaml
---
name: blog-writer
description: 将当前对话中完成的任务总结成博客文章。当用户说"帮我总结写成一篇文章"、"/blog"、"写成博客"或类似表达时触发。
---
```

YAML frontmatter 中的 `description` 很重要，它决定了 Skill 何时被触发。

### 定义工作流程

在 SKILL.md 的正文部分，定义 Claude 的工作流程：

1. 回顾对话，提取任务背景、解决过程、结果
2. 根据内容判断文章风格（技术教程/问题解决/经验分享）
3. 生成包含 YAML frontmatter 的 Markdown 文章
4. 保存到指定目录

### 指定文章格式

定义文章的 YAML frontmatter 格式：

```yaml
---
title: 中文标题
date: YYYY-MM-DD HH:MM:SS +0800
categories: [分类1, 分类2]
tags: [标签1, 标签2]
author: sjc
description: 一句话描述
---
```

## 使用效果

创建完成后，在任何对话中完成任务后，只需要说 `/blog`，Claude 就会：

1. 自动回顾整个对话
2. 提取关键信息
3. 生成格式正确的博客文章
4. 保存到 `_posts` 目录

比如这篇文章，就是用刚创建的 blog-writer Skill 生成的。

## 总结

通过创建 Skill，可以让 Claude Code 具备特定的工作流程和领域知识。blog-writer Skill 实现了：

- 自动化博客写作流程
- 保持格式一致性
- 节省整理时间

这种方式也可以应用到其他重复性工作中，比如生成周报、代码文档等。

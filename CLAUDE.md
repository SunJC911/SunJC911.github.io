# CLAUDE.md

本文件为 Claude Code (claude.ai/code) 在此仓库中工作时提供指导。

## 项目概述

这是一个基于 Jekyll 的个人博客网站，使用 GitHub Pages 托管，采用 Chirpy 主题（v7.2.4+）。网站语言为简体中文（zh-CN），时区为 Asia/Shanghai。

## 常用命令

### 本地开发

```bash
# 安装依赖
bundle install

# 启动本地开发服务器（带热重载）
bundle exec jekyll s -l -H 127.0.0.1

# 或使用工具脚本
bash tools/run.sh

# 生产模式预览
bash tools/run.sh --production
```

### 构建与测试

```bash
# 生产环境构建
JEKYLL_ENV=production bundle exec jekyll build -d "_site"

# HTML 链接检查
bundle exec htmlproofer "_site" --disable-external

# 或使用工具脚本
bash tools/test.sh
```

### Docker 开发（可选）

```bash
docker run -it --rm \
  --volume="$PWD:/srv/jekyll" \
  --publish 4000:4000 \
  jekyll/jekyll:4.2.0 \
  jekyll serve
```

## 架构

### 目录结构

- `_posts/` - 博客文章（Markdown），文件名格式：`YYYY-MM-DD-title.md`
- `_tabs/` - 导航标签页（About、Archives、Categories、Tags）
- `_data/` - YAML 数据文件（作者信息、联系方式、分享配置）
- `_plugins/` - 自定义 Jekyll 插件
- `assets/img/` - 图片资源
- `tools/` - 开发脚本（run.sh、test.sh）

### 核心配置

- `_config.yml` - Jekyll 主配置（网站信息、评论系统、PWA 等）
- `Gemfile` - Ruby 依赖管理

### 文章前置信息格式

```yaml
---
title: 文章标题
date: 2025-01-01 12:00:00 +0800
categories: [分类1, 分类2]
tags: [标签1, 标签2]
author: sjc           # 可选，对应 _data/authors.yml
image: /path/to.jpg   # 可选，预览图
pin: false            # 可选，是否置顶
---
```

### 部署流程

推送到 `main` 分支后，GitHub Actions 自动执行：
1. 构建 Jekyll 站点（生产模式）
2. htmlproofer 链接检查
3. 部署到 GitHub Pages

## 主题特性

- **评论系统**：Utterances（基于 GitHub Issues）
- **PWA**：已启用离线缓存和应用安装
- **分析**：GoatCounter
- **社交分享**：Twitter、Facebook、Telegram

## 资源链接

- [Chirpy 主题文档](https://chirpy.cotes.page/)
- [Jekyll 官方文档](https://jekyllrb.com/docs/)

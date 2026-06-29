# kkSaMa-123 的博客

这是一个 Jekyll Markdown 个人博客，适合部署到 GitHub Pages。

## 本地预览

安装 Ruby/Jekyll 环境后运行：

```bash
bundle exec jekyll serve
```

然后访问 `http://localhost:4000/`。

## 新增文章

在 `_posts` 目录里新建 Markdown 文件，文件名格式：

```text
YYYY-MM-DD-title.md
```

文章开头写 front matter：

```md
---
title: "文章标题"
date: 2026-06-28
category: "学习笔记"
excerpt: "首页文章卡片上显示的摘要。"
---

正文从这里开始。
```

推送到 `main` 分支后，GitHub Pages 会自动构建并发布到 `https://kksama-123.github.io/`。

## 发布到 GitHub Pages

仓库推送到 GitHub 后，在仓库设置中打开 Pages，选择 `GitHub Actions` 作为来源。
本仓库已包含自动发布配置：`.github/workflows/pages.yml`。

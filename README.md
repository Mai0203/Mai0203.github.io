# 懋屿

一个使用 [Hugo](https://gohugo.io/) 构建的中文个人博客，用来发布 Blog、随笔和学习记录。

- 在线地址：<https://mai0203.github.io/>
- 部署平台：GitHub Pages
- Hugo 版本：Extended `0.158.0`
- 其他依赖：无 Node.js、无数据库

## 本地运行

### 1. 获取项目

```bash
git clone https://github.com/Mai0203/Mai0203.github.io.git
cd Mai0203.github.io
```

如果项目已经在本地，直接进入项目目录即可。

### 2. 安装 Hugo

项目使用 `mise.toml` 固定 Hugo Extended 的版本，推荐通过 [mise](https://mise.jdx.dev/) 管理：

```bash
mise install
```

如果本机已经安装了 Hugo Extended，可以跳过这一步。使用下面的命令确认版本：

```bash
hugo version
```

### 3. 启动开发服务器

使用 mise：

```bash
mise exec -- hugo server -D
```

或者直接使用本机 Hugo：

```bash
hugo server -D
```

启动后访问 <http://localhost:1313/>。修改 Markdown、HTML、CSS 或 JavaScript 文件时，浏览器会自动刷新。

参数 `-D` 表示在本地预览标记为草稿的文章。按 `Control + C` 停止服务器。

## 发布一篇文章

在 `content/blog/` 中新建一个 Markdown 文件，例如：

```text
content/blog/my-first-post.md
```

文章可以使用以下模板：

```markdown
---
title: "文章标题"
description: "显示在文章列表和搜索摘要中的简短介绍。"
date: 2026-08-10T20:00:00+08:00
categories: ["随笔"]
tags: ["生活", "记录"]
featured: false
draft: true
---

从这里开始写正文。

## 小标题

正文支持标准 Markdown 语法。
```

常用字段说明：

- `title`：文章标题。
- `description`：文章摘要。
- `date`：发布时间，建议保留 `+08:00` 时区。
- `categories`：文章分类。
- `tags`：文章标签。
- `featured`：设为 `true` 时可作为首页推荐文章。
- `draft`：草稿设为 `true`；准备发布时改为 `false`。

生产构建不会包含 `draft: true` 的文章。

## 修改网站内容

- 首页文字：`content/_index.md`
- 关于页面：`content/about/_index.md`
- Blog 列表设置：`content/blog/_index.md`
- Blog 文章：`content/blog/*.md`
- 网站名称、作者和描述：`hugo.toml`
- 页面模板：`layouts/`
- 样式：`static/css/style.css`
- 交互脚本：`static/js/main.js`
- 网站图标：`static/favicon.svg`

## 生产构建

使用 mise：

```bash
mise exec -- hugo --gc --minify
```

或者直接使用 Hugo：

```bash
hugo --gc --minify
```

构建结果会生成在 `public/` 目录中。该目录是生成产物，不需要手动编辑或提交。

## 部署到 GitHub Pages

项目已经配置了 `.github/workflows/main.yml`。向 `main` 分支推送提交后，GitHub Actions 会自动构建并部署网站：

```bash
git add .
git commit -m "新增文章"
git push origin main
```

可以在仓库的 **Actions** 页面查看构建状态。首次配置仓库时，需要在 **Settings → Pages → Build and deployment** 中将 Source 设置为 **GitHub Actions**。

部署成功后，网站地址为：

```text
https://mai0203.github.io/
```

## 项目结构

```text
.
├── .github/workflows/main.yml  # GitHub Pages 自动部署
├── content/                    # 首页、关于页和文章内容
├── layouts/                    # Hugo 页面模板
├── static/                     # CSS、JavaScript 和图标
├── hugo.toml                   # 网站配置
├── mise.toml                   # Hugo 版本配置
└── README.md                   # 项目说明
```

## 常见问题

### 新文章没有显示

检查文章是否仍为 `draft: true`。本地运行时使用 `-D` 可以显示草稿，正式发布前需要改为 `draft: false`。

### 本地提示 `command not found: hugo`

先运行 `mise install`，再通过 `mise exec -- hugo server -D` 启动；或者自行安装 Hugo Extended `0.158.0`。

### 推送后网站没有更新

打开仓库的 **Actions** 页面检查部署任务。若任务没有启动，确认代码已推送到 `main`，并确认 Pages 的 Source 为 **GitHub Actions**。

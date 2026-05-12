---
title: "Hugo 使用指南"
date: 2024-02-01T14:00:00+08:00
draft: false
description: "Hugo 静态网站生成器的基本使用教程"
cover: "/images/cover2.jpg"
categories:
  - 教程
tags:
  - Hugo
  - 静态网站
toc: true
---

## Hugo 简介

Hugo 是用 Go 编写的静态网站生成器，以其极快的构建速度而闻名。

## 安装

### macOS

```bash
brew install hugo
```

### Linux

```bash
sudo apt-get install hugo
```

### Windows

```bash
choco install hugo-extended
```

## 创建新站点

```bash
hugo new site myblog
cd myblog
```

## 添加主题

```bash
git init
git submodule add https://github.com/yourname/bolo themes/bolo
echo 'theme = "bolo"' >> hugo.toml
```

## 创建内容

```bash
hugo new posts/my-first-post.md
```

## 本地预览

```bash
hugo server -D
```

## 构建站点

```bash
hugo
```

构建后的文件会输出到 `public/` 目录。

## 配置说明

详细配置请参考主题的 [README.md](https://github.com/yourname/bolo#readme)

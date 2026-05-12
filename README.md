# Bolo Hugo Theme

![License](https://img.shields.io/github/license/yourname/bolo)
![Hugo Minimum Version](https://img.shields.io/badge/hugo-%3E%3D0.80.0-blue)

一个从 solo-nexmoe 静态网站转换而来的 Hugo 博客主题，采用 MDUI 框架，具有响应式设计，适合技术博客和个人网站。

## 预览

![Screenshot](https://raw.githubusercontent.com/zhangzhuo0705/hugo-solo-nexmoe/main/images/screenshot.png)

## 特性

- 响应式设计，支持移动端
- MDUI Material Design 风格
- Canvas 背景动画效果
- 文章目录（TOC）支持
- 标签和分类
- 友情链接页面
- 社交链接展示
- 分页功能
- 图片懒加载
- 一言/签名文字

## 快速开始

### 安装

```bash
# 在你的 Hugo 站点目录下
git init
git submodule add https://github.com/yourname/bolo themes/bolo
```

### 配置

在 `hugo.toml` 中设置主题：

```toml
cp themes/bolo
```

### 运行

```bash
hugo server -D
```

## 配置说明

### 基础配置

```toml
baseURL = "https://example.org/"
languageCode = "zh-cn"
title = "你的博客标题"
theme = "bolo"
```

### 参数配置

| 参数 | 类型 | 必填 | 说明 | 示例 |
|------|------|------|------|------|
| `avatar` | string | 否 | 头像图片路径 | `/images/avatar.png` |
| `hitokoto` | string | 否 | 一言/签名文字 | `生活不止眼前的代码，还有诗和远方。` |

### 社交链接

```toml
[[params.social]]
  name = "GitHub"
  url = "https://github.com/yourname"
  icon = "solo-github"

[[params.social]]
  name = "微信"
  value = "your_wechat_id"
  icon = "solo-wechat"
```

### 友情链接

```toml
[[params.links]]
  name = "GitHub"
  url = "https://github.com"
  avatar = "/images/avatar.png"
```

### 导航菜单

```toml
[menu]
  [[menu.main]]
    name = "首页"
    url = "/"
    weight = 1
    [menu.main.params]
      icon = "solo-home"

  [[menu.main]]
    name = "友情链接"
    url = "/links/"
    weight = 2
    [menu.main.params]
      icon = "solo-about"

  [[menu.main]]
    name = "时间线"
    url = "/archives/"
    weight = 3
    [menu.main.params]
      icon = "solo-list"
```

## 内容类型

### 创建文章

```bash
hugo new posts/my-post.md
```

文章 front matter 支持以下字段：

```yaml
---
title: "文章标题"
date: 2024-01-01
draft: false
description: "文章描述"
cover: "/images/cover.jpg"  # 封面图
categories: ["分类"]
tags: ["标签1", "标签2"]
toc: true  # 是否显示目录
---
```

### 创建特殊页面

```bash
# 友情链接页面
hugo new page/links.md

# 归档页面
hugo new page/archives.md
```

## 开发

```bash
# 克隆主题仓库
git clone https://github.com/yourname/bolo.git

# 进入示例站点
cd bolo/exampleSite

# 启动开发服务器
hugo server --themesDir ../..
```

## 贡献

欢迎提交 Issue 和 Pull Request！详情请查看 [CONTRIBUTING.md](CONTRIBUTING.md)

## 许可证

[MIT License](LICENSE)

## 致谢

- [nexmoe](https://github.com/nexmoe) - 原始主题设计
- [MDUI](https://www.mdui.org/) - Material Design UI 框架

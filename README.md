# Hugo Solo Nexmoe

![License](https://img.shields.io/github/license/zhangzhuo0705/hugo-solo-nexmoe)
![Hugo Minimum Version](https://img.shields.io/badge/hugo-%3E%3D0.128.0-blue)

一个从 Solo Nexmoe 风格移植而来的 Hugo 博客主题，使用 MDUI，适合中文个人博客与技术文章站点。

- 在线演示：<https://zhangzhuo0705.github.io/hugo-solo-nexmoe/>
- 最低版本：Hugo 0.128.0

![主题预览](https://raw.githubusercontent.com/zhangzhuo0705/hugo-solo-nexmoe/main/images/screenshot.png)

## 功能

- 响应式文章列表和文章页
- MDUI 视觉样式与 Canvas 背景
- 浮动文章目录
- 分类、标签和归档时间线
- 友情链接和社交按钮
- 首页及列表分页
- 图片懒加载和默认封面
- 支持域名根路径和项目子路径部署

## 环境要求

- Git
- Hugo 0.128.0 或更高版本，标准版或 Extended 版均可

```bash
hugo version
git --version
```

## 安装

在已有 Hugo 站点根目录执行：

```bash
git init
git submodule add https://github.com/zhangzhuo0705/hugo-solo-nexmoe.git themes/hugo-solo-nexmoe
```

更新主题子模块：

```bash
git submodule update --init --recursive
```

## 最小配置

在站点根目录创建或编辑 `hugo.toml`：

```toml
baseURL = "https://example.org/"
locale = "zh-cn"
title = "我的博客"
theme = "hugo-solo-nexmoe"

[params]
  mainSections = ["posts"]
  avatar = "images/avatar.jpg"
  hitokoto = "认真记录，持续成长。"

[[params.social]]
  name = "GitHub"
  url = "https://github.com/your-name"
  icon = "solo-github"

[[params.links]]
  name = "Hugo"
  url = "https://gohugo.io/"
  avatar = "https://gohugo.io/favicon.ico"

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

[taxonomies]
  tag = "tags"
  category = "categories"

[pagination]
  pagerSize = 10

[markup]
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 4
    ordered = false
```

把本地头像保存为 `static/images/avatar.jpg`；`avatar` 也可以填写完整的 HTTPS 地址。

## 特殊页面

```bash
cp themes/hugo-solo-nexmoe/archetypes/links.md content/links.md
cp themes/hugo-solo-nexmoe/archetypes/archives.md content/archives.md
```

主题根据 front matter 的 `layout` 生成 `/links/` 和 `/archives/`。

## 配置参考

### 站点参数

| 参数 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| `params.mainSections` | string array | Hugo 自动推断 | 首页展示的内容分区，推荐设为 `["posts"]` |
| `params.avatar` | string | `avatar.png` | 本地站点路径或完整 HTTPS 地址 |
| `params.hitokoto` | string | 内置中文句子 | 页面底部的一言文字 |
| `params.footer` | string (HTML) | 主题内置版权信息 | 自定义侧栏页脚，支持 HTML；不设置时使用默认内容 |
| `params.footerFilings` | array | 空 | 版权行下方的备案信息，每项支持 `text` 与 `url`；不配置则不显示 |
| `pagination.pagerSize` | integer | `10` | 每页文章数量 |

页脚示例：

```toml
[params]
  footer = '© 2026 <a href="https://example.com">Your Name</a> · Powered by <a href="https://gohugo.io">Hugo</a>'
```

备案信息示例（仅在未设置 `params.footer` 时显示）：

```toml
[[params.footerFilings]]
  text = "蒙ICP备2020004404号-1"
  url = "https://beian.miit.gov.cn/"
```

### 社交链接

`params.social` 每项支持 `name`、`icon`，以及二选一的行为字段：

- `url`：在新标签页打开链接。
- `value`：弹窗显示并允许复制文本，适合微信号等信息。

### 友情链接

`params.links` 每项支持 `name`、`url` 和 `avatar`。图片字段也兼容 `logo`；未设置时使用默认图标路径。

### 菜单

导航读取 `menu.main`。`weight` 控制顺序，`menu.main.params.icon` 指定主题图标类名。

## 创建文章

```bash
hugo new content posts/my-post.md
```

```yaml
---
title: "文章标题"
date: 2026-10-19
draft: false
description: "首页显示的文章摘要。"
cover: "images/cover.jpg"
categories: ["技术文章"]
tags: ["Hugo", "写作"]
toc: true
---
```

封面保存到 `static/images/cover.jpg`，配置中使用 `images/cover.jpg`。不要写 `static/` 前缀或硬编码 Pages 项目名。`toc` 默认开启，设置为 `false` 可关闭浮动目录。

## 本地开发

自己的站点：

```bash
hugo server -D
```

主题仓库（从仓库根目录运行）：

```bash
hugo server --source exampleSite --themesDir ../.. --theme hugo-solo-nexmoe
```

生产构建：

```bash
hugo --gc --minify
```

## GitHub Pages

`.github/workflows/pages.yml` 会在 `main` 更新时构建 `exampleSite` 并部署到 GitHub Pages。工作流使用 Hugo 0.161.1，并用 Pages 返回的地址设置 `baseURL`，因此资源和文章链接能保留项目子路径。

复用前请修改站点信息，并在仓库设置中把 Pages Source 设为 **GitHub Actions**。

## 贡献与许可

- [贡献说明](CONTRIBUTING.md)
- [更新记录](CHANGELOG.md)
- [演示图片来源](exampleSite/IMAGE_SOURCES.md)
- [MIT License](LICENSE)

## 致谢

- [Hugo](https://gohugo.io/)
- [MDUI](https://www.mdui.org/)
- [Nexmoe](https://github.com/nexmoe)
- [原始 Hugo Nexmoe 主题](https://github.com/nexmoe/hugo-theme-nexmoe)

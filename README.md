# Bolo Hugo 主题说明文档

## 主题概述

**Bolo** 是一个从 solo-nexmoe 静态网站转换而来的 Hugo 博客主题，采用 MDUI 框架，具有响应式设计，适合技术博客和个人网站。

### 技术栈
- **框架**: MDUI (Material Design UI)
- **图标**: 自定义 Iconfont 字体图标
- **图片加载**: lazysizes 懒加载
- **特效**: Canvas 背景动画

---

## 目录结构

```
bolo/
├── layouts/
│   ├── _default/
│   │   ├── baseof.html      # 基础模板（所有页面的骨架）
│   │   ├── single.html      # 单篇文章详情页
│   │   └── list.html        # 列表页（首页、分类页、标签页）
│   ├── links.html           # 友情链接页面
│   ├── archives.html        # 时间线/归档页面
│   ├── 404.html             # 404 错误页
│   └── partials/
│       ├── head.html        # <head> 部分（meta、CSS 引用）
│       ├── header.html      # 顶部导航栏（含 Canvas 背景）
│       ├── sidebar.html     # 侧边栏（头像、文章数、导航、小工具）
│       ├── nav.html         # 导航菜单
│       ├── widgets.html     # 侧边栏小工具（社交、标签、分类）
│       ├── pagination.html  # 分页组件
│       ├── footer.html      # 底部（JS 引用）
│       └── copyright.html   # 版权声明
├── static/
│   ├── css/
│   │   ├── base.css         # 主题基础样式
│   │   ├── mdui.min.css     # MDUI 框架样式
│   │   └── font-icon.css    # 图标字体样式
│   ├── js/
│   │   ├── mdui.min.js      # MDUI 框架脚本
│   │   ├── canvas.js        # Canvas 背景动画
│   │   ├── app.js           # 应用主脚本
│   │   ├── lazysizes.min.js # 图片懒加载库
│   │   └── common.js        # 通用工具函数
│   └── images/
│       └── bg.jpg           # 背景图片
├── exampleSite/             # 示例站点
│   ├── config.toml          # 示例配置
│   ├── content/
│   │   ├── posts/           # 示例文章
│   │   └── page/links.md    # 友情链接页
│   └── static/images/       # 示例静态资源
└── theme.toml               # 主题元信息
```

---

## 配置说明

### 基础配置 (hugo.toml)

```toml
baseURL = "https://example.org/"
languageCode = "zh-cn"
title = "你的博客标题"
theme = "bolo"
```

### 参数配置 ([params])

| 参数 | 类型 | 必填 | 说明 | 示例 |
|------|------|------|------|------|
| `avatar` | string | 否 | 头像图片路径 | `/images/avatar.png` 或完整 URL |
| `hitokoto` | string | 否 | 一言/签名文字 | `生活不止眼前的代码，还有诗和远方。` |


### 社交链接 ([params.social])

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

配置 `value` 字段后，点击图标会弹窗显示内容，支持一键复制。不配置 `value` 则按 `url` 跳转。

[[params.social]]
  name = "RSS 订阅"
  url = "/index.xml"
  icon = "solo-rss"
```

**可用图标**:

| 图标 class | 用途 |
|-----------|------|
| `solo-github` | GitHub |
| `solo-rss` | RSS 订阅 |
| `solo-wechat` | 微信（SVG 图标） |
| `solo-comment` | 邮箱/留言 |
| `solo-about` / `solo-about2` | 关于 |
| `solo-home` | 首页 |
| `solo-list` | 列表 |
| `solo-tag` / `solo-tags` | 标签 |
| `solo-category` | 分类 |
| `solo-search` | 搜索 |
| `solo-browse` | 浏览 |
| `solo-top` | 顶部 |

### 友情链接 ([params.links])

```toml
[[params.links]]
  name = "GitHub"              # 网站名称
  url = "https://github.com"   # 链接地址
  avatar = "/images/avatar.png" # 头像/Logo 图片（可选）
```

显示为卡片网格布局，支持 hover 动效。

### 导航菜单 ([menu.main])

```toml
[[menu.main]]
  identifier = "home"      # 唯一标识符
  name = "首页"            # 显示名称
  url = "/"                # 链接地址
  weight = 1               # 排序权重（数字越小越靠前）
  [menu.main.params]
    icon = "solo-home"     # 菜单图标
```

### 其他推荐配置

```toml
# 分类法
[taxonomies]
  tag = "tags"
  category = "categories"

# 分页
[pagination]
  pagerSize = 10

# Markdown 渲染（目录支持）
[markup]
  [markup.tableOfContents]
    startLevel = 2
    endLevel = 4
    ordered = false
```

---

## 页面模板

### 1. 首页 / 列表页 (list.html)

**功能**: 以卡片形式展示文章列表，支持分页。

**特性**:
- 显示文章封面（`cover` 参数）
- 显示发布日期、分类、标签
- 显示文章摘要（`description` 参数或自动截取前 100 字）
- 排除 `layout = "links"` 和 `layout = "archives"` 的文章

### 2. 文章详情页 (single.html)

**功能**: 展示单篇文章的完整内容。

**特性**:
- 文章封面图
- 元信息：发布日期、最后修改日期、浏览量、分类、标签
- 目录导航（TOC）- 可切换显示/隐藏
- 文章内容渲染

**文章 Front Matter 参数**:

```yaml
---
title: "文章标题"
date: 2024-05-12           # 发布日期
cover: "/images/cover.jpg" # 封面图（可选）
categories: ["分类"]        # 分类（可选）
tags: ["标签1", "标签2"]   # 标签（可选）
views: 256                 # 浏览量（可选，手动设置）
toc: true                  # 是否显示目录（默认 true）
description: "文章摘要"     # 自定义摘要（可选）
---
```

### 3. 友情链接页 (links.html)

**创建方式**: 在 `content` 目录创建 `links.md`：

```yaml
---
title: "友情链接"
type: "links"
---
```

**数据来源**: 从 `params.links` 配置中读取。

### 4. 时间线/归档页 (archives.html)

**创建方式**: 在 `content` 目录创建 `archives.md`：

```yaml
---
title: "时间线"
type: "archives"
---
```

**功能**: 按年份和月份分组展示所有文章，采用时间线样式。

### 5. 404 页面 (404.html)

**功能**: 当访问不存在的页面时显示错误提示和返回首页链接。

---

## 侧边栏组件

### 头像区域
- 显示头像（`params.avatar`）
- 显示文章总数（排除 links 和 archives 页面）

### 导航菜单
- 渲染 `[menu.main]` 配置的所有菜单项
- 当前页面自动高亮

### 小工具 (widgets.html)
1. **社交按钮**: 显示 `params.social` 配置的社交链接
2. **标签云**: 显示所有标签（需配置 `taxonomies`）
3. **分类列表**: 显示所有分类及文章数量（需配置 `taxonomies`）

### 版权信息
- 显示年份、网站标题、Hugo 和主题链接

---

## 自定义与扩展

### 修改颜色主题
编辑 `static/css/base.css`，搜索 `#ff4e6a`（主题粉色）进行替换。

### 添加新的社交图标
1. 在 `static/css/font-icon.css` 中定义新的图标 class
2. 在配置中使用该 class 名称

### 覆盖主题模板
在站点根目录创建同名布局文件即可覆盖主题默认模板：

```
layouts/
├── _default/
│   └── single.html    # 覆盖主题的单页模板
└── partials/
    └── custom.html    # 添加自定义 partial
```

### 添加自定义 CSS/JS
在 `layouts/partials/head.html` 或 `layouts/partials/footer.html` 中追加引用。

---

## 示例站点验证

示例站点位于 `themes/bolo/exampleSite/`，包含：

- **3 篇示例文章**: 涵盖技术文章和生活随笔
- **友情链接页**: 展示如何配置 links
- **完整配置**: config.toml 包含所有可用配置项

**运行示例站点**:

```bash
cd themes/bolo/exampleSite
hugo server --themesDir ../.. --theme bolo
```

**构建测试**:

```bash
cd themes/bolo/exampleSite
hugo --themesDir ../.. --theme bolo
```

---

## 已知特性

| 特性 | 状态 |
|------|------|
| 响应式设计 | ✅ |
| 暗色模式 | ❌ |
| 文章目录 (TOC) | ✅ |
| 分页 | ✅ |
| 标签云 | ✅ |
| 分类列表 | ✅ |
| 友情链接 | ✅ |
| 时间线归档 | ✅ |
| 图片懒加载 | ✅ |
| Canvas 背景动画 | ✅ |
| RSS 订阅 | ✅ |
| 404 页面 | ✅ |
| 代码高亮 | 依赖 Hugo 内置 |

---

## 许可证

MIT License

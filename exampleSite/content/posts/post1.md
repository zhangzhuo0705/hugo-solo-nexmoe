---
title: "使用JavaScript实现瀑布流布局"
date: 2024-05-12
cover: "/images/post1.jpg"
categories: ["技术文章"]
tags: ["JavaScript", "前端"]
views: 256
---

## 前言

瀑布流布局是一种流行的网页布局方式，常见于图片展示类网站。本文将介绍如何使用纯JavaScript实现一个响应式的瀑布流布局效果，无需依赖第三方库。

## 基本原理

瀑布流布局的核心原理是：

1. 计算每列的当前高度
2. 将新元素放置在高度最小的列
3. 更新该列的高度

## 代码实现

```javascript
class Waterfall {
    constructor(container, columns = 4) {
        this.container = container;
        this.columns = columns;
        this.columnHeights = new Array(columns).fill(0);
    }
    
    layout(items) {
        items.forEach(item => {
            const minHeight = Math.min(...this.columnHeights);
            const minIndex = this.columnHeights.indexOf(minHeight);
            
            item.style.left = `${minIndex * (100 / this.columns)}%`;
            item.style.top = `${minHeight}px`;
            
            this.columnHeights[minIndex] += item.offsetHeight;
        });
        
        this.container.style.height = Math.max(...this.columnHeights) + 'px';
    }
}
```

## 总结

通过以上代码，我们实现了一个简单但功能完整的瀑布流布局。
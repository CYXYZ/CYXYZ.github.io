# 🏥 医学影像研究博客

[![License MIT](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](LICENSE)

一个专注于医学影像分析的研究博客平台，展示前沿的医学影像处理技术和创新应用。

## 🎯 项目概述

本项目是一个基于 Jekyll 的医学影像研究博客，旨在分享和记录医学影像领域的最新研究进展、技术笔记和实践经验。采用现代化的医学学术风格设计，提供丰富的交互体验。

### 研究方向

- **2D/3D 医学影像配准**：探索扩散模型在医学影像空间对齐中的创新应用
- **Foundation Model**：从零开始构建基础模型，深入研究模型设计、训练策略和优化技巧

## ✨ 主要特性

### 🎨 现代化设计
- **医学学术风格**：采用专业的紫蓝色和粉红色渐变配色
- **动态交互界面**：多元素浮动动画效果
- **响应式设计**：完全适配各种设备尺寸

### 📱 用户体验
- **模块化内容**：按研究领域分类组织文章
- **Tag 过滤系统**：根据标签快速查找相关内容
- **智能导航**：直观的分类导航菜单
- **流畅动画**：精心设计的过渡效果

## 📁 项目结构

```
.
├── _includes/          # HTML 模板组件
│   ├── head.html       # 页面头部
│   ├── nav.html        # 导航栏
│   └── footer.html     # 页脚
├── _layouts/           # 页面布局
│   ├── default.html    # 默认布局
│   ├── page.html       # 页面布局
│   └── post.html       # 文章布局
├── _posts/             # 博客文章
├── category-*.html     # 研究领域分类页面
├── css/                # 样式文件
├── js/                 # JavaScript 脚本
├── img/                # 图片资源
├── index.html          # 首页
└── _config.yml         # Jekyll 配置
```

## 🚀 快速开始

### 本地预览

安装 Jekyll 后，在项目目录下运行：

```bash
jekyll serve
# 或
jekyll s
```

访问 `http://127.0.0.1:4000/` 即可预览。

### 撰写新文章

在 `_posts` 中创建 Markdown 文件，命名格式：`YYYY-MM-DD-标题.md`

```markdown
---
layout:     post
title:      文章标题
subtitle:   文章副标题
date:       2026-03-07
author:     作者名
header-img: img/example.jpg
catalog:    true
category:   2D/3D配准
tags:
    - 标签1
    - 标签2
---

# 文章内容
在这里开始写你的文章...
```

**关键字段说明：**
- `layout`: post（文章布局）
- `title`: 文章标题（必需）
- `subtitle`: 副标题
- `date`: 发布日期
- `author`: 作者名
- `header-img`: 头部背景图片
- `catalog`: 是否生成目录
- `category`: 文章分类（2D/3D配准 或 Foundation Model）
- `tags`: 文章标签（用于分类过滤）

### 添加研究领域

要添加新的研究领域：

1. 在根目录创建 `category-name.html`
2. 配置 Front Matter 和 permalink
3. 添加分类特定的样式和内容

## 🎯 按标签过滤

访问分类页面时，博客自动检索和显示特定标签的所有文章：

- `/category-2d3d/` - 显示 tag 为 "2D/3D" 的所有文章
- `/category-foundation-model/` - 显示 tag 为 "Foundation Model" 的所有文章

## 🛠️ 技术栈

| 技术 | 说明 |
|------|------|
| Jekyll | 静态网站生成器 |
| Bootstrap | 前端响应式框架 |
| LESS | CSS 预处理器 |
| GitHub Pages | 部署平台 |
| Liquid | 模板引擎 |

## 🔧 配置管理

### 修改网站基本信息

编辑 `_config.yml`：

```yaml
title: CYXYZ's Blog
SEOTitle: 崔先生的博客 | CYXYZ's Blog
description: 医学影像研究与笔记
url: http://cyxyz.github.io
sidebar-avatar: /img/my.png
github_username: CYXYZ
email: mr.cyxyz@qq.com
```

### 侧边栏配置

```yaml
sidebar: true
sidebar-about-description: "Hello, laborer!"
sidebar-avatar: /img/my.png
```

## 📊 功能组件

### 研究领域卡片
- 医学学术风格渐变背景
- 悬停时的上升和阴影效果
- 直观的分类导航

### 文章列表卡片
- 左侧动态主题色边框
- 标签显示
- 作者和日期信息展示

### 动态侧边栏元素
- 科研性的浮动图标（📊🧬🔍⚗️💡🎯🚀✨）
- 持续的动画效果
- 响应式隐藏

## 📝 当前内容

### 已发布文章

1. **DiffPose 代码笔记** 
   - 分类：2D/3D 医学影像配准
   - 标签：DiffPose、2D/3D
   - 内容：详解论文与代码对应关系

2. **Foundation Model 研究笔记**（模板）
   - 分类：Foundation Model
   - 标签：Foundation Model
   - 用途：作为新写作文章的起点

## 🎨 样式自定义

### 全局样式
- 主样式文件：`css/hux-blog.css`
- 最小化样式：`css/hux-blog.min.css`
- 语法高亮：`css/syntax.css`

### 响应断点
- 大屏幕（≥1200px）：完整显示侧边栏装饰
- 中等屏幕（992px-1199px）：缩小侧边栏元素
- 小屏幕（≤768px）：隐藏侧边栏装饰

## 📚 使用指南

### 本地开发流程

1. **克隆仓库**
   ```bash
   git clone <repo-url>
   cd CYXYZ.github.io
   ```

2. **安装依赖**
   ```bash
   bundle install
   ```

3. **本地运行**
   ```bash
   bundle exec jekyll serve
   ```

4. **提交更改**
   ```bash
   git add .
   git commit -m "描述你的改动"
   git push origin master
   ```

### 发布流程

1. 在 `_posts` 中添加文章
2. 本地测试确保无误
3. 提交到 GitHub
4. GitHub Pages 自动部署

## 🔍 搜索功能

- 通过标签页面 `/tags/` 浏览所有标签
- 使用分类页面快速查找特定领域文章
- 导航栏提供快速访问主要分类

## 📦 资源优化

- **最小化图片资源**：仅保留必要的图片文件
- **渐变背景**：使用 CSS 渐变替代背景图片
- **CSS3 动画**：支持硬件加速，性能优化
- **响应式加载**：智能适配不同设备

## 🎓 学习资源

- [Jekyll 官方文档](http://jekyllcn.com/)
- [GitHub Pages 帮助](https://docs.github.com/cn/pages)
- [Bootstrap 文档](http://v3.bootcss.com/)
- [Liquid 模板语言](https://github.com/Shopify/liquid/wiki)

## 📝 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 👨‍💻 作者

**CYXYZ**
- 邮箱：mr.cyxyz@qq.com
- GitHub：[@CYXYZ](https://github.com/CYXYZ)

## 🙏 致谢

感谢以下项目和作者：
- [Hux Blog](https://github.com/Huxpro/huxpro.github.io) - 原始设计灵感
- [Jekyll](http://jekyllcn.com/) - 静态网站生成器
- [Bootstrap](http://getbootstrap.com/) - CSS 框架

---

**最后更新**：2026 年 3 月 7 日 | 📮 欢迎反馈和建议！


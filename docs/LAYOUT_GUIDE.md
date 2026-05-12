# Layout 组件使用指南

## 📖 概述

Layout 组件是 LingLog 项目的核心布局组件，它为所有页面提供一致的结构和样式。该组件集成了 ClickSpark 点击效果、导航栏、全局样式等功能。

---

## 🎯 Layout 组件位置

```
src/layouts/Layout.astro
```

---

## 📋 组件功能

Layout 组件自动提供以下功能：

| 功能 | 说明 |
|------|------|
| **导航栏** | 包含首页、日常、灵笼、关于四个导航链接 |
| **ClickSpark 效果** | 点击页面产生红色火花动画（#ff6b6b） |
| **页面框架** | 完整的 HTML 结构和元数据 |
| **全局样式** | 自动应用 `/styles/global.css` |
| **页面标题** | 自动设置浏览器标题和 `<h1>` 标题 |

---

## 🚀 快速开始

### 基础用法

创建一个新页面文件 `src/pages/mypage.astro`：

```astro
---
import Layout from '../layouts/Layout.astro';

const pageTitle = "我的页面";
---

<Layout pageTitle={pageTitle}>
</Layout>
```

保存后，访问 `http://localhost:4322/mypage/` 即可看到页面。

---

## 📝 组件属性

Layout 组件只有一个必需属性：

### pageTitle（必需）

- **类型**: `string`
- **说明**: 页面的标题，将显示在 `<h1>` 中和浏览器标题栏中

**示例**:
```astro
<Layout pageTitle="我的博客">
```

---

## 💡 使用示例

### 示例 1：简单页面

```astro
---
import Layout from '../layouts/Layout.astro';

const pageTitle = "联系我";
---

<Layout pageTitle={pageTitle}>
  <p>邮箱: example@email.com</p>
  <p>微信: xxxxx</p>
</Layout>
```

### 示例 2：文章列表页面

```astro
---
import Layout from '../layouts/Layout.astro';

const pageTitle = "我的文章";
const posts = [
  { title: "Astro 入门指南", date: "2026-05-12" },
  { title: "React 组件开发", date: "2026-05-11" },
];
---

<Layout pageTitle={pageTitle}>
  <h2>最近发布</h2>
  <ul>
    {posts.map(post => (
      <li>
        <a href={`/posts/${post.title}`}>{post.title}</a>
        <span> - {post.date}</span>
      </li>
    ))}
  </ul>
</Layout>
```

### 示例 3：含有多个部分的页面

```astro
---
import Layout from '../layouts/Layout.astro';

const pageTitle = "我的作品";
---

<Layout pageTitle={pageTitle}>
  <section>
    <h2>Web 开发</h2>
    <p>多个 Web 项目的介绍...</p>
  </section>

  <section>
    <h2>开源贡献</h2>
    <p>参与的开源项目...</p>
  </section>
</Layout>
```

---

## 🎨 自定义内容

### 使用 `<slot />`

Layout 组件使用 `<slot />` 来渲染页面内容。在 Layout 标签中放置的所有内容都会被插入到这个位置：

```astro
<Layout pageTitle={pageTitle}>
  <!-- 这里的所有内容都会被插入到 <slot /> 位置 -->
  <h2>子标题</h2>
  <p>段落内容</p>
</Layout>
```

---

## 🔧 ClickSpark 配置

ClickSpark 组件已在 Layout 中配置了默认参数：

| 参数 | 值 | 说明 |
|------|-----|------|
| `sparkColor` | `#ff6b6b` | 火花颜色（红色） |
| `sparkSize` | `12` | 火花初始长度 |
| `sparkRadius` | `25` | 火花传播距离 |
| `sparkCount` | `8` | 每次点击的火花数量 |
| `duration` | `500` | 动画持续时间（毫秒） |

如需修改 ClickSpark 参数，请编辑 `src/layouts/Layout.astro` 中的相应部分。

---

## 📁 项目文件结构

```
LingLog/
├── src/
│   ├── components/
│   │   └── ClickSpark.jsx          # React 点击效果组件
│   ├── layouts/
│   │   └── Layout.astro            # 主布局组件 ⭐
│   ├── pages/
│   │   ├── index.astro             # 首页
│   │   ├── daily.astro             # 日常页面
│   │   ├── linglong.astro          # 灵笼页面
│   │   └── about.astro             # 关于页面
│   └── styles/
│       └── global.css              # 全局样式
├── public/
│   └── styles/
│       └── global.css              # 静态样式文件
└── docs/
    └── LAYOUT_GUIDE.md             # 本文档
```

---

## 📚 创建新页面的完整步骤

### 1. 在 `src/pages/` 中创建新文件

例如：创建 `src/pages/portfolio.astro`

### 2. 导入 Layout 组件

```astro
---
import Layout from '../layouts/Layout.astro';
---
```

### 3. 定义页面标题

```astro
const pageTitle = "我的作品集";
```

### 4. 使用 Layout 包装页面

```astro
<Layout pageTitle={pageTitle}>
  <!-- 页面内容 -->
</Layout>
```

### 5. 完整示例

```astro
---
import Layout from '../layouts/Layout.astro';

const pageTitle = "我的作品集";
---

<Layout pageTitle={pageTitle}>
  <h2>Web 设计</h2>
  <p>展示你的作品...</p>
</Layout>
```

---

## ✅ 常见问题

### Q: 如何改变导航栏的链接？
**A:** 编辑 `src/layouts/Layout.astro` 中的 `<nav>` 部分。

### Q: 如何修改火花效果的颜色？
**A:** 修改 Layout.astro 中 ClickSpark 组件的 `sparkColor` 属性。

### Q: 能否对某个页面不使用 Layout？
**A:** 可以，创建不使用 Layout 的 `.astro` 文件，需要自己编写 HTML 结构。

### Q: 如何在页面中添加自定义样式？
**A:** 在 Layout 中添加 `<style>` 标签，或在 `src/styles/global.css` 中添加全局样式。

### Q: 如何增加新的导航项？
**A:** 编辑 `src/layouts/Layout.astro` 的 `<nav>` 部分，添加新的 `<a>` 标签和对应的页面。

---

## 🎓 学习资源

- [Astro 官方文档](https://docs.astro.build/)
- [Astro Layouts](https://docs.astro.build/en/basics/layouts/)
- [React 官方文档](https://react.dev/)

---

## 📝 版本历史

| 版本 | 日期 | 变更 |
|------|------|------|
| 1.0 | 2026-05-12 | 初始版本，包含 Layout 基础使用指南 |

---

最后更新：2026年5月12日

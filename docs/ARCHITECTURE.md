# LingLog 项目架构指南

## 🏗️ 项目架构概览

LingLog 是一个基于 Astro 和 React 的现代化博客网站，集成了美观的点击动画效果和统一的页面布局。

```
┌─────────────────────────────────────────────────┐
│         Astro 静态网站生成框架                    │
├─────────────────────────────────────────────────┤
│  Layout 组件 (src/layouts/Layout.astro)          │
│  ├─ ClickSpark 动画组件                         │
│  ├─ 导航栏                                       │
│  ├─ 页面框架                                     │
│  └─ 全局样式应用                                 │
├─────────────────────────────────────────────────┤
│  页面层 (src/pages/)                             │
│  ├─ index.astro（首页）                         │
│  ├─ daily.astro（日常）                         │
│  ├─ linglong.astro（灵笼）                      │
│  └─ about.astro（关于）                         │
├─────────────────────────────────────────────────┤
│  组件层 (src/components/)                        │
│  └─ ClickSpark.jsx（React 动画组件）            │
├─────────────────────────────────────────────────┤
│  样式层 (public/styles/)                         │
│  └─ global.css（全局样式）                      │
└─────────────────────────────────────────────────┘
```

---

## 🔄 工作流程

### 1. 用户访问页面
```
http://localhost:4322/ 
    ↓
路由匹配 (src/pages/index.astro)
    ↓
导入 Layout 组件
    ↓
渲染 HTML + React 组件
    ↓
浏览器展示页面
```

### 2. 用户交互
```
用户点击页面
    ↓
ClickSpark React 组件监听点击事件
    ↓
计算点击位置和火花轨迹
    ↓
Canvas 绘制动画
    ↓
显示红色火花效果
```

---

## 📦 关键组件说明

### Layout.astro（核心布局）

**位置**: `src/layouts/Layout.astro`

**职责**:
- 提供统一的页面结构
- 包含导航栏
- 集成 ClickSpark 动画
- 应用全局样式
- 定义 `<slot />` 用于页面内容

**使用方式**:
```astro
<Layout pageTitle="页面标题">
  <!-- 页面特定内容 -->
</Layout>
```

### ClickSpark.jsx（动画效果）

**位置**: `src/components/ClickSpark.jsx`

**职责**:
- 监听点击事件
- 计算火花位置和轨迹
- 使用 Canvas API 绘制动画

**配置参数**:
- `sparkColor`: 火花颜色（默认 #fff）
- `sparkSize`: 火花长度（默认 10）
- `sparkRadius`: 传播距离（默认 15）
- `sparkCount`: 火花数量（默认 8）
- `duration`: 动画时长（默认 660ms）

### global.css（全局样式）

**位置**: `public/styles/global.css`

**内容**:
- 页面整体布局
- 导航栏样式
- 标题样式
- 背景颜色等

---

## 🔌 技术栈

| 技术 | 用途 | 版本 |
|------|------|------|
| **Astro** | 静态网站生成 | ^6.3.1 |
| **React** | 动画组件 | 最新 |
| **@astrojs/react** | Astro-React 集成 | 最新 |
| **CSS** | 页面样式 | 原生 CSS |

---

## 📂 目录结构详解

```
LingLog/
├── src/
│   ├── components/
│   │   └── ClickSpark.jsx              # React 点击动画组件
│   │
│   ├── layouts/
│   │   └── Layout.astro                # 主布局模板
│   │
│   ├── pages/                          # 页面文件（自动路由）
│   │   ├── index.astro                 # → / 路由
│   │   ├── daily.astro                 # → /daily/ 路由
│   │   ├── linglong.astro              # → /linglong/ 路由
│   │   ├── about.astro                 # → /about/ 路由
│   │   └── posts/
│   │       └── post-1.md               # 博客文章
│   │
│   └── styles/                         # （已移至 public/styles/）
│
├── public/
│   └── styles/
│       └── global.css                  # 全局样式文件
│
├── docs/                               # 📍 文档文件夹
│   ├── README.md                       # 文档中心首页
│   ├── LAYOUT_GUIDE.md                 # Layout 使用指南
│   └── ARCHITECTURE.md                 # 本文档
│
├── astro.config.mjs                    # Astro 配置文件
├── package.json                        # npm 依赖配置
└── tsconfig.json                       # TypeScript 配置
```

---

## 🔄 添加新页面的流程

### 第 1 步：创建页面文件
```
src/pages/newpage.astro
```

### 第 2 步：导入 Layout
```astro
---
import Layout from '../layouts/Layout.astro';
---
```

### 第 3 步：定义标题和内容
```astro
---
const pageTitle = "新页面";
---

<Layout pageTitle={pageTitle}>
  <h2>页面内容标题</h2>
  <p>内容...</p>
</Layout>
```

### 第 4 步：自动路由
创建的页面自动对应路由：
- `src/pages/newpage.astro` → `http://localhost:4322/newpage/`

### 第 5 步（可选）：添加导航链接
编辑 `src/layouts/Layout.astro`，在 `<nav>` 中添加：
```html
<a href="/newpage/">新页面</a>
```

---

## 🎨 样式管理

### 全局样式
- **文件**: `public/styles/global.css`
- **应用**: 通过 `<link rel="stylesheet" href="/styles/global.css" />` 在 Layout 中导入
- **影响范围**: 所有页面

### 局部样式
可在 `.astro` 文件中添加 `<style>` 标签：

```astro
<style>
  .custom-class {
    color: red;
  }
</style>
```

---

## 🚀 部署建议

1. **静态部署**（推荐）
   ```bash
   npm run build
   ```
   生成的 `dist/` 文件夹可直接部署到任何静态托管服务

2. **支持的托管平台**
   - Netlify
   - Vercel
   - GitHub Pages
   - 任何静态文件服务器

3. **环境变量**（如需要）
   在 `astro.config.mjs` 中配置

---

## 🔧 常见修改

### 修改导航栏
编辑 `src/layouts/Layout.astro` 中的 `<nav>` 部分

### 修改火花颜色
编辑 Layout.astro 中 ClickSpark 的 `sparkColor` 属性

### 修改全局颜色方案
编辑 `public/styles/global.css`

### 添加新的全局样式
在 `public/styles/global.css` 中追加

---

## 📊 性能考虑

- **Astro** 预渲染所有页面为静态 HTML
- **ClickSpark** 仅在需要时加载 React（client:load）
- **CSS** 内联在 HTML 中，减少 HTTP 请求
- **构建后** 无需服务器，可直接在 CDN 上运行

---

## 🐛 调试技巧

### 查看生成的 HTML
```bash
npm run build
# 查看 dist/ 文件夹中的文件
```

### 检查浏览器控制台
- F12 打开开发者工具
- 查看 Console 标签中的错误信息

### 验证样式应用
- 使用浏览器检查器（F12 > 元素）
- 查看计算的 CSS 样式

---

## 📚 进阶主题

### 集成 Markdown 博客
可在 `src/pages/posts/` 中创建 `.md` 文件，Astro 自动转换为页面。

### 添加动态内容
在 frontmatter 中编写 JavaScript，生成动态内容。

### 自定义 React 组件
在 `src/components/` 中创建新的 React 组件，在 Layout 或页面中使用。

---

## 📖 相关文档

- [Astro 官方指南](https://docs.astro.build/en/guides/)
- [Astro 文件结构](https://docs.astro.build/en/basics/project-structure/)
- [Astro 路由](https://docs.astro.build/en/basics/routing/)

---

最后更新：2026年5月12日

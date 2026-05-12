# LingLog 项目文档

欢迎来到 LingLog 项目的文档中心！这里包含了项目的各种教学资源和指南。

## 📖 文档列表

### 1. [Layout 组件使用指南](./LAYOUT_GUIDE.md) ⭐

介绍如何使用 Layout 组件来快速创建新页面。

**包含内容:**
- 组件概述和功能
- 快速开始指南
- 多个实际使用示例
- 自定义配置方法
- 常见问题解答

**适合**: 想要创建新页面或理解项目结构的开发者

---

## 🎯 快速导航

### 首次使用？
→ 阅读 [Layout 组件使用指南](./LAYOUT_GUIDE.md) 的"快速开始"部分

### 想创建新页面？
→ 查看 [Layout 组件使用指南](./LAYOUT_GUIDE.md) 中的"创建新页面的完整步骤"

### 需要代码示例？
→ 查阅 [Layout 组件使用指南](./LAYOUT_GUIDE.md) 中的"使用示例"部分

---

## 📁 项目结构

```
LingLog/
├── src/
│   ├── components/       # React 组件
│   ├── layouts/          # Astro 布局组件
│   ├── pages/            # 页面文件
│   └── styles/           # 样式文件
├── public/               # 静态资源
├── docs/                 # 📍 文档中心（你在这里）
└── package.json          # 项目配置
```

---

## 🚀 快速命令参考

```bash
# 启动开发服务器
npm run dev

# 构建项目
npm run build

# 预览构建结果
npm run preview
```

---

## 💡 核心概念

### Layout 组件（src/layouts/Layout.astro）
项目的主布局模板，包含：
- 导航栏
- ClickSpark 点击效果
- 全局样式应用
- 页面框架

### 页面（src/pages/*.astro）
使用 Layout 组件创建的具体页面：
- index.astro（首页）
- daily.astro（日常）
- linglong.astro（灵笼）
- about.astro（关于）

### ClickSpark 组件（src/components/ClickSpark.jsx）
React 组件，提供点击火花动画效果。

---

## 📚 相关资源

- [Astro 官方文档](https://docs.astro.build/)
- [Astro 中文文档](https://docs.astro.build/zh/)
- [React 官方文档](https://react.dev/)

---

## ✏️ 如何提交问题或建议

如有任何问题或建议，请参考相应的文档部分，或检查代码注释。

---

最后更新：2026年5月12日

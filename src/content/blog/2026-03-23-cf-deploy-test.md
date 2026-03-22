---
title: 'Cloudflare Pages 自动部署测试'
description: '从本地提交到 GitHub，验证 Cloudflare Pages 是否能自动拉取、构建并发布。'
pubDate: 'Mar 23 2026'
heroImage: '../../assets/blog-placeholder-1.jpg'
---

这是一篇**测试博客**，用于验证 Cloudflare Pages 的自动化流程是否正常：

- GitHub 仓库推送（push）
- Cloudflare Pages 自动拉取
- `npm run build` 自动构建
- 产物发布到线上

## ✅ 检查清单

如果你能在博客的 `/blog/` 列表里看到这篇文章，并且点进来能正常打开，说明：

1. **构建成功**：Astro 正常编译
2. **路由正常**：静态页面生成正确
3. **资源正常**：图片与样式加载正常

## 🔧 这次提交我做了什么

- 新增一篇 Markdown 文章到：`src/content/blog/`
- 不改动构建配置（尽量减少变量）

下一步如果要进一步确认，我们可以再做一次：

- 新增一篇 MDX 文章
- 改一处页面文案（比如首页标题）
- 加一个自定义组件

（如果部署失败，把 Cloudflare Pages 的 Build Logs 贴我，我来对症修。）

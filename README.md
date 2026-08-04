# Sharewin Material - Static Website

企业英文展示站 + 询盘收集，基于纯静态 HTML/CSS/JS，部署在 Cloudflare Pages + GitHub。

## 📁 项目结构

```
sharewinmaterial-site/
├── index.html          # 首页（Hero + 产品预览 + CTA）
├── about.html          # About 页面（公司介绍 + 价值观 + 厂房图片位）
├── products.html       # Products 页面（珠光膜/热封膜/印刷标签 + 参数表）
├── contact.html        # Contact 页面（联系方式 + 询盘表单 + FAQ）
├── 404.html           # 404 错误页
├── robots.txt          # SEO 爬虫指引
├── sitemap.xml         # SEO 站点地图
├── _headers            # Cloudflare 安全 & 缓存头
├── _redirects         # Cloudflare 重定向规则
├── css/
│   └── style.css      # 全局样式（响应式、B2B 企业风格）
├── images/
│   ├── logo.svg       # 企业 LOGO（可替换为你的 PNG/AI）
│   └── favicon.svg    # 浏览器标签页图标
└── README.md           # 本文件
```

## 🚀 部署步骤（GitHub + Cloudflare Pages）

### 第一步：创建 GitHub 仓库

1. 登录 GitHub → New repository
2. 仓库名建议：`sharewinmaterial-website`（随便取）
3. 设为 **Public**（Cloudflare Pages 免费版需要）
4. **不要**勾选 "Add a README"（我们已有）

### 第二步：上传代码到 GitHub

**方式 A：用 Git 命令行（推荐）**

```bash
# 在你的电脑上操作
cd path/to/sharewinmaterial-site
git init
git add .
git commit -m "Initial commit: Sharewin Material website"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/sharewinmaterial-website.git
git push -u origin main
```

**方式 B：直接网页上传**

1. 进入 GitHub 仓库 → "uploading an existing file"
2. 把整个文件夹内容拖进去 → Commit

### 第三步：连接 Cloudflare Pages

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 左侧菜单 → **Workers & Pages** → **Create application** → **Pages** → **Connect to Git**
3. 授权 GitHub → 选择刚创建的仓库
4. 配置构建设置：
   - **Framework preset**: `None`（纯静态）
   - **Build command**: 留空
   - **Build output directory**: `/`（根目录）
5. 点 **Save and Deploy**

### 第四步：绑定自定义域名（可选但推荐）

1. 在 Cloudflare Pages 项目 → **Settings** → **Domains**
2. 添加你的域名（如 `sharewinmaterial.com`）
3. 按提示到域名注册商处改 NS 服务器为 Cloudflare 的
4. Cloudflare 自动签发 SSL 证书（免费 HTTPS）

### 第五步：验证 SEO

1. 部署完成后，访问 `https://你的项目.pages.dev`
2. 确认 4 个页面都能正常打开
3. 提交 sitemap 到 [Google Search Console](https://search.google.com/search-console)
4. 验证 `robots.txt` 可访问：`https://你的域名/robots.txt`

## ✏️ 后续维护指南

### 添加新产品

**方法：直接编辑 `products.html`**

1. 复制一个现有的 `<section class="section" id="...">` 区块
2. 修改 `id`、`h3` 标题、描述文字、参数表格内容
3. 在顶部 `.product-categories` 里加一个对应的导航按钮
4. `git push` → Cloudflare 自动重新部署（约 30 秒）

### 替换图片

1. 把你的厂房/产线/产品照片放到 `images/` 目录
2. 在 HTML 中找到对应的 `<div class="img-placeholder">` 区块
3. 替换为：`<img src="images/你的照片.jpg" alt="描述" style="width:100%; border-radius:10px;">`
4. **图片建议**：
   - 格式：`.jpg`（照片）或 `.webp`（更小更快）
   - 大小：单张 < 300KB
   - 尺寸：1200×800px 左右
   - 用 [TinyPNG](https://tinypng.com) 压缩后再上传

### 修改联系方式

全局搜索以下信息，逐一替换：
- `297347085@qq.com`
- `xiechangfeng@hotmail.com`
- `+86 13537510911`
- `xie13537510911`

涉及文件：`index.html`、`about.html`、`products.html`、`contact.html`、`_headers` 等。

### 修改公司介绍文案

编辑 `about.html` 中 `<div class="about-text">` 内的 `<p>` 段落。

### 更新 LOGO

当前 `images/logo.svg` 为矢量版奔马 Logo（4.4KB，无限缩放不模糊）。

如需替换：
- **格式**：`.svg`（矢量最佳，推荐）或 `.png`（透明背景）
- **尺寸**：导航栏显示高度约 42px，SVG 内部 viewBox 建议 480×463 左右
- **文件大小**：控制在 50KB 以内（SVG 通常只有几 KB）
- **替换方式**：直接覆盖 `images/logo.svg` 文件即可
- **favicon**：浏览器标签页图标在 `images/favicon.svg`，可同步替换

## 🔧 进阶优化建议

### 让询盘表单真正发送邮件

当前表单使用 `mailto:` 方案（用户点提交会打开邮件客户端）。如需自动收邮件，可选方案：

| 方案 | 难度 | 费用 | 说明 |
|------|------|------|------|
| **Cloudflare Workers + Email** | ⭐⭐ | 免费额度够用 | 配合 Workers 转发表单到你的邮箱 |
| **Formspree** | ⭐ | 免费版每月 50 条 | 改 form 的 `action` 即可 |
| **Netlify Forms** | ⭐ | 免费版每月 100 条 | 需迁移到 Netlify |

### SEO 加速收录

1. 注册 [Google Search Console](https://search.google.com/search-console) → 添加网站 → 验证所有权
2. 提交 `sitemap.xml` 链接
3. 注册 [Bing Webmaster Tools](https://www.bing.com/webmasters)（Bing 会同步给 Yahoo）
4. 在 Contact 页面加 `Schema.org` 结构化数据（地址、电话等）

### 多语言（后续扩展）

如需增加中文/西班牙语版本：
- 建 `zh/index.html`、`es/index.html`
- 在导航栏加语言切换器
- 在 `<html>` 标签加 `lang="en"` 属性

## 📋 检查清单

部署前确认：
- [ ] 4 个 HTML 页面内容正确
- [ ] 联系方式全部替换为真实信息
- [ ] LOGO 已替换
- [ ] 图片已上传并替换占位符
- [ ] `sitemap.xml` 中的域名改为你的真实域名
- [ ] `robots.txt` 中的域名改为你的真实域名
- [ ] 测试表单提交是否正常

部署后确认：
- [ ] 网站可正常访问（HTTPS）
- [ ] 所有页面链接互通
- [ ] 移动端显示正常（手机打开试试）
- [ ] Google Search Console 已提交 sitemap
- [ ] 用 [Google PageSpeed Insights](https://pagespeed.web.dev) 测速 > 90 分

## 📞 技术支持

如遇到部署问题，可查阅：
- [Cloudflare Pages 官方文档](https://developers.cloudflare.com/pages/)
- [Cloudflare Community Forum](https://community.cloudflare.com/)

# 我的物品 · 智能收纳管理

一个移动端优先的个人物品收纳管理 PWA。项目使用原生 HTML、CSS 和 JavaScript，无需后端服务，数据保存在当前浏览器的 LocalStorage 中。

## 功能

- 分类管理：新增、编辑、删除、搜索和排序
- 物品管理：名称、图片、备注、数量、位置、购买日期和价格
- 图片处理：最多 5 张图片，上传后自动压缩为 Base64
- 数据统计：总数量、分类数量、估值、分类分布、近 7 天趋势和位置分布
- 数据备份：导出/导入 JSON
- PWA：可安装到手机桌面，并支持静态资源离线缓存
- 响应式布局：适配手机、平板和桌面端

## 本地运行

Service Worker 需要 HTTP 或 HTTPS 环境，不能直接通过 `file://` 打开。使用任意静态服务器运行项目根目录：

```bash
python -m http.server 8080
```

然后访问 <http://localhost:8080/>。

如果使用 Node.js，也可以运行：

```bash
npx serve .
```

## 部署到静态托管

本项目没有构建步骤，发布目录就是仓库根目录。

### GitHub Pages

1. 将仓库推送到 GitHub。
2. 打开仓库的 Settings → Pages。
3. 在 Build and deployment 中选择 `Deploy from a branch`。
4. 选择目标分支和 `/ (root)` 目录并保存。

### Netlify / Vercel / Cloudflare Pages

连接 Git 仓库后使用以下配置：

- Build command：留空
- Output directory：`.` 或仓库根目录
- Install command：留空

## 项目结构

```text
.
├── index.html          # 页面入口
├── css/styles.css      # 主题、组件和响应式样式
├── js/app.js           # Storage、Render、Controller 和交互逻辑
├── manifest.json       # PWA 清单
├── sw.js               # Service Worker 离线缓存
└── icons/icon.svg      # 应用图标
```

## 数据说明

LocalStorage 键名为 `myItemsApp_v1`，数据结构包含 `categories` 和 `items` 两个数组。图片会作为 Base64 字符串存储在浏览器中，因此建议定期使用设置页导出 JSON 备份。

清除浏览器站点数据会删除本地数据；跨设备使用时请通过导出/导入完成迁移。

## 开发检查

```bash
node --check js/app.js
```

本项目为纯静态站点，不需要安装依赖或执行打包命令。

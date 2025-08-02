# 部署指南

## Vercel 静态文件部署

本项目已配置为使用 Vercel 进行静态文件部署。由于构建文件已经在 GitHub 仓库中，我们可以直接部署静态文件而无需在 Vercel 上重新构建。

### 部署步骤

#### 1. 准备工作
确保你的项目已经构建完成，所有静态文件都在 `build/` 目录中：
- `index.html`
- `static/` 目录（包含编译后的 JS、CSS 文件）
- `manifest.json`
- `service-worker.js`
- `favicon.ico`
- `asset-manifest.json`
- 其他静态资源

#### 2. 连接 GitHub 仓库到 Vercel

1. 访问 [Vercel Dashboard](https://vercel.com/dashboard)
2. 点击 "New Project"
3. 选择你的 GitHub 仓库
4. 在项目配置页面：
   - **Framework Preset**: 选择 "Other"
   - **Build Command**: 留空或设置为 `echo "Static files already built"`
   - **Output Directory**: 设置为 `build`
   - **Install Command**: 留空

#### 3. 部署配置

项目根目录的 `vercel.json` 文件已经配置好：
- 使用 `@vercel/static` 处理静态文件
- 配置了 SPA 路由重写规则
- 设置了适当的 HTTP 头部

#### 4. 部署

1. 点击 "Deploy" 按钮
2. Vercel 会自动从你的 GitHub 仓库拉取代码
3. 由于没有构建步骤，部署会很快完成
4. 部署完成后，你会得到一个 Vercel 域名

### 自动部署

每次你向 GitHub 仓库的 `main` 分支推送代码时，Vercel 会自动重新部署。

### 自定义域名

1. 在 Vercel 项目设置中添加自定义域名
2. 更新 DNS 记录指向 Vercel 的服务器
3. 等待 DNS 传播完成

### 环境变量

如果需要配置环境变量：
1. 在 Vercel 项目设置中找到 "Environment Variables"
2. 添加所需的变量
3. 重新部署以应用更改

### 故障排除

#### 常见问题

1. **404 错误**：
   - 检查 `vercel.json` 中的路由配置
   - 确保 `build/index.html` 存在

2. **构建失败**：
   - 确保 `build/` 目录包含所有必要的静态文件
   - 检查文件权限

3. **路由问题**：
   - 确保 SPA 路由重写规则正确配置
   - 测试直接访问静态文件路径

#### 调试

1. 查看 Vercel 部署日志
2. 检查浏览器开发者工具的网络和控制台
3. 验证静态文件是否正确加载

### 性能优化

- 静态文件会自动通过 CDN 分发
- 启用了适当的缓存策略
- Service Worker 配置了缓存控制

### 回滚

如果需要回滚到之前的版本：
1. 在 Vercel 项目页面查看部署历史
2. 点击之前的部署版本
3. 选择 "Promote to Production"

---

更多信息请参考 [Vercel 文档](https://vercel.com/docs)。 
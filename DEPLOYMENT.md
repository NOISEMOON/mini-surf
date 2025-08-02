# MIDI Surf 部署指南

## 部署到 Vercel

**注意**: 如果遇到配置错误，请确保使用最新的 `vercel.json` 配置格式。

### 方法1：通过 Vercel CLI（推荐）

1. **安装 Vercel CLI**
   ```bash
   npm i -g vercel
   ```

2. **登录 Vercel**
   ```bash
   vercel login
   ```

3. **部署项目**
   ```bash
   vercel
   ```

4. **设置生产环境**
   ```bash
   vercel --prod
   ```

### 方法2：通过 GitHub 集成

1. **推送代码到 GitHub**
   ```bash
   git add .
   git commit -m "Add Vercel deployment config"
   git push origin main
   ```

2. **在 Vercel 中导入项目**
   - 访问 [vercel.com](https://vercel.com)
   - 点击 "New Project"
   - 选择你的 GitHub 仓库
   - 配置构建设置：
     - Framework Preset: Other
     - Build Command: `npm run build`
     - Output Directory: `build`
   - 点击 "Deploy"

### 方法3：通过 GitHub Actions（自动部署）

1. **设置 Vercel Secrets**
   - 在 GitHub 仓库设置中添加以下 secrets：
     - `VERCEL_TOKEN`: 从 Vercel 账户设置获取
     - `ORG_ID`: 从 Vercel 项目设置获取
     - `PROJECT_ID`: 从 Vercel 项目设置获取

2. **推送代码触发自动部署**
   ```bash
   git push origin main
   ```

## 环境变量

如果需要设置环境变量，可以在 Vercel 项目设置中添加：

- `NODE_ENV=production`
- `HTTPS=true`

## 自定义域名

1. 在 Vercel 项目设置中添加自定义域名
2. 更新 DNS 记录指向 Vercel 的服务器
3. 等待 DNS 传播完成

## 故障排除

### 构建失败
- 检查 Node.js 版本（需要 14+）
- 确保所有依赖都已安装
- 查看构建日志中的错误信息

### PWA 功能不工作
- 确保使用 HTTPS
- 检查 Service Worker 是否正确注册
- 验证 manifest.json 文件格式

### MIDI 功能不工作
- 确保浏览器支持 Web MIDI API
- 检查用户是否允许了 MIDI 设备访问权限
- 验证设备连接状态

## 性能优化

- 启用 Vercel 的 CDN 缓存
- 压缩静态资源
- 使用 Service Worker 进行缓存策略优化 
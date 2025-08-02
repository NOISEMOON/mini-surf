# MIDI Surf 部署指南

## 部署到 Vercel

**静态文件部署方案** - 这是最简单、最稳定的部署方式。

### 部署步骤

1. **本地构建项目**:
   ```bash
   npm run build
   ```

2. **部署到 Vercel**:
   ```bash
   # 安装 Vercel CLI
   npm i -g vercel
   
   # 登录 Vercel
   vercel login
   
   # 部署项目
   vercel --prod
   ```

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

静态文件部署不需要特殊的环境变量设置。

## 自定义域名

1. 在 Vercel 项目设置中添加自定义域名
2. 更新 DNS 记录指向 Vercel 的服务器
3. 等待 DNS 传播完成

## 故障排除

### 构建失败
- 确保本地构建成功：`npm run build`
- 检查 `build/` 目录是否包含所有必要文件

### PWA 功能不工作
- 确保使用 HTTPS（Vercel 自动提供）
- 检查 Service Worker 是否正确注册
- 验证 manifest.json 文件格式

### MIDI 功能不工作
- 确保浏览器支持 Web MIDI API
- 检查用户是否允许了 MIDI 设备访问权限
- 验证设备连接状态

## 性能优化

- Vercel 自动提供全球 CDN 加速
- 静态资源已优化压缩
- Service Worker 提供离线缓存功能 
# BPB Worker Panel 自动同步部署项目

这个项目用于自动同步 [BPB Worker Panel](https://github.com/bia-pain-bache/BPB-Worker-Panel) 的最新版本，并自动部署到 Cloudflare Workers。

## ✨ 特点

- 🚀 **一键部署**：只需配置 GitHub Secrets，即可自动部署
- 🔄 **自动更新**：每周自动检查并同步最新版本
- 📦 **自动配置**：自动创建和绑定 KV 空间
- 🔐 **安全管理**：环境变量通过 GitHub Secrets 安全管理
- ⚡ **零配置**：无需手动配置 Cloudflare，一切自动完成

## 📋 必填变量

在使用本项目前，需要在 GitHub 仓库的 **Settings > Secrets and variables > Actions** 中配置以下变量：

### Cloudflare 相关（必填）
- `CLOUDFLARE_API_TOKEN`：Cloudflare API Token
  - 获取方式：Cloudflare 控制台 → My Profile → API Tokens → Create Token
  - 权限要求：`Account:Read` + `Workers Scripts:Edit`
- `CLOUDFLARE_ACCOUNT_ID`：Cloudflare Account ID
  - 获取方式：Cloudflare 控制台右侧边栏可以找到

### BPB 面板配置（必填）
- `UUID`：用于面板认证的 UUID
- `TR_PASS`：Trojan 密码

### GitHub Token（可选）
- `GH_TOKEN`：GitHub Personal Access Token（如不配置则使用默认 token）

## 🚀 快速开始

### 1. Fork 本项目

点击右上角的 Fork 按钮，将项目 Fork 到你的 GitHub 账号。

### 2. 配置 Secrets

进入你 Fork 的仓库，依次点击：**Settings > Secrets and variables > Actions > New repository secret**

添加上述所有必填变量。

### 3. 手动触发部署

进入 **Actions** 页面，选择 **Auto Update Worker** 工作流，点击 **Run workflow** 按钮。

### 4. 访问面板

部署成功后，访问：

```
https://Panel-action.你的子域名.workers.dev/panel
```

### 5. 设置管理员密码

首次访问面板时，需要设置管理员密码。

**密码要求**：必须包含数字 + 大写字母 + 小写字母

## 🔧 自动化功能

- ✅ **每周自动更新**：每周日凌晨 1 点自动检查并同步最新版本
- ✅ **自动部署**：检测到新版本后自动部署到 Cloudflare Workers
- ✅ **自动绑定 KV**：自动创建名为 "kv" 的 KV namespace 并绑定
- ✅ **环境变量同步**：自动将 UUID 和 TR_PASS 同步到 Cloudflare Workers

## 📖 手动操作

### 强制更新
在 Actions 页面手动触发工作流时，勾选 `force_update` 选项。

### 强制部署
在 Actions 页面手动触发工作流时，勾选 `force_deploy` 选项。

## 📁 项目结构

```
.
├── .github/workflows/
│   └── upbpb.yml          # 主工作流文件
├── _worker.js             # Cloudflare Worker 脚本
├── .env.example           # 环境变量示例
├── README.md              # 项目说明
└── version.txt            # 当前版本记录
```

## ⚠️ 免责声明

**本项目仅供学习和研究使用。**

使用本项目时，请务必：
- 遵守当地法律法规
- 遵守 Cloudflare 服务条款和使用政策
- 不得用于任何非法用途

项目作者不对使用本项目产生的任何后果负责。

## 📞 支持

如有问题，请在 [Issues](../../issues) 中提出。

---

**源项目**: [bia-pain-bache/BPB-Worker-Panel](https://github.com/bia-pain-bache/BPB-Worker-Panel)

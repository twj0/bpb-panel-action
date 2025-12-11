# BPB Panel 自动同步系统

## 项目概述
这个项目提供了一个完整的 GitHub Actions 工作流，用于自动同步 BPB Worker Panel 的最新版本，并维护项目的 README.md 文档。

## 🚀 功能特性

### 核心功能
- ✅ **自动版本检测**: 每天凌晨1点自动检查 BPB Worker Panel 的新版本
- ✅ **智能更新**: 仅在检测到新版本时执行更新操作
- ✅ **文件同步**: 自动下载并解压最新的 worker.zip 文件
- ✅ **版本管理**: 维护 version.txt 文件记录当前版本
- ✅ **文档更新**: 自动生成和更新 README.md 文件

### 增强功能
- ✅ **README.md 自动生成**: 创建包含项目信息、使用说明和更新日志的专业文档
- ✅ **更新日志管理**: 自动维护更新历史，保留最近10条记录
- ✅ **多触发方式**: 支持定时触发、推送触发和手动触发
- ✅ **强制更新**: 支持手动强制更新（忽略版本检查）
- ✅ **状态跟踪**: 详细的日志记录和状态输出

## 🔧 技术实现

### 工作流配置
- **运行环境**: Ubuntu Latest
- **触发条件**: 
  - 定时触发: 每天凌晨1点 (`0 1 * * *`)
  - 推送触发: main 分支推送
  - 手动触发: 支持 workflow_dispatch 输入参数

### 认证配置
- **GitHub Token**: 使用 `${{ secrets.GITHUB_TOKEN }}` 进行 API 认证
- **自定义 Token**: 支持使用 `SYNC_TOKEN` 变量（在 GitHub Settings > Secrets and variables > Actions 中设置）

## 📋 使用方法

### 1. 基础设置
确保在 GitHub 仓库的设置中配置以下密钥：
```
GitHub Settings > Secrets and variables > Actions
- Name: SYNC_TOKEN
- Value: 你的 GitHub Personal Access Token
```

### 2. 触发工作流
- **自动触发**: 工作流会自动在每天凌晨1点运行
- **手动触发**: 
  1. 进入 GitHub 仓库的 Actions 页面
  2. 选择 "Auto Update Worker" 工作流
  3. 点击 "Run workflow" 按钮
  4. 可选择输入 `force_update` 参数来强制更新（忽略版本检查）

工作流支持手动启动，无需等待定时任务运行。

### 3. 工作流输出
工作流会生成以下输出：
- `updated`: 是否执行了更新 (true/false)
- `tag_name`: 最新版本标签
- `update_date`: 更新时间戳

## 📁 文件结构

```
.github/workflows/
└── upbpb.yml          # 主工作流文件

README.md              # 自动生成的项目文档
version.txt            # 版本记录文件
SYNC.md               # 本说明文档
```

## 🔍 工作流详细步骤

### 1. 环境设置
- 设置 BPB Worker Panel API 地址
- 配置目标文件名称 (worker.zip)

### 2. 版本检查
- 读取本地 version.txt 文件
- 调用 GitHub API 获取最新 Release 信息
- 比较版本并判断是否需要更新

### 3. 文件更新
- 下载最新版本的 worker.zip
- 解压并覆盖现有文件
- 更新 version.txt 文件

### 4. README.md 更新
- 检查 README.md 是否存在
- 如不存在则创建新的文档
- 更新项目信息、版本号和更新时间
- 添加新的更新日志条目
- 保持日志条目数量在合理范围内（最近10条）

### 5. 自动提交
- 使用 git-auto-commit-action 提交更改
- 自动生成包含版本信息的提交消息

## ⚙️ 配置参数

### Workflow Dispatch 输入
- `force_update`: 是否强制更新（忽略版本检查）
  - 类型: 布尔值
  - 默认值: false
  - 描述: 设置为 true 时强制更新，无论版本是否相同

### 环境变量
- `REPO_URL`: BPB Worker Panel 的 GitHub API 地址
- `TARGET_FILE`: 要下载的目标文件名 (worker.zip)

## 📝 更新日志

### 当前版本增强
- ✨ 新增 README.md 自动生成功能
- ✨ 新增更新日志自动管理
- ✨ 优化工作流输出和状态跟踪
- ✨ 增强错误处理和日志记录

## 🔧 故障排除

### 常见问题
1. **API 访问失败**: 检查 GitHub Token 权限和网络连接
2. **文件下载失败**: 确认目标文件在 Release 中存在
3. **提交失败**: 检查仓库权限和分支保护规则

### 调试方法
- 查看工作流运行日志获取详细信息
- 检查 GitHub Actions 的执行状态
- 验证 Secrets 配置是否正确

## 📞 支持
如有问题，请检查工作流运行日志或在 Issues 中寻求帮助。

---
*此文档由 GitHub Actions 工作流自动生成和维护*
# Obsidian + GitHub 同步方案

> 建立时间：2026-03-28
> 状态：已完成 ✅

---

## 方案概述

- **桌面端**：Obsidian + Obsidian Git 插件
- **移动端**：Obsidian + Working Copy（iOS）
- **远程仓库**：GitHub

---

## GitHub 信息

| 项目 | 内容 |
|------|------|
| 仓库地址 | https://github.com/huangpeng516-web/knowledge |
| Token | （已保管，详见知识库管理员） |

---

## 桌面端设置（Windows/Mac）

### 第一步：安装 Git
- 下载：https://git-scm.com/download/win
- 安装：全程默认选项，一路 Next

### 第二步：克隆仓库
```bash
cd %userprofile%\Documents
git clone https://github.com/huangpeng516-web/knowledge.git
```

### 第三步：安装 Obsidian Git 插件
1. Obsidian 设置 → 社区插件 → 打开「社区插件安全模式」
2. 浏览 → 搜索「Obsidian Git」→ 安装 → 启用

### 第四步：配置插件
| 设置项 | 值 |
|--------|-----|
| Repository URL | https://github.com/huangpeng516-web/knowledge |
| Username | huangpeng516-web |
| Auto commit interval | 5 分钟 |
| Auto push interval | 5 分钟 |

### 第五步：设置 Git 身份
```bash
git config --global user.email "your@email.com"
git config --global user.name "Your Name"
```

---

## 移动端设置（iOS）

### 工具组合
- Obsidian（笔记编辑）
- Working Copy（Git 客户端）

### 克隆仓库
1. Working Copy → + → GitHub → 登录 → knowledge → Clone
2. 克隆到本地

### 同步问题
⚠️ iOS 应用之间隔离，Working Copy 和 Obsidian 无法直接共享文件夹。

**解决方案**：暂用手动方式——
- 在 Obsidian 写笔记
- 通过 iOS 分享功能把内容发给知识库管理员，帮存到 GitHub

---

## 服务器端推送（备用）

服务器直接 `git push` 有网络问题时，用 GitHub API 替代：

```bash
# 上传文件到 GitHub
curl -X PUT \
  -H "Authorization: token <TOKEN>" \
  -H "Content-Type: application/json" \
  -d "{\"message\": \"提交信息\", \"content\": \"$(base64 -w0 文件名.md)\"}" \
  "https://api.github.com/repos/huangpeng516-web/knowledge/contents/文件路径/文件名.md"
```

---

## 注意事项

1. **Token 保管**：不要公开泄露 GitHub Token（已在密码管理器备份）
2. **同步间隔**：建议 Auto commit 5分钟，Auto push 10分钟
3. **冲突处理**：多设备同时编辑可能冲突，建议同一笔记同一时间只在一端编辑

# 个人网站（GitHub Pages 部署）

本仓库包含简历个人网站源码。使用 GitHub Pages 发布，推荐方式：选择 `main` 分支的 `docs/` 目录作为发布来源。

## 目录结构
- `docs/`：线上发布目录（GitHub Pages 指向此目录）
- `personal-website/`：源文件副本（本地预览用，可选）

## 本地预览
直接用浏览器打开 `docs/index.html` 即可。

## 发布到 GitHub Pages（两种方式）

### 方式 A：网页端设置（最简单）
1. 新建 GitHub 仓库（公开或私有均可）。
2. 推送代码（确保 `docs/` 目录存在 `index.html`）。
3. 打开仓库 Settings → Pages：
   - Source：`Deploy from a branch`
   - Branch：`main`，Folder：`/docs`
   - 保存，等待几分钟即可生成访问链接。

### 方式 B：使用 GitHub CLI（命令行）
前置：安装并登录 `gh`（GitHub CLI）。
```bash
# 初始化与首推送
git init
git add .
git commit -m "feat: add resume site (docs for gh-pages)"
gh repo create <your-username>/<repo-name> --source=. --public --confirm
git push -u origin main

# 开启 Pages 指向 docs 目录
gh api \
  -X PUT \
  -H "Accept: application/vnd.github+json" \
  "/repos/<your-username>/<repo-name>/pages" \
  -f source[branch]=main -f source[path]=/docs
```

## 可选：自定义域名
1. 在 `docs/` 目录内新增 `CNAME` 文件，填入你的域名（例如：`example.com`）。
2. 在域名 DNS 添加 `CNAME` 记录指向 `<your-username>.github.io`。
3. GitHub Pages 中勾选 Enforce HTTPS。

---
如需把网站根目录改为仓库根（而非 `docs/`），请将 `docs/` 内容移到仓库根，并在 Pages 设置中选择 `Branch: main`、`Folder: /`（默认）。


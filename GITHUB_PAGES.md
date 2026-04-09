# 将个人主页部署到 GitHub Pages

GitHub 不会“渲染” jemdoc 源码，而是托管你编译好的 **静态 HTML**（`docs/` 目录）。本仓库已包含生成好的 `docs/`，也可用脚本或 CI 重新生成。

## 方式一：用 GitHub Actions 自动部署（推荐）

1. 在 GitHub 上新建仓库，把本仓库内容 **push** 上去（含 `.github/workflows/deploy-pages.yml`）。
2. 打开仓库 **Settings → Pages**。
3. **Build and deployment → Source** 选 **GitHub Actions**（不要选 “Deploy from a branch” 与 `docs` 同时开两套，任选一种即可）。
4. 再执行一次 **push** 到 `main`（或 `master`），或到 **Actions** 里手动运行 **Deploy GitHub Pages**。
5. 部署完成后，在 **Settings → Pages** 里可看到站点地址，一般为：  
   `https://<你的用户名>.github.io/<仓库名>/`  
   首页对应 `docs/index.html`。

以后只要改 `jwfu/*.jemdoc` 或 `jwfu/jemdoc.css` 等，push 后 Actions 会重新编译并发布。

本地可先执行（需已安装 Python）：

```bash
chmod +x build-site.sh
./build-site.sh
```

## 方式二：不用 Actions，直接从 `docs/` 分支发布

1. 本地或 CI 运行 `./build-site.sh`，保证 `docs/` 是最新的。
2. 将 `docs/` **提交并 push** 到默认分支。
3. **Settings → Pages → Source** 选 **Deploy from a branch**，分支选 `main`（或 `master`），文件夹选 **`/docs`**，保存。

## 仓库与推送示例

若尚未初始化 git：

```bash
cd /path/to/jemdoc_mathjax-master
git init
git add .
git commit -m "Add personal site and GitHub Pages"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

将 `<你的用户名>`、`<仓库名>` 换成你自己的。

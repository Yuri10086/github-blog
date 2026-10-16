# 我的个人博客

基于 [Hugo](https://gohugo.io) + [GitHub Pages](https://pages.github.com) 的个人博客。

## 目录结构

```
github-blog/
├─ config.toml              # Hugo 配置（站点地址、主题、搜索）
├─ content/
│  ├─ _index.md             # 首页
│  └─ posts/                # 文章目录（Obsidian 同步到这里）
│     └─ hello-world.md
├─ archetypes/default.md    # 新文章模板
├─ themes/paper/            # PaperMod 主题（子模块，见下）
├─ .github/workflows/
│  └─ hugo.yml              # GitHub Actions 自动构建部署
├─ .gitignore
└─ README.md
```

## 第一次部署（3 步）

### 1. 创建 GitHub 仓库

打开 <https://github.com/new>，仓库名填 `github-blog`，选 **Public**，先**不要**勾选初始化 README（本地已有）。

### 2. 补上主题子模块

主题文件夹 `themes/paper` 是空的，需要拉下来。在本目录执行：

```powershell
git init
git remote add origin https://github.com/yuri10086/github-blog.git
git submodule add https://github.com/adityatelange/hugo-paper.git themes/paper
```

> 如果你还没装 Git，可以直接到 <https://github.com/adityatelange/hugo-paper/releases> 下载 zip，解压后把里面的内容放进 `themes/paper/`。

### 3. 推送并开启 Pages

```powershell
git add .
git commit -m "init: hugo blog"
git branch -M main
git push -u origin main
```

然后在仓库 **Settings → Pages → Source** 选择 **GitHub Actions**。

等 Actions 跑完，访问：`https://yuri10086.github.io/github-blog/`

## 日常写文章

两种方式，任选：

- **GitHub 网页**：仓库 → `content/posts` → **Add file → Create new file**，写完 commit，自动发布。
- **Obsidian**：把 vault 指到 `content/posts`（推荐安装 Git 插件自动提交），或者手动把笔记复制进来再推送。

## 常用配置（config.toml）

| 想改什么 | 改哪里 |
|---------|--------|
| 站点标题 | `title` |
| 站点地址（换域名后） | `baseURL` |
| 亮/暗主题 | `params.theme` = `auto` / `light` / `dark` |
| 搜索开关 | `params.enableSearch` |

## 换主题

```powershell
git submodule remove themes/paper
git submodule add <新主题仓库地址> themes/<新主题名>
```

然后把 `config.toml` 里的 `theme = "paper"` 改成新主题名。

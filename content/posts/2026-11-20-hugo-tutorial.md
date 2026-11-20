---
title: "Hugo Tutorial"
date: 2026-11-20T18:55:00+08:00
draft: false
slug: "hugo-tutotial-20261120"
summary: "这篇文章提供从创建页面到发布的指引。"
tags: [入门教程]
categories: [Hugo]
author: "Voosk"
ShowToc: true
---

## 准备工作
假设你还没有拉取仓库，首先应当使用 `git clone` 命令把博客拉取到本地，随后进入项目目录。

```sh
mkdir /select/a/path
cd /path/to/the/directory
git clone <URL> .
```

## 新建一篇文章
在 Hugo 中，文章来自 Markdown 文件。文章在被创建以后就会被索引，不需要维护目录。
你可以手动新建 `.md` 文件，也可以使用 `hugo new <path>` 命令从模板新建，文章要放在 `content/posts` 目录，文件使用英文命名。

## 文章结构
文章开头有一段 Front Matter，随后是正文。

Front Matter 由 `---` 包裹，内含 Meta，下表展示了常见的 Meta。

|Meta|含义|示例值|
|---|---|---|
|title|标题|"Hugo tutorial"|
|date|日期|2026-11-20T16:58:59+08:00|
|draft|是否为草稿|true/false|
|slug|URL末端名称|"hugo-tutorial-20261120"|
|summary|文章简介|"这篇文章提供从创建页面到发布的指引。"|
|tag|标签|["Hugo", "blog"]|
|author|作者|"Voosk"|
|ShowToc|Show Table of contents，页面是否显示大纲|true/false|

注意字符串类型需要加双引号。下面是一份完整的 Front Matter 示例。

```markdown
---
title: "Hugo Tutorial"
date: 2026-11-20T16:58:59+08:00
draft: true
slug: "hugo-tutotial-20261120"
summary: "这篇文章提供从创建页面到发布的指引。"
tags: [入门教程]
categories: [Hugo]
author: "Voosk"
ShowToc: true
---
```

当 draft 值为 true 的时候将文章设定为草稿，仅本地预览（Debug）可见，在线（Release）不可见（如何查看本地预览请见后文）。没写完的文章标记为草稿在本地看，不要渲染到线上。

slug 可以设定 URL 末端名称，例如 `http://localhost:1313/posts/hugo-tutotial-20261120/`。

文章较长的时候可以启用 ShowToc 展示大纲；出于美观，文章较短时建议关闭它。

在写好 Front Matter 的 Meta 以后，便可以开始编写正文。

## 预览文章
首先我们需要给操作系统安装 Hugo，macOS 可以使用 `brew install hugo` 安装，Arch Linux 可以使用 `yay -Ss hugo` 来查找和确认包，随后使用 `-S` 参数进行安装。

安装好 Hugo 以后，执行命令启动本地 Hugo 服务器：

```sh
hugo server -D
```

随后会得到一些输出，节选后部分：

```
                  │ ZH - CN 
──────────────────┼─────────
 Pages            │      42 
 Paginator pages  │       0 
 Non-page files   │       0 
 Static files     │       1 
 Processed images │       0 
 Aliases          │      14 
 Cleaned          │       0 

Built in 18 ms
Environment: "development"
Serving pages from disk
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1) 
Press Ctrl+C to stop

Change detected, rebuilding site (#1).
2026-11-20 18:40:22.514 +0800
Source changed /posts/2026-11-20-hugo-tutorial.md
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Total in 13 ms

Change detected, rebuilding site (#2).
2026-11-20 18:41:32.013 +0800
Source changed /posts/2026-11-20-hugo-tutorial.md
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Total in 9 ms
```

可以看到输出中统计了页面数据，并且提示 Web Server 在 `http://localhost:1313/` 可用。使用浏览器访问该页面即可预览整个博客。

## 发布
当你已经完成文章的撰写，并且在浏览器中确认无误，便可以发布。将本地的 git 修改推送到 GitHub 远程代码托管仓库即可，Cloudflare 会自动构建页面，稍等片刻便可以在网页上看到新文章。

## 其他内容
当前博客两位作者用户名分别为 Voosk 和 Liling。

Front Matter Meta 里面 author 如果不写，Hugo 会将文章作者默认归属给 Voosk。

新增作者需要在 `content/authors` 新建 markdown 文件，可以复制 `content/authors/voosk.md` 作为模板。

**作者页**
| 作者 | 页面 |
|---|---|
| Voosk | <https://blog.int86.xyz/authors/voosk/> |
| Liling | <https://blog.int86.xyz/authors/liling/> |

作者页里用 shortcode 自动列出该作者的文章：（即使是代码框里面，这条 shortcode 也会被执行，需要反斜杠隔开）
```text
\{\{\< authorposts "Voosk" \>\}\}
```

**Cloudflare Pages 构建配置**
| 项 | 值 |
|---|---|
| Framework preset | Hugo |
| Build command | `hugo --gc --minify` |
| Output directory | `public` |
| 环境变量 | `HUGO_VERSION` = 本地 `hugo version` 的版本号 |


主题 PaperMod 已 vendor 在 `themes/PaperMod/`，构建不依赖外部下载。

---

## 常见错误排查
写完文章以后在线上看不到：
- 去看看本地预览是否正常。
- 本地修改是否成功推送至 GitHub 仓库？
- 日期是否写成了未来？未来的文章不会被生成。
- 正式发布文章的时候，Front Matter 中 draft 属性是否忘记设置为 false？

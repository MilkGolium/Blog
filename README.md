# Blog

个人博客源码，Hugo + PaperMod，部署在 Cloudflare Pages。

- 线上：<https://blog.int86.xyz>
- 写文章：`hugo new posts/标题.md`，写完 `git push` 自动发布
- 本地预览：`hugo server -D` → <http://localhost:1313>

## 写一篇文章

```bash
cd ~/Documents/Projects/Blog
hugo new posts/2026-11-21-some-title.md
hugo server -D
```

front matter（`hugo new` 会自动生成，填好中文即可）：

```yaml
---
title: "中文标题"
date: 2026-11-21T20:00:00+08:00
draft: false
author: "Voosk"          # 必填：Voosk 或 Liling
slug: "some-title"       # 决定 URL，英文小写连字符
tags: ["Rust", "开发日志"]
categories: ["技术笔记"]
summary: "一句话摘要，显示在列表页"
ShowToc: true
---
```

三条必须注意的：

- **`author` 必须写**，否则会被算成站点默认作者（Voosk）
- **`date` 不能是未来时间**，否则页面不会生成，而且没有任何报错
- 文件名建议英文；URL 以 `slug` 为准

## 作者页

| 作者 | 页面 |
|---|---|
| Voosk | <https://blog.int86.xyz/authors/voosk/> |
| Liling | <https://blog.int86.xyz/authors/liling/> |

作者页里用 shortcode 自动列出该作者的文章：

```text
{{< authorposts "Voosk" >}}
```

新增作者：复制 `content/authors/voosk.md` 改名，把 `title` 和 shortcode 里的名字换掉。

## Cloudflare Pages 构建配置

| 项 | 值 |
|---|---|
| Framework preset | Hugo |
| Build command | `hugo --gc --minify` |
| Output directory | `public` |
| 环境变量 | `HUGO_VERSION` = 本地 `hugo version` 的版本号 |

主题 PaperMod 已 vendor 在 `themes/PaperMod/`，构建不依赖外部下载。

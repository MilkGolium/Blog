# Blog

个人博客源码，Hugo + PaperMod，部署在 Cloudflare Pages。

- 线上：https://blog.int86.xyz
- 写文章：`hugo new posts/标题.md`，写完 `git push`
- 本地预览：`hugo server -D` → http://localhost:1313

Cloudflare Pages 构建配置：

| 项 | 值 |
|---|---|
| Framework preset | Hugo |
| Build command | `hugo --gc --minify` |
| Output directory | `public` |
| 环境变量 | `HUGO_VERSION` = 本地 `hugo version` 的版本号 |

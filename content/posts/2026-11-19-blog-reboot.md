---
title: "博客重开"
date: 2026-11-19T18:00:00+08:00
draft: false
tags: ["随笔"]
categories: ["日志"]
author: "Voosk"
summary: "换掉手写 HTML，改用 Hugo。服务器搬家、被墙、折腾一圈之后的一个小结。"
---

这个博客原来是手写的 HTML，一个 `index.html` 撑了三天。今天换成 Hugo，写文章终于只是写 Markdown 了。

顺便记录一下这两天折腾的事：

- 服务器的 IP 被墙了，TCP 全断，ICMP 还通
- 换了 Cloudflare 回源方案，代理又能用了，而且以后 IP 再被墙也不用再花钱换
- 博客挪到 Cloudflare Pages，源站彻底不对外

## 为什么是 Hugo

单二进制，没有 `node_modules`。构建一篇文章是毫秒级，Cloudflare Pages 上几乎不会因为超时失败。

```bash
hugo new posts/新文章.md
hugo server -D
```

写完之后 `git push`，Pages 自己构建发布。

## 接下来写什么

目前想写这几类：

1. **游戏开发日志** —— 《The Law Of Prey》的进展和踩坑
2. **Rust 学习笔记** —— 从 C 转过去的一些差异
3. **乡村生活** —— 冬天、柴火、九只狗

不确定能不能坚持，但先把框架搭起来。

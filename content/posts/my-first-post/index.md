---
title: "我是如何搭建个人博客的"
date: 2026-04-23T20:00:00+08:00
draft: false
tags: ["博客搭建", "Hugo", "Vercel", "前端折腾"]
categories: ["建站记录"]
---

> “折腾，是极客的宿命。既然别人是跳动的，那我也绝不甘于静止。”

欢迎来到我的个人博客！我是 Kiki，只偏爱于篮球巨星-Curry。

你现在看到的这个悬浮着“毛玻璃便当盒”、标题闪烁着霓虹呼吸灯、背后还有我偶像库里坐镇的博客，是我从零开始一行行代码折腾出来的。

这篇文章，我将复盘整个博客的搭建全流程，以及那些让我差点抓狂的踩坑瞬间，希望能帮到后来者。在这里要衷心感谢下面链接的博主！

最主要搭建博客流程可以参考网址：[text](https://www.z2x-blog.top/blog-setup/course/)，我这里只是简单介绍一下容易出问题的地方！

## 1. 核心框架：Hugo + PaperMod

在这个注重效率的时代，我选择了 **Hugo** 作为静态网站生成器。它编译速度极快，且不需要复杂的数据库。
主题方面，我选用了极简的 **PaperMod**。但为了突破它原有的限制，我做了一些“硬核魔改”。

### 💣 踩坑警告：Git 子模块的记忆陷阱
在刚引入 PaperMod 主题时，直接克隆会导致它自带一个 `.git` 文件夹。如果你直接 `git push`，云端的仓库里只会剩下个空壳，最终导致网页渲染失败。
* **我的破局之法：** 暴力破解！直接把 `themes` 里的 `papermod` 文件夹重命名为 `mytheme`，然后在 `hugo.yaml` 中修改 `theme: 'mytheme'`。这成功骗过了 Git 的缓存，顺利将主题源码推上了云端。

## 2. 自动化部署：Vercel 免费又好用

代码放在 GitHub 后，我利用 **Vercel** 进行了持续部署。每次我在本地写完笔记，只需一个 `git push`，Vercel 就会自动拉取代码并更新网站。

### 💣 踩坑警告：遭遇无情的 404 NOT_FOUND
明明代码传上去了，打开网页却是 404？这绝对是 Vercel 的部署设置没对齐。
* **核心排查步：** 必须进到 Vercel 的 `Project Settings -> Build & Development Settings`，将 Framework Preset 强行指定为 `Hugo`，并且把 Output Directory 设定为 `public`。重新部署（Redeploy）后，画面瞬间点亮。

## 3. 视觉进化：从毛坯房到赛博精装

我不想让博客看起来像个干瘪的说明书，所以我深入 `assets/css/extended/custom.css` 进行了一场视觉重构。

* **极致悬浮卡片 (Glassmorphism)：**
  废弃了主题默认的大灰框，写了全新的毛玻璃 CSS 代码：
  `background: rgba(20, 20, 20, 0.6); backdrop-filter: blur(10px);`
  配合极其丝滑的 `:hover` 浮动阴影，让文章卡片悬浮在库里的背景图之上。
* **霓虹呼吸标题：**
  利用 `@keyframes` 动画引擎，给主标题加上了 2 秒一个周期的多层绿色 `text-shadow`，让 "KIKI BLOG" 拥有了赛博朋克般的呼吸感。
* **便当盒布局 (Bento Box)：**
  在 `layouts/partials/` 下硬核覆写了 `index_profile.html`，利用 CSS Grid 打造了 2x2 的互动网格，分类展示了我的学习笔记和学术项目。

## 接下来写点什么？

这个博客将成为我的“数字花园”。接下来，我会在这里陆续更新：
你所感兴趣的一切！

感谢你的访问，随时欢迎在各个文章下面给我留言互动！

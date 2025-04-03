# 🍥Sytusの窝

## 🏆概述

本站是由 Sytus 基于 [Fuwari](https://github.com/saicaca/fuwari) 创建的个人网站，主要用于发布本人的学习笔记与随笔等，其主要格式为 MarkDown，欢迎阅读。本站目前为 2.0 版本，前身的框架为 [Hexo](https://hexo.io/zh-cn/)，所以部分文章的发布时间并不准确，还请见谅。

本站部署于 [Github Page](https://pages.github.com/)，源代码发布于 [Github](https://github.com/SytusRamlethal/SytusRamlethal.github.io)，使用 [GitHub Actions](https://docs.github.com/zh/actions) 技术，当代码推送至仓库时，将自动构建。

如果您对本站或本站内容有任何疑问，欢迎在 [Github议题](https://github.com/SytusRamlethal/SytusRamlethal.github.io/issues) 进行询问。

## ✨ 功能特性

* [X]  基于 Astro 和 Tailwind CSS 开发
* [X]  流畅的动画和页面过渡
* [X]  亮色 / 暗色模式
* [X]  自定义主题色和横幅图片
* [X]  响应式设计
* [ ]  评论
* [X]  搜索
* [X]  文内目录

## 🧞 指令


| Command                            | Action                                |
| ---------------------------------- | ------------------------------------- |
| `pnpm install` 并 `pnpm add sharp` | 安装依赖                              |
| `pnpm dev`                         | 在`localhost:4321` 启动本地开发服务器 |
| `pnpm build`                       | 构建网站至`./dist/`                   |
| `pnpm preview`                     | 本地预览已构建的网站                  |
| `pnpm new-post <filename>`         | 创建新文章                            |
| `pnpm astro ...`                   | 执行`astro add`, `astro check` 等指令 |
| `pnpm astro --help`                | 显示 Astro CLI 帮助                   |

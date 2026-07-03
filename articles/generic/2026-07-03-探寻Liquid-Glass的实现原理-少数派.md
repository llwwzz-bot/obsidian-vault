---
url: "https://sspai.com/post/100983"
platform: Web
date: 2026-07-03
tags: [Liquid Glass, iOS 开发, CALayer, 私有 API, 视觉特效, RuntimeBrowser]
source_title: "探寻Liquid Glass的实现原理 - 少数派"
author: "深空灰SpaceGrey"
doc_type: knowledge
---
# 📚 探寻Liquid Glass的实现原理 - 少数派

> **类型**：知识卡片  |  **核心概念**：Liquid Glass 效果通过三层 CALayer 实现，核心是私有类 CABackDropLayer 及其参数控制。

## 📋 摘要

本文通过逆向工程揭示了苹果Liquid Glass效果由三层CALayer实现，包括高光、阴影和形变模糊层，并介绍了通过私有类CABackDropLayer调整参数的方法。

## 🔑 关键知识点

- 苹果 API 仅提供一行代码实现 Liquid Glass，但无法自定义。
- 通过视图调试发现效果由三层 CALayer 组成：高光轮廓、阴影、形变与模糊（CABackDropLayer）。
- 使用 RuntimeBrowser 提取 iOS 26 中 CABackDropLayer 的头文件，与 iOS 18 对比发现新增参数。
- 关键参数包括 tracksLuma（跟踪背景亮度）、lumaSubrect（跟踪区域）、allowsFilteredLuma（允许叠加黑白层）。
## 🎯 适用场景

- 为 iOS 应用添加类似 visionOS 的玻璃质感 UI 元素。
- 自定义 Liquid Glass 效果，调整颜色深浅、模糊区域等。
## ⚖️ 方案权衡

使用私有 API 可能导致 App Store 审核拒绝或系统更新后失效；但能实现更丰富的视觉效果，适合非发布用途或研究。
## 🖼️ 图片

![图片1](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/0)

![图片2](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/1)

![图片3](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/2)

![图片4](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/3)

![图片5](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/4)

![图片6](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/5)

![图片7](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/6)

![图片8](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/7)

![图片9](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/8)

![图片10](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/9)

![图片11](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/10)

![图片12](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/11)

![图片13](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/12)

![图片14](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/13)

![图片15](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/14)

![图片16](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/15)

![图片17](https://rss-collector.liwenzhestudy.workers.dev/img/a6d701f3-ddf4-4eea-9bf9-a9efb074c3dc/16)
## 📎 原文

[探寻Liquid Glass的实现原理 - 少数派](https://sspai.com/post/100983)

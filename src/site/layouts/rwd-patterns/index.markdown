---
layout: section
title: "响应式 Web 设计模式"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。."
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 2
id: rwd-patterns
collection: multi-device-layouts
---

{% wrap content%}

大多数响应式网页的布局可以归纳为五种设计模式：mostly fluid、column drop、layout shifter、tiny tweaks和off canvas。一些情况下，页面可能会采用组合设计模式，例如组合使用column drop和off canvas。这些设计模式最初都是由
[Luke Wroblewski](http://www.lukew.com/ff/entry.asp?1514) 定义的，它们为响应式页面提供了一个坚实的基础。


## 设计模式

To create simple, easy-to-understand samples, each the samples
below were created with real markup using
[`flexbox`](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Flexible_boxes),
typically with three content `div`'s contained within a primary container `div`.
 Each sample was written starting with the smallest view first and breakpoints
were added when necessary.  The [flexbox layout mode is well
supported](http://caniuse.com/#search=flexbox) for modern browsers, though may
still require vendor prefixing for optimal support.

为创建简单易懂的示例，下面每一个案例都是基于 [`flexbox`](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Flexible_boxes) 通过真实的标签创建的，主要是在一个主 div 内放置了三个内容 div 。每个示例都是先从定义最小视图开始，然后在必要时候加上响应节点。尽管需要依赖特定前缀来实现最佳效果，但是 flexbox 布局模式已经得到了主流浏览器的支持。

{% include modules/nextarticle.liquid %}

{% endwrap %}

---
layout: article
title: "Mostly fluid"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "大多数的流式模式由流式网格构成。在中等或大点的屏幕中总是具有相同的尺寸，而在更大屏幕中才会调整边距。"  
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 1
collection: rwd-patterns
---

{% wrap content%}

在小点的屏幕中， 当列内容变成垂直排列时，fluid grid 模式会导致主内容区域的重新流动。

这个模式的主要特点是它只需要在小屏幕和大屏幕之间设置一个断点。

{% link_sample _code/mostly-fluid.html %}
  <img src="imgs/mostly-fluid.svg">
  试一试
{% endlink_sample %}

在最小的屏幕中，每个内容 `div` 都垂直排列。

当屏幕宽度达到 600px 时，主内容 `div` 保持 100% 的宽度，而下面两个 `div` 则位于第一个div下方，如图所示。

当屏幕宽度超过 800px 时， 主内容 `div` 则固定宽度并在屏幕上居中。

使用这种设计模式的网站有：

 * [A List Apart](http://mediaqueri.es/ala/)
 * [Media Queries](http://mediaqueri.es/)
 * [SimpleBits](http://simplebits.com/)


{% include_code _code/mostly-fluid.html mfluid css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}

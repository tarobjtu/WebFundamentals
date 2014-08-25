---
layout: article
title: "Layout shifter"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "Layout shifter 在多断点的情况下是最好的模式。"   
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 3
collection: rwd-patterns
---

{% wrap content%}

这种布局的关键在于，内容不是向下流动或移到到其他列下面，而是四处移动。

由于每个响应点对应的布局有巨大的差异，所以要保持一致需要更复杂的操作，并可能需要对元素内部做出改动，而不仅仅是改变全局布局。

{% link_sample _code/layout-shifter.html %}
  <img src="imgs/layout-shifter.svg">
  试一试
{% endlink_sample %}

这个例子简单展示了 layout shifter 模式。

当屏幕较小时，内容div纵向排列。

而当屏幕变大时，布局发生了很大的改变，布局形成左边一个 `div` ，而右边由两个 `div` 垂直排列组成。

使用这种设计模式的网站包括：

 * [Food Sense](http://foodsense.is/)
 * [Seminal Responsive Design
  Example](http://alistapart.com/d/responsive-web-design/ex/ex-site-FINAL.html)
 * [Andersson-Wise Architects](http://www.anderssonwise.com/)

{% include_code _code/layout-shifter.html lshifter css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}

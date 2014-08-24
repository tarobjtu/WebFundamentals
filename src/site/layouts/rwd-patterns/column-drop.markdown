---
layout: article
title: "Column Drop"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "对于满屏多列的布局，使用column drop 模式时，当视窗宽度小于内容区域的宽度时，内容将垂直排列。"  
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 2
collection: rwd-patterns
---

{% wrap content%}

这种模式最终会导致内容变成垂直排列。

选择合适的断点取决于不同的内容及设计。

{% link_sample _code/column-drop.html %}
  <img src="imgs/column-drop.svg">
  试一试
{% endlink_sample %}

与 mostly fluid 设计模式的示例类似，内容在最小视图下将垂直排列。

而当屏幕宽度超过 600px 时，主内容和第二个内容 `div` 将占据了屏幕全部宽度。

`div` 的顺序则根据CSS中的order属性排列。当宽度达到800px时，三个内容 `div` 一起出现，并占据屏幕的全部宽度。

使用这种设计模式的网站包括：

 * [Modernizr](http://modernizr.com/)
 * [Wee Nudge](http://weenudge.com/)

{% include_code _code/column-drop.html cdrop css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}

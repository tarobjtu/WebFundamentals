---
layout: article
title: "Tiny tweaks"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "Tiny tweaks 模式会对布局做细微的改变，比如调整字体大小、缩放图片大小或者细微地移动内容。"  
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 4
collection: rwd-patterns
---

{% wrap content%}

这种模式对于单列布局非常适合，比如单页面以文章为主的线性布局的网站。


{% link_sample _code/tiny-tweaks.html %}
  <img src="imgs/tiny-tweaks.svg">
  试一试
{% endlink_sample %}

顾名思义，屏幕尺寸改变时会导致示例的细微改变。

当屏幕宽度变得越来越大时，字体和边距也跟着改变。

使用这种设计模式的网站包括：

 * [Opera's Shiny Demos](http://shinydemos.com/)
 * [Ginger Whale](http://gingerwhale.com/)
 * [Future Friendly](http://futurefriendlyweb.com/)

{% include_code _code/tiny-tweaks.html ttweaks css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}

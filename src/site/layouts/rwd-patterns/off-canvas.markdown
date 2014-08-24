---
layout: article
title: "Off canvas"
description: "响应式Web设计模式发展地很快，但总有一些已有的模式在跨终端方面工作得很好。"
introduction: "与垂直排列内容不同，off canvas 模式将不常用的内容（也许是导航或屏幕外的菜单）只在大屏幕情况下显示，而在小屏幕下只显示主要内容。"  
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
article:
  written_on: 2014-04-30
  updated_on: 2014-08-24
  order: 5
collection: rwd-patterns
---

{% wrap content%}

{% link_sample _code/off-canvas.html %}
  <img src="imgs/off-canvas.svg">
  试一试
{% endlink_sample %}


与垂直排列内容不同，这个示例中通过 `transform: translate(-250px, 0)` 隐藏了两个内容 `div`。

通过使用 JavaScript 添加或删除样式来显示或隐藏内容。

当屏幕变得更宽时，会移除将元素设置为屏幕外的样式，将内容显示在可视范围内中。

注意：在这个示例中，iOS 6 中的 Safari 浏览器和 Android 浏览器并不支持 `flexbox`  的 `flex-flow: row nowrap` 属性，
所以我们必须使用绝对定位的方式。

使用这种设计模式的网站包括：

 * [HTML5Rocks
  Articles](http://www.html5rocks.com/en/tutorials/developertools/async-call-stack/)
 * [Google Nexus](http://www.google.com/nexus/)
 * [Facebook's Mobile Site](https://m.facebook.com/)

{% include_code _code/off-canvas.html ocanvas css %}

{% include modules/nextarticle.liquid %}

{% endwrap %}

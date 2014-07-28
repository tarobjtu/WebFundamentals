---
layout: article
title: "设置视口"
description: "Much of the web isn't optimized for those multi-device experiences. Learn the
             fundamentals to get your site working on mobile, desktop or anything else with a screen."
introduction: "针对设备优化的页面需要在文档头部加上meta视口元素，视口标签可以告诉浏览器网页的纬度和缩放程度是什么。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
collection: rwd-fundamentals
key-takeaways:
  set-viewport:
    - 用meta视口标签来控制浏览器视口的宽度和缩放程度。
    - 添加 <code>width=device-width</code> 来适应不同的密度无关像素(device independent pixels)时屏幕的宽度。
    - 添加 <code>initial-scale=1</code>，使得CSS中的像素和密度无关像素的对应关系是1:1的。
    - 如果用户不能缩放页面的话，要确保你的页面还是可用的。
  size-content-to-vp:
    - 如果要在元素上使用固定宽度，数值不能太大。
    - 不能以某一个特定的视口尺寸作为内容的渲染标准。
    - 用CSS媒体查询来定义不同尺寸的屏幕所需要的不同的样式。
  media-queries:
    - Media queries can be used to apply styles based on device characteristics.
    - Use <code>min-width</code> over <code>min-device-width</code> to ensure the broadest experience.
    - Use relative sizes for elements to avoid breaking layout.
  choose-breakpoints:
    - Create breakpoints based on content, never on specific devices, products or brands.
    - Design for the smallest mobile device first, then progressively enhance the experience as more screen real estate becomes available.
    - Keep lines of text to a maximum of around 70 or 80 characters.
remember:
  use-commas:
    - 用逗号来分隔这些属性，以保证老式浏览器的兼容性。
---
{% wrap content %}

<style>
  .smaller-img {
    width: 60%;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

  video.responsiveVideo {
    width: 100%;
  }
</style>


{% include modules/toc.liquid %}

{% include modules/takeaway.liquid list=page.key-takeaways.set-viewport %}

为了提供最好的用户体验，移动端的浏览器会按照桌面端的屏幕宽度来渲染页面（通常是980px左右，这个值会根据设备的不同有所浮动），为了更容易地阅读页面，字体会相应的加大，内容也会有所缩放来适应屏幕。对于用户来说，这么做的结果就是页面上的字体可能忽大忽小，还可能需要双击或者捏动缩放屏幕才能看清内容。

{% highlight html %}
<meta name="viewport" content="width=device-width, initial-scale=1.0">
{% endhighlight %}

用meta视口的`width=device-width`来控制页面以适应密度无关像素的屏幕的宽度，这样页面就在回流的时候可以适应不同的屏幕尺寸，无论是在小屏幕的移动端或者是大屏幕的桌面端都可以适应。

<div class="clear">
  <div class="g--half">
    {% link_sample _code/vp-no.html %}
      <img src="imgs/no-vp.png" class="smaller-img" srcset="imgs/no-vp.png 1x, imgs/no-vp-2x.png 2x" alt="Page without a viewport set">
      查看示例
    {% endlink_sample %}
  </div>

  <div class="g--half g--last">
    {% link_sample _code/vp.html %}
      <img src="imgs/vp.png" class="smaller-img"  srcset="imgs/vp.png 1x, imgs/vp-2x.png 2x" alt="Page with a viewport set">
      查看示例
    {% endlink_sample %}
  </div>
</div>

当横屏的时候，有些浏览器会保持页面的宽度不变然后放大屏幕，而不是用回流重新加载出页面。添加`initial-scale=1`属性，使得无论手持设备的方向是怎么样的，CSS的像素和密度无关像素都是1:1的关系，另外还能让页面占满整个横屏宽度。

{% include modules/remember.liquid inline="True" list=page.remember.use-commas %}

## 确保视口可用

除了要设置`initial-scale`,你还可以设置针对视口应用`minimum-scale`、`maximum-scale`还有`user-scalable`属性。不过一旦这几个属性设置好了，用户就没法随意缩放视口了，这对视口的可用性造成了一定问题。

{% include modules/nextarticle.liquid %}

{% endwrap %}

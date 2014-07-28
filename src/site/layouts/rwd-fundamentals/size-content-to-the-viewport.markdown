---
layout: article
title: "内容大小适应视口"
description: "Much of the web isn't optimized for those multi-device experiences. Learn the
             fundamentals to get your site working on mobile, desktop or anything else with a screen."
introduction: "无论是在桌面设备还是移动设备上，用户总是习惯性垂直地浏览网页而不是横向地浏览。强制用户更改浏览页面的习惯，或者需要缩小页面才能看到它的全貌，这些都是很差的用户体验。"
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 2
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
    - Use a comma to separate attributes to ensure older browsers can properly parse the attributes.
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

{% include modules/takeaway.liquid list=page.key-takeaways.size-content-to-vp %}

当你使用`meta viewport`标签开发一个移动站点的时候，常常不小心就创建出不兼容部分视口的页面。举例来说，如果一个图片的宽度超过视口的宽度，就会出现横向滚动条。你需要调整内容来适应视口的宽度，以免出现横向滚动条。 

不同的设备CSS的像素点在屏幕维度和宽度是不一样的（例如手机和平板之间，甚至不同的手机屏幕都不一样），不能用特定的视口宽度来渲染内容。

对页面上的元素设置较大的固定宽度（下面的例子所示），会导致在屏幕小的设备上,层超出视口的宽度（例子：320px分辨率的设备屏幕，例如iPhone）。所以你需要考虑使用相对的宽度值，比如百分比（例如：width: 100%;）。相似地，在使用数值较大的绝对对的定位时也要小心，小屏幕上可能会出现元素溢出到视口外面的情况。

<div class="clear">
  <div class="g--half">
    {% link_sample _code/vp-fixed.html %}
      <img src="imgs/vp-fixed-iph.png" srcset="imgs/vp-fixed-iph.png 1x, imgs/vp-fixed-iph-2x.png 2x"  alt="Page with a 344px fixed width element on an iPhone.">
      查看例子
    {% endlink_sample %}
  </div>

  <div class="g--half g--last">
    {% link_sample _code/vp-fixed.html %}
      <img src="imgs/vp-fixed-n5.png" srcset="imgs/vp-fixed-n5.png 1x, imgs/vp-fixed-n5-2x.png 2x"  alt="Page with a 344px fixed width element on a Nexus 5.">
      查看例子
    {% endlink_sample %}
  </div>
</div>

{% include modules/nextarticle.liquid %}

{% endwrap %}

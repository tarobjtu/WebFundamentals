---
layout: section
title: "响应式网页设计基础"
description: "Much of the web isn't optimized for those multi-device experiences. Learn the
             fundamentals to get your site working on mobile, desktop or anything else with a screen."
introduction: "The use of mobile devices to surf the web is growing at an astronomical pace,
              but unfortunately much of the web isn't optimized for those mobile devices. Mobile
              devices are often constrained by display size and require a different approach
              to how content is laid out on screen."
article:
  written_on: 2014-04-30
  updated_on: 2014-04-30
  order: 1
rel:
  gplusauthor: https://plus.google.com/+PeteLePage
  twitterauthor: "@petele"
id: rwd-fundamentals
collection: multi-device-layouts

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

<div class="media media--video">
  <iframe src="https://www.youtube.com/embed/oK09n_PGhTo?controls=2&modestbranding=1&showinfo=0&utm-source=crdev-wf" frameborder="0" allowfullscreen=""></iframe>
</div>

平板手机、平板、桌面电脑、游戏机、电视还有可穿戴设备……现在各种各样的设备导致了屏幕尺寸也是五花八门。而且在未来，屏幕的尺寸也会越来越不同，为了跟上这趋势，你的站点应该要尽量去适应各种屏幕尺寸才行。

{% link_sample _code/weather.html %}
  <video autoplay loop controls class="responsiveVideo">
    <source src="videos/resize.webm" type="video/webm">
    <source src="videos/resize.mp4" type="video/mp4">
  </video>
{% endlink_sample %}

Ethan Marcotte 最先在[A List Apart](http://alistapart.com/article/responsive-web-design/)中定义了响应式网页设计：网页可以根据用户正在使用的设备来做出响应，布局的更改是基于设备的大小和容量。举例来说，在一部手机上，用户会看到一栏的内容；在平板上，可能内容还是相同的，但是是分两栏呈现的。

{% include modules/nextarticle.liquid %}

{% endwrap %}

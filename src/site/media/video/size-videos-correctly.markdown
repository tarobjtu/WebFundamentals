---
layout: article
title: "正确调整视频大小"
description: " 当关系到保持用户愉悦度时，视频大小就显得尤为重要了。"
introduction: "当关系到保持用户愉悦度时，视频大小就显得尤为重要了。"
translator: <a href="http://crimx.com" target="_blank">黄杰华（StrayBugs）</a>
reviewer: （待校正）
article:
  written_on: 2014-04-16
  updated_on: 2014-08-01
  order: 3
collection: videos
key-takeaways:
  add-a-video:
    - Use the video element to load, decode, and play video on your site.
    - Produce video in multiple formats to cover a range of mobile platforms.
    - Size videos correctly; ensure they don't overflow their containers.
    - Accessibility matters; add the track element as a child of the video element.
remember:
  media-fragments:
    - The Media Fragments API is supported on most platforms, but not on iOS.
    - Make sure Range Requests are supported by your server. Range Requests are enabled by default on most servers, but some hosting services may turn them off.
  dont-overflow:
    - 不要强行改变视频的宽高比。压扁或者拉伸都会很难看。
  accessibility-matters:
    - The track element is supported on Chrome for Android, iOS Safari, and all current browsers on desktop except Firefox (see <a href="http://caniuse.com/track" title="Track element support status">caniuse.com/track</a>). There are several polyfills available too. We recommend <a href='//www.delphiki.com/html5/playr/' title='Playr track element polyfill'>Playr</a> or <a href='//captionatorjs.com/' title='Captionator track'>Captionator</a>.
  construct-video-streams:
    - MSE is supported by Chrome and Opera on Android, and in Internet Explorer 11 and Chrome for desktop, with support planned for <a href='http://wiki.mozilla.org/Platform/MediaSourceExtensions' title='Firefox Media Source Extensions implementation timeline'>Firefox</a>.
  optimize:
    - <a href="../images/">Images</a>
    - <a href="../../performance/optimizing-content-efficiency/">Optimizing content efficiency</a>
---

{% wrap content%}

{% include modules/toc.liquid %}

<style>

  img, video, object {
    max-width: 100%;
  }

  img.center {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }

</style>

当关系到保持用户愉悦度时，视频大小就显得尤为重要了。

* 使用大尺寸和高质量视频时注意不要超出平台的承受范围。
* 视频应尽可能的短。
* 过长的视频可能会引起下载和加载的中断；有的浏览器会等待视频下载完才开始播放。


## 检测视频的大小

视频真正的编码帧大小有可能与视频元素的大小不一样（就像图片不一定按照它本身的大小显示）。

要检测视频编码的大小，可以用视频元素的 `videoWidth` 和 `videoHeight` 属性。而 `width` 和 `height` 则返回视频元素的大小，这两个值可能已被 CSS 或内联 width 和 height 属性修改了。


## 保证视频不会溢出容器

当视频元素大小超过窗口时就有可能会溢出容器，此时用户将无法看到完整的内容或使用上面的控件。

<div class="clear">
    <img class="g-wide--1 g-medium--half" alt="Android Chrome screenshot, portrait: unstyled video element overflows viewport" src="images/Chrome-Android-portrait-video-unstyled.png">
    <img class="g-wide--2 g-wide--last g-medium--half g--last" alt="Android Chrome screenshot, landscape: unstyled video element overflows viewport" src="images/Chrome-Android-landscape-video-unstyled.png">
</div>

你可以通过 JavaScript 或 CSS 控制视频大小。像 [FitVids](//fitvidsjs.com/) 之类的 JavaScript 库或插件可以方便地保持适当的大小和宽高比，甚至可以用在 YouTube 和其它源的 Flash 视频上。

使用 [CSS media queries](../../layouts/rwd-fundamentals/#use-css-media-queries-for-responsiveness) 媒体查询 (CSS media queries)去指定元素的大小随窗口尺寸变化而变化; `max-width: 100%` 会是你的好朋友。

{% include modules/remember.liquid title="Remember" list=page.remember.dont-overflow %}

对于 iframes 中的媒体内容（像 YouTube 视频），可以采用响应式的方法（比如这个 [由 John Surdakowski 提出的](//avexdesigns.com/responsive-youtube-embed/) ）。

**CSS:**

{% include_code _code/responsive_embed.html styling css %}

**HTML:**

{% include_code _code/responsive_embed.html markup html %}

对比 {% link_sample _code/responsive_embed.html %}响应式样例{% endlink_sample %} 和 {% link_sample _code/unyt.html %}非响应式样例{% endlink_sample %}。


{% include modules/nextarticle.liquid %}

{% endwrap %}

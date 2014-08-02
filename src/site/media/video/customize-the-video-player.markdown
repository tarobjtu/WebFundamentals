---
layout: article
title: "自定义视频播放器"
description: " 不同平台播放视频的方式不同。移动平台的解决方案需要考虑设备的方向（横向或者纵向视图）。使用全屏API来控制视频内容的全屏视图。"
introduction: "不同平台播放视频的方式不同。移动平台的解决方案需要考虑设备的方向（横向或者纵向视图）。使用全屏API来控制视频内容的全屏视图。"
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
    - Don't force element sizing that results in an aspect ratio different from the original
      video. Squashed or stretched looks bad.
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


不同平台播放视频的方式不同。移动平台的解决方案需要考虑设备的方向（横向或者纵向视图）。使用全屏API来控制视频内容的全屏视图。

## 跨设备的设备方向检测


在台式显示器或者笔记本电脑上很少会考虑设备的方向，但如果要在手机和平板上做网页设计，设备的方向就尤为重要了。

iPhone上的Safari对横竖方向转换的支持就做得很好:

<div class="clear">
    <img class="g-wide--1 g-medium--half" alt="Screenshot of video playing in Safari on iPhone, portrait" src="images/iPhone-video-playing-portrait.png">
    <img class="g-wide--2 g-wide--last g-medium--half g--last" alt="Screenshot of video playing in Safari on iPhone, landscape" src="images/iPhone-video-playing-landscape.png">
</div>

而iPad与Chrome for Android对设备方向的支持则可能会出现问题。比如，在iPad的横向模式上播放无任何配置的视频就会是这个样子：

<img class="center" alt="Screenshot of video playing in Safari on iPad Retina, landscape"
src="images/iPad-Retina-landscape-video-playing.png">

在CSS上设置视频 `width: 100%` 或者 `max-width: 100%` 可以解决大部分的设备横向布局问题。你也可以使用考虑全屏的解决方案。

## 页内或全屏播放

不同平台播放视频的方式不一样。iPhone上的Safari会在页内显示视频元素，而播放时会进入全屏：

<img class="center" alt="Screenshot of video element on iPhone, portrait" src="images/iPhone-video-with-poster.png">

在安卓上，视频默认在页内播放，用户可以按全屏按钮请求全屏:

<img class="center" alt="Screenshot of video playing in Chrome on Android, portrait" src="images/Chrome-Android-video-playing-portrait-3x5.png">

iPad上的Safari在页内播放视频：

<img class="center" alt="Screenshot of video playing in Safari on iPad Retina, landscape" src="images/iPad-Retina-landscape-video-playing.png">

## 控制全屏内容

对于不支持全屏播放的平台，可以使用[广泛支持](//caniuse.com/fullscreen)的全屏API。用这个API去控制全屏内容或者页面。

要全屏一个元素，比如一个视频：
{% highlight javascript %}
elem.requestFullScreen();
{% endhighlight %}

使整个document对象全屏:
{% highlight javascript %}
document.body.requestFullScreen();
{% endhighlight %}

还可以监听全屏状态转换:
{% highlight javascript %}
video.addEventListener("fullscreenchange", handler);
{% endhighlight %}

或者检测一个元素是否正处于全屏模式:
{% highlight javascript %}
console.log("In full screen mode: ", video.displayingFullscreen);
{% endhighlight %}

还可以用CSS伪类 `:fullscreen` 去改变元素在全屏模式下的样式。

在支持全屏API的设备上，可以考虑用缩略图作为视频的占位符:

<video autoplay loop class="center">
  <source src="video/fullscreen.webm" type="video/webm">
  <source src="video/fullscreen.mp4" type="video/mp4">
  <p>This browser does not support the video element.</p>
</video>

点击{% link_sample _code/fullscreen.html %}示例{% endlink_sample %}，看查看完整的效果。

**注意:** `requestFullScreen()` 当前还处在测试阶段，可能需要额外的代码来实现完整的跨浏览器支持。

{% include modules/nextarticle.liquid %}

{% endwrap %}

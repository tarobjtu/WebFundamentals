---
layout: article
title: "可访问性很重要"
description: " 可访问性不是一个特性。"
introduction: "可访问性不是一个特性。缺少了字幕和描述，有视力或听力障碍的用户根本无法去了解一个视频。相比糟糕的用户体验，
               添加此类内容花费的时间不算什么。所以，为所有用户都提供一个基本的用户体验吧。"
translator: <a href="http://crimx.com" target="_blank">黄杰华（StrayBugs）</a>
reviewer: （待校正）
article:
  written_on: 2014-04-16
  updated_on: 2014-08-01
  order: 4
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
    - Chrome for Android，iOS Safari 和当前所有的桌面浏览器都支持轨道元素，除了火狐（参见 <a href="http://caniuse.com/track" title="Track element support status">caniuse.com/track</a>）。 可以用填充物（polyfills）替代，我们推荐 <a href='//www.delphiki.com/html5/playr/' title='Playr track element polyfill'>Playr</a> 或者 <a href='//captionatorjs.com/' title='Captionator track'>Captionator</a>。
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


## 引入字幕来增加可访问性

利用轨道元素 `<track>` 添加字幕或描述来增加媒体在移动设备上的可访问性。

{% include modules/remember.liquid title="Remember" list=page.remember.accessibility-matters %}

使用了轨道元素后，字幕看起来是这样的：

 <img class="center" alt="Screenshot showing captions displayed using the track element in Chrome on Android" src="images/Chrome-Android-track-landscape-5x3.jpg">

## 添加轨道元素

为视频添加字幕很简单，就是添加一个轨道元素作为视频元素的孩子：

{% include_code _code/track.html track html %}

轨道元素的 `src` 属性提供了轨道文件的位置。

## 在轨道文件中定义字幕

轨道文件使用 WebVTT 格式描述时间的开始:

    WEBVTT

    00:00.000 --> 00:04.000
    Man sitting on a tree branch, using a laptop.

    00:05.000 --> 00:08.000
    The branch breaks, and he starts to fall.

    ...

{% include modules/nextarticle.liquid %}

{% endwrap %}

---
layout: article
title: "传统平台的替代品"
description: "并不是所有平台都支持所有的视频格式，检查一下主流平台所支持的视频格式，并且确保你的视频在这些主流平台中都可以运行。"
introduction: "并不是所有平台都支持所有的视频格式，检查一下主流平台所支持的视频格式，并且确保你的视频在这些主流平台中都可以运行。"
article:
  written_on: 2014-04-16
  updated_on: 2014-08-01
  order: 2
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

## 所支持的视频格式

使用 `canPlayType(`) 可找出所支持的视频格式。该方法有一个由 `mime-type` 和可选的解码器组成的字符串变量，返回下面这些值：

<table class="table">
  <thead>
    <tr>
      <th>返回值</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Return value">(空字符串)</td>
      <td data-th="Description">不支持容器和/或解码器。</td>
    </tr>
    <tr>
      <td data-th="Return value"><code>maybe</code></td>
      <td data-th="Description">
        或许支持容器和解码器，但浏览器将需要下载一些视频来验证。
      </td>
    </tr>
    <tr>
      <td data-th="Return value"><code>probably</code></td>
      <td data-th="Description">显然支持该格式。
      </td>
    </tr>
  </tbody>
</table>

这里有些范例， `canPlayType()` 的参数和在Chrome运行时的返回值：


<table class="table">
  <thead>
    <tr>
      <th>类型</th>
      <th>返回值</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Type"><code>video/xyz</code></td>
      <td data-th="Response">(空字符串)</td>
    </tr>
    <tr>
      <td data-th="Type"><code>video/xyz; codecs="avc1.42E01E, mp4a.40.2"</code></td>
      <td data-th="Response">(空字符串)</td>
    </tr>
    <tr>
      <td data-th="Type"><code>video/xyz; codecs="nonsense, noise"</code></td>
      <td data-th="Response">(空字符串)</td>
    </tr>
    <tr>
      <td data-th="Type"><code>video/mp4; codecs="avc1.42E01E, mp4a.40.2"</code></td>
      <td data-th="Response"><code>probably</code></td>
    </tr>
    <tr>
      <td data-th="Type"><code>video/webm</code></td>
      <td data-th="Response"><code>maybe</code></td>
    </tr>
    <tr>
      <td data-th="Type"><code>video/webm; codecs="vp8, vorbis"</code></td>
      <td data-th="Response"><code>probably</code></td>
    </tr>
  </tbody>
</table>


## 生成多种格式的视频

有很多工具可以把同一视频保存为其他格式：

* 桌面工具： [FFmpeg](//ffmpeg.org/)
* GUI 应用程序： [Miro](//www.mirovideoconverter.com/),
  [HandBrake](//handbrake.fr/), [VLC](//www.videolan.org/)
* 在线编码/转码服务：
  [Zencoder](//en.wikipedia.org/wiki/Zencoder),
  [Amazon Elastic Encoder](//aws.amazon.com/elastictranscoder)

## 检测所使用的视频格式

想知道浏览器实际支持哪些视频格式么？

在 JavaScript 中，使用视频的  `currentSrc` 属性，可返回所使用的源。

想看这个操作的话，可以查看{% link_sample _code/video-main.html %}这个示例{% endlink_sample %}：Chrome 和 Firefox 选用 `chrome.webm`（因为它是这两个浏览器所支持的视频格式列表的第一个条目），而 Safari 选用 `chrome.mp4`。

{% include modules/nextarticle.liquid %}

{% endwrap %}

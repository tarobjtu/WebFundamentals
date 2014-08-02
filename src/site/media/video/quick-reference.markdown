---
layout: article
title: "视频元素快速参考"
description: "简要概述了视频元素上的属性"
introduction: "简要概述了视频元素上的属性"
article:
  written_on: 2014-04-16
  updated_on: 2014-08-01
  order: 5
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

## 视频元素属性

要查看完整的视频元素属性和定义，参阅[视频元素规范](//www.w3.org/TR/html5/embedded-content-0.html#the-video-element)。

<table class="table">
  <thead>
      <th>属性</th>
      <th>有效性</th>
      <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td data-th="Attribute"><code>src</code></td>
      <td data-th="Availability">所有浏览器</td>
      <td data-th="Description">视频的地址（URL）</td>
    </tr>
    <tr>
      <td data-th="Attribute"><code>poster</code></td>
      <td data-th="Availability">所有浏览器</td>
      <td data-th="Description">视频封面地址（URL），视频元素加载之后即刻显示，无需下载视频内容</td>
    </tr>
    <tr>
      <td data-th="Attribute"><code>preload</code></td>
      <td data-th="Availability">所有移动设备浏览器都忽略此属性</td>
      <td data-th="Description">在视频播放之前提示浏览器预加载元数据（或部分视频）是值得的。属性的取值有 none 、 metadata 或 auto （详情请参阅下面预加载部分）</td>
    </tr>
    <tr>
      <td data-th="Attribute"><code>autoplay</code></td>
      <td data-th="Availability">iPhone 与 Android 不支持，所有桌面浏览器、iPad、火狐和 Opera for Android 支持</td>
      <td data-th="Description">尽早开始下载和播放。（参阅下面自动播放部分）</td>
    </tr>
    <tr>
      <td data-th="Attribute"><code>loop</code></td>
      <td data-th="Availability">所有浏览器</td>
      <td data-th="Description">循环播放视频</td>
    </tr>
    <tr>
      <td data-th="Attribute"><code>controls</code></td>
      <td data-th="Availability">所有浏览器</td>
      <td data-th="Description">显示默认的视频控制（播放、暂停、等等）</td>
    </tr>
  </tbody>
</table>

### 自动播放（Autoplay）

对于桌面版，`autoplay` 告诉浏览器尽可能早的开始下载和播放。在 iOS 和 Chrome for Android 上，`autoplay` 是无效的，用户必须点击屏幕去播放视频。

即使在支持自动播放的平台上，你也要考虑启用它是不是一个好主意：

* 数据流量有可能是昂贵的。
* 不经询问，一开始就下载和播放会不经意的占用带宽和 CPU，延迟了页面的渲染。
* 用户所处的环境可能不适合播放视频和音频。

自动播放行为可以在 Android 网络视图（WebView）通过 [WebSettings API](//developer.android.com/reference/android/webkit/WebSettings.html#setMediaPlaybackRequiresUserGesture(boolean)) 配置。它默认是 true 但一个网络视图应用程序可以选择禁用它。

### 预加载（Preload）

`preload` 属性提示浏览器应该预加载多少信息和内容。

<table>
  <thead>
    <tr>
      <th>值</th>
      <th>描述</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Value"><code>none</code></td>
      <td data-th="Description">用户可能不看这个视频，不要预加载任何东西</td>
    </tr>
    <tr>
      <td data-th="Value"><code>metadata</code></td>
      <td data-th="Description">预加载元数据（时长、尺寸、字幕轨）以及最小限度的视频</td>
    </tr>
    <tr>
      <td data-th="Value"><code>auto</code></td>
      <td data-th="Description">允许马上下载整个视频</td>
    </tr>
  </tbody>
</table>

`preload` 属性在不同的平台上有不同的效果。比如，Chrome 的桌面版会缓冲25秒的视频，但 iOS 与 Android 版则不会。这意味着在移动版上会出现桌面版所没有的播放启动延迟。详情参阅 [Steve Souders' test page](//stevesouders.com/tests/mediaevents.php)。

## JavaScript

[The HTML5 Rocks Video article](//www.html5rocks.com/en/tutorials/video/basics/#toc-javascript) 很好的总结了控制视频播放的 JavaScript 属性、方法和事件。我们这里已经包括了这些内容，并更新了与移动方面相关的一些内容。

### 属性（Properties）

<table class="table">
  <thead>
    <th>属性</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td data-th="Property"><code>currentTime</code></td>
      <td data-th="Description">以秒为单位获取或设置播放位置</td>
    </tr>
    <tr>
      <td data-th="Property"><code>volume</code></td>
      <td data-th="Description">获取或设置视频当前的音量</td>
    </tr>
    <tr>
      <td data-th="Property"><code>muted</code></td>
      <td data-th="Description">获取或设置音频静音状态</td>
    </tr>
    <tr>
      <td data-th="Property"><code>playbackRate</code></td>
      <td data-th="Description">获取或设置播放速率；1 为正常速率正向播放</td>
    </tr>
    <tr>
      <td data-th="Property"><code>buffered</code></td>
      <td data-th="Description">有关视频已缓冲多少，是否准备好播放的信息。参阅 <a href="http://people.mozilla.org/~cpearce/buffered-demo.html" title="Demo displaying amount of buffered video in a canvas element">样例</a> </td>
    </tr>
    <tr>
      <td data-th="Property"><code>currentSrc</code></td>
      <td data-th="Description">正在播放的视频的地址</td>
    </tr>
    <tr>
      <td data-th="Property"><code>videoWidth</code></td>
      <td data-th="Description">视频的宽度，以像素为单位（与视频元素的 width 不同）</td>
    </tr>
    <tr>
      <td data-th="Property"><code>videoHeight</code></td>
      <td data-th="Description">视频的高度，以像素为单位（与视频元素的 height 不同）</td>
    </tr>
  </tbody>
</table>

移动设备不支持 playbackRate（{% link_sample _code/scripted.html %}样例{% endlink_sample %}）和 volume 。

### 方法（Methods）

<table class="table">
  <thead>
    <th>方法</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td data-th="Method"><code>load()</code></td>
      <td data-th="Description">加载或重新加载视频源而不启动播放（比如用 JavaScript 改变视频的 src 的时候）</td>
    </tr>
    <tr>
      <td data-th="Method"><code>play()</code></td>
      <td data-th="Description">在当前进度开始播放视频</td>
    </tr>
    <tr>
      <td data-th="Method"><code>pause()</code></td>
      <td data-th="Description">在当前进度暂停视频</td>
    </tr>
    <tr>
      <td data-th="Method"><code>canPlayType('format')</code></td>
      <td data-th="Description">找出支持哪些格式（参阅检查支持哪些格式）</td>
    </tr>
  </tbody>
</table>

在移动设备上（除了 Opera 和 Android）play() 和 pause() 只有在响应用户动作的时候才有效，比如点击一个按钮（参阅 {% link_sample _code/scripted.html %}样例{% endlink_sample %}）。同样地，对于嵌入 YouTube 视频之类的内容也不能启动播放。

### 事件（Events）

这只是可能发射的[媒体事件](//developer.mozilla.org/docs/Web/Guide/Events/Media_events)的一个子集。完整的列表请参阅 Mozilla 开发者社群上的媒体事件页面。

<table class="table">
  <thead>
    <th>事件</th>
    <th>描述</th>
  </thead>
  <tbody>
    <tr>
      <td data-th="Event"><code>canplaythrough</code></td>
      <td data-th="Description">当足够的数据可用，浏览器认为视频可以不中断播放完毕时发射</td>
    </tr>
    <tr>
      <td data-th="Event"><code>ended</code></td>
      <td data-th="Description">视频播放完毕时发射</td>
    </tr>
    <tr>
      <td data-th="Event"><code>error</code></td>
      <td data-th="Description">错误发生时发射</td>
    </tr>
    <tr>
      <td data-th="Event"><code>playing</code></td>
      <td data-th="Description">当视频第一次开始播放、按下暂停之后或者重新开始时发射</td>
    </tr>
    <tr>
      <td data-th="Event"><code>progress</code></td>
      <td data-th="Description">周期性地发射，显示下载进度</td>
    </tr>
    <tr>
      <td data-th="Event"><code>waiting</code></td>
      <td data-th="Description">当一个动作被延迟，在等待另一个动作完成时发射</td>
    </tr>
    <tr>
      <td data-th="Event"><code>loadedmetadata</code></td>
      <td data-th="Description">当浏览器加载完元数据（时间、尺寸、字幕）时发射</td>
    </tr>
  </tbody>
</table>

{% include modules/nextarticle.liquid %}

{% endwrap %}
